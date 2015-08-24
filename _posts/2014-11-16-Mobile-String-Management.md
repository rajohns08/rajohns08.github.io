---
layout: post
title: iOS and Android String Management
---

Recently I've been thinking more about following the [Don't Repeat Yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (DRY) principle in relation to mobile development. Specifically I have been contemplating how to handle string management between iOS and Android projects. Following DRY, we obviously shouldn't be repeating our strings and string keys in both our native iOS and Android environments. So recently I started googling around for potential solutions to this problem.

I found a great tool called [Twine](https://github.com/mobiata/twine) that helps solve this exact issue. Basically you create all of your strings in a central strings.txt file (hopefully kept in its own version control). You then run the twine command line tool to generate your iOS and Android native string files (.strings for iOS and .xml for Android) from your central strings.txt file. This way you only need to update your strings in one location and have them auto-generated into your individual native mobile environments.

Here is an example of how it works: create a strings.txt file anywhere you like, and fill it with something like the following:

```
[[General]]
    [unknownErrorTitle]
        en = Unknown Error
    [unknownErrorMsg]
        en = An unknown error occurred.

[[Login]]
    [signin]
        en = Sign In
    [username]
        en = Username
    [password]
        en = Password
```

The double bracket items are optional and are just for separating different logical categories. The single bracket items are required and are the keys for the strings. The 'en' means that the following should be the string for this key in the English language. That's another great feature of Twine, it handles localization! So you could add multiple strings for each key specifying the language for each string if you wanted.

Once you have your strings.txt file ready, you can generate your native strings files from it with a twine command line tool:

**`twine generate-all-string-files /Users/yourUsername/Documents/strings.txt /Users/yourUsername/Documents/YourAndroidApp/app/src/main/res`**

The above command is for generating Android strings only. For iOS the command would be something like the following:

**`twine generate-all-string-files /Users/yourUsername/Documents/strings.txt $PROJECT_DIR/$PROJECT_NAME/Locales/`**

## Automating Generation

Ok, so now we have a central place for our strings and we can generate our native strings files by running those 2 twine commands, but do we really want to have to do that every time we update the strings file?

What would be more convenient is if we could have those strings files generated automatically every time we update our central strings.txt file. To accomplish this we can take advantage of [launch daemons](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html#//apple_ref/doc/uid/10000172i-SW7-BCIEDDBJ) on OS X.

First, we need to create an executable file to handle our twine commands. Just make a new .sh file and insert the twine commands from above. Don't forget to make the file executable by running **`chmod +x yourScript.sh`**. I actually had issues using the .sh file extension so you might need to remove the extension altogether to get it to run from your launch daemon:

![_config.yml]({{ site.baseurl }}/images/GenJudgeStringsGetInfo.png)

It is not enough to just remove the extension in the file name in Finder, you have to open up "Get Info" on the file and remove the extension from there as shown above. "GenJudgeStrings" above is just the name of my script with the twine commands. Yours can be whatever you like.

Now that we have our script for generating the native strings files, we need to make something call that script anytime our strings.txt file is updated. Here is where the launch daemon comes in. Make a .plist file with the following format:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
   <key>Label</key>
   <string>com.rajohns.stringwatcher</string>
   <key>ProgramArguments</key>
   <array>
      <string>/Users/rajohns/Desktop/GenJudgeStrings</string>
   </array>
   <key>RunAtLoad</key>
   <true/>
   <key>WatchPaths</key>
    <array>
        <string>/Users/rajohns/Documents/strings.txt</string>
    </array>
</dict>
</plist>
```

You should change the string under Label to be whatever you want your label to be. The string in the ProgramArguments array is the file that you want to be executed (the script you just created), and the string under the WatchPaths key is the file we want to watch (our strings.txt file). The `RunAtLoad` key set to true just says that this daemon should run when it is loaded.

Make sure to paste your .plist file in `/Users/yourUsername/Library/LaunchAgents/` and it should automatically start every time you login on Mac OS X.

Now we have a central place for our strings for iOS and Android, and when we update our central strings.txt file our native strings files will be automatically and immediately generated. Mission accomplished.

<br><br><br>
