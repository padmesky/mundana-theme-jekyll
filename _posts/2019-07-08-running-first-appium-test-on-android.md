---
title: Running First Appium Test on Android
author: havva
image: http://www.havvanurelveren.com/assets/images/first-appium-test.jpg
---

After I installed Appium on my PC, I've written my first appium test script. I used android apps of spotify and dropbox, since i didn't have my own mobile app. Here i'll show you the example for dropbox since I had a problems with spotify , i'll mention this problem at the end of the post.

Here is my firs very basic Appium test script with C# for Dropbox:
1.  Download .apk file of the Dropbox from the internet and save it in a local folder.
2.  Enable Developer Options of the device you'll use and be sure USB debugging is also enabled.
3.  When you connect the device to your Computer with USB cable set the USB connection as PTP on your device.
4.  Write your appium script and run it on your device :) I've written my appium tests with C# in Visual Stduio. This is a console application but you can apply this code to any types of  projects, it's up to you. It can be a web project or a desktop project as well.
![](/assets/images/Appium_first_test_code.jpg)
Let's take a closer look. First we should set the desired capablities which are the parameters provides information about the device and the app.

```
capabilities.SetCapability("udid", "42003fc3d449630b"); 
```

Udid is Id of your device, you can reach this information with -adb devices command on the cmd prompt:

```
capabilities.SetCapability(CapabilityType.Platform, "Android");
```

Platform indicates that the mobile operation system of your device and app like Windows Mobile, IOS or Android.

```
 capabilities.SetCapability("app", "C:/apklar/com.dropbox.android-3.0.0.12-300012-minAPI15.apk");
```
 
 Here is the file path of the .apk file of your app.

```
capabilities.SetCapability("appActivity", ".activity.LoginOrNewAcctActivity"); 
```

Activity is not always required to lunch an app since usually there is an MainActivity but since i tried to perform a login activiy here, I've needed activity. And I get the activity name from the error message shows up on the AppiumServer (Node.js command prompt)

```
capabilities.SetCapability(CapabilityType.Version, "6.0.1");
```

Version indicates that which version of the Android is loaded on your device.
```
driver = new AndroidDriver<AppiumWebElement>(new Uri("http://127.0.0.1:4723/wd/hub"), capabilities, new TimeSpan(0, 0, 180));
```
URI is the ip and port information of the Appium Server you opened. Send your Request to the Appium Server. When Appium Server takes the request, checks if the app is already installed on the device, if it's not, first installs the app and then launchs the app.

And we came to the login part, now we need to find the text fields on the screen and type user name and password and tap to sign in button on the screen just like a real person.
I used UIAutomatorViewert tool of Android to get the element ids. This tool brings you screenshot of the current screen. If you click on the element you can see the id on the right sight of the tool.(Your device must be connected to your computer with USB before taking the screenshot )
![](/assets/images/uiautomatorviewer_tool.jpg)
Only problem that I faced about UIAutomatorViewer so far is finding element ids of the dynamic pages, For example if an animation or a video plays on the screen it's not able to catch the screen. I couldn't test the Spotify, for the same reason. Of cource you can skip that page manually and continue to test other pages with automatically. Maybe there is solution of this problem but i couldn't find it yet :)

5.  Ok, finally you your script is ready to run, You just have to open a Node.Js Command Prompt and run 'Appium' command to open a Appium Sever. And Run your project.