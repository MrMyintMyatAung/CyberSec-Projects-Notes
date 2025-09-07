## What You Need for This Project

-   A computer with Android Studio installed

## Purpose

To configure your system so the Android Debug Bridge tool can access your Android emulator.

## Installing Platform-Tools

Launch Android Studio. From the menu bar, click **Tools**, "**SDK Manager**".

In the Preferences box, click the "**SDK Tools**" tab.

Make sure both these items are installed, as shown below:

-   **Android SDK Command-line Tools**
-   **Android SDK Platform-Tools**

![](https://samsclass.info/128/proj/M200-1.png)

## Launching ADB

In the SDK Manager window, notice the Android SDK Location, outlined in green in the image above.

Open a Terminal or Command Prompt window and execute these commands, as shown below, replacing the path in the first command with the Android SDK Location on your system:

> cd /Users/sambowne/Library/Android/sdk
> cd platform-tools
> ./adb version

![](https://samsclass.info/128/proj/M200-2.png)

## Launching an Emulator

In Android Studio, close the SDK Manager window.

You should already have made an emulator in a previous project.

In Device Manager, start an emulator, as shown below.

![](https://samsclass.info/128/proj/M200-3.png)

## Connecting to your Android Device with ADB

In the Terminal or Command Prompt window you used previously, execute these commands:

> ./adb devices

You should see a device listed, as shown below.

![](https://samsclass.info/128/proj/M200-4.png)

> ## M 200.1: ADB Shell (15 pts)
> 
> In the Terminal or Command Prompt window you used previously, execute these commands:
> 
> > ./adb shell
> > uname -a
> 
> Find the text in that box that is covered by the green box in the image below. That's the flag.
> 
> ![](https://samsclass.info/128/proj/M200-5.png)



