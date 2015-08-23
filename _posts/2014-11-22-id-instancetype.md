---
layout: post
title: Objective-C, id vs instancetype
---

In Objective-C it is considered better practice to return `instancetype` from methods on a class that return a type of itself.

For example:

Animal.h

```objc
@interface Animal : NSObject

+ (id)giveMeAnimalA;
+ (instancetype)giveMeAnimalB;
+ (Animal *)giveMeAnimalC;

@end
```

Animal.m

```objc
@implementation Animal

+ (id)giveMeAnimalA {
    return [[[self class] alloc] init];
}

+ (instancetype)giveMeAnimalB {
    return [[[self class] alloc] init];
}

+ (Animal *)giveMeAnimalC {
    return [[[self class] alloc] init];
}

@end
```

In the above code, the factory method that returns `instancetype` is better practice. But why? The answer is simple. `instancetype` does type checking for us at compile time to warn us of problems.

For example, if we try to call

```objc
[[Animal giveMeAnimalA] count];
```

The compiler will warn us of nothing, but we will crash at runtime with an exception because   `Animal` doesn't have a `count` method. But why didn't the compiler warn us of this impending crash you might ask? Because we are returning the generic type `id` from that factory method. Thus even though `Animal` doesn't have a `count` method, the compiler reasons that this object could be of any type and it knows of some objects that do have a count method.

Now if we were to use our second factory method and try to call

```objc
[[Animal giveMeAnimalB] count];
```

the compiler would immediately warn us that `Animal` does not have a `count` method, and we could avoid crashing at runtime. But wouldn't it be simpler just to make our return type `Animal*`? The compiler should definitely warn us that `Animal` doesn't have a `count` method in that case, but what if we had a subclass of animal who wanted to use the same factory method?

Imagine we have a `Dog` subclass of `Animal`:

```objc
@interface Dog : Animal

- (void)makeSound;

@end
```

Now if we tried to call

```objective-c
[[Dog giveMeAnimalC] makeSound];
```

it wouldn't work because we would have been returned an `Animal` which doesn't have a `makeSound`   method. If we had used `instancetype` however, with

```objc
[[Dog giveMeAnimalB] makeSound];
```

then we could successfully call the `makeSound` method since `instancetype` would have returned us a `Dog`.

Note: This post has been in reference to factory methods specifically. "alloc", "init", and "new" methods that return `id` will automatically be converted to `instancetype` under the hood. However, it is still considered better practice to go ahead and name those return types to be `instancetype`   also to avoid any ambiguity and to stay consistent. A full sample project that illustrates this post can be found [here](https://github.com/rajohns08/codingdiscovery/tree/master/2014.11.22%20-%20InstanceType) if you want to download it and take a look for yourself.
