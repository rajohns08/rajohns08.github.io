---
layout: post
title: Setting up a UIScrollView with Auto Layout in iOS
---

When setting up a `UIScrollView` using Auto Layout, there were a couple of tricky things that tripped me up the first time I attempted it. My personal litmus test for determining if I have set up a proper `UIScrollView` is making sure a `UILabel` word wraps correctly, so that is why I will be using a `UILabel` in this guide. Here are the steps I take now to set up a `UIScrollView`:

**1.** Assuming you are starting with a blank `UIViewController` in Storyboard, drag on a `UIScrollView`:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/1.png)
<br><br><br>

**2.** Set the leading/top/trailing/bottom constraints to 0 on the `UIScrollView`. Make sure "Constrain to margins" is NOT checked.

![_config.yml]({{ site.baseurl }}/images/UIScrollView/2.png)
<br><br><br>

**3.** Drag on a `UIView` to be a subview of your `UIScrollView`. This is the key piece of the puzzle that tripped me up for a while. We want all of our elements to be contained in this container `UIView` inside the `UIScrollView`.

![_config.yml]({{ site.baseurl }}/images/UIScrollView/3.png)
<br><br><br>

**4.** Set the leading/top/trailing/bottom constraints to 0 on the `UIView`. Again, make sure "Constrain to margins" is NOT checked.

**5.** Make your `UIScrollView` and `UIView` have equal widths by Ctrl-dragging from one to the other.

![_config.yml]({{ site.baseurl }}/images/UIScrollView/4.png)
<br><br><br>

**6.** Drag on a `UILabel` and set its leading/top/trailing (don't do bottom yet) to be 20 or whatever you like.

![_config.yml]({{ site.baseurl }}/images/UIScrollView/5.png)
<br><br><br>

**7.** Your storyboard scene probably looks something like this:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/6.png)
<br><br><br>

**8.** Press the red circle in the navigator area to view the auto layout warnings/errors:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/7.png)
<br><br><br>

**9.** Update the frame on the `UILabel` by clicking the yellow triangle next to the label view:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/8.png)
<br><br><br>

**10.** And now click the Fix Misplacement button:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/9.png)
<br><br><br>

**11.** Select your `UILabel` and set its Lines property in the attributes inspector to 0:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/10.png)
<br><br><br>

**12.** Set the bottom space to superview on the `UILabel`. After this step all auto layout warnings should go away.

![_config.yml]({{ site.baseurl }}/images/UIScrollView/11.png)
<br><br><br>

**Note:** As you add more elements to your scroll view, always make sure the bottommost element is the one with the bottom space to superview set. So if we added a button below our label, we would remove this constraint from the label and put it on the button. Also, you can adjust the constant value of this constraint to set the content size of the scroll view.

**13.** Add a few lines of text to your label and update the frames. Make sure the label word wraps correctly when viewing and running the app. At this point I know that I have set up my `UIScrollView` correctly with Auto Layout.

**Bonus Tip:** As you populate your scroll view with multiple elements in storyboard, it can become quite long. You may eventually have trouble fitting all of your elements in the storyboard scene and wonder how to continue adding elements. To accomplish this task, select the view controller scene and in the size inspector swap to a freeform simulated size:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/12.png)
<br><br><br>

Now you should be able to increase the height of the storyboard scene and keep adding elements to your view. Just make sure you also increase the bottom space to superview constant on your bottommost UI element, so the scroll view and content view increase with the new size of the storyboard scene:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/13.png)

<br><br><br>
