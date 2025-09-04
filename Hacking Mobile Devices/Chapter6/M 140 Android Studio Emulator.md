# M 140: Android Studio Emulator (15 pts)

# M 140: Android Studio Emulator (15 pts)

## What You Need for This Project

- Any computer

## Purpose

To prepare an Android emulator, so you can easily install apps from Google Play and audit their security.

# Task 1: Installing Android Studio

## Dowloading Android Studio

In a Web browser, go to

[**https://developer.android.com/studio**](https://developer.android.com/studio)

Download the software, as shown below.

(The name of the button is "Download Android Studio Meerkat Feature Drop" as of June, 2025.)

![](https://samsclass.info/128/proj/M140-1.png)

Run the installer with the default options.

Launch Android Studio. Don't import settings. Accept the default options. Accept any agreements you are asked to.

Create a New Project.

Select the "**Basic Views**" activity, as shown below.

Click **Next**. Click **Finish**.

![](https://samsclass.info/128/proj/M140-11.png)

## Starting an Emulator

In Android Studio, on the right side, click the "

**Virtual Device Manager**

" button, highlighted in blue in the image below.

You should see a phone, like the "Medium Phone" shown below. Click the right-arrow on that phone's line to start it.

![](https://samsclass.info/128/proj/M140-12.png)

The emulator starts, as shown below.

If you are asked to, allow it to use the microphone.

![](https://samsclass.info/128/proj/M140-7.png)

To make the emulator appear in its own window, at the top right of the Emulator pane, click the gear icon, outlined in red in the image above, point to "**View Mode**", and click **Float**.

> Troubleshooting
> 
> 
> On a Mac, from the Android Studio menu bar, click "Android Studio", Preferences, Tools, Emulator. Uncheck "Launch in a tool window".
> 
> Close Android Studio and relaunch it.
> 
> If you are using a PC, the first two clicks are File, Settings.
> 
> ---
> 

## Installing Qute: Terminal Emulator

From the Android home screen, at the bottom, click the center icon to launch Google Play.

Log in with a Google account. Don't enable backups.

In Google Play, search for **Qute**, as shown below.

Install "**Qute: Terminal Emulator**".

![](https://samsclass.info/128/proj/M140-8.png)

> M 140.1: Operating System (15 pts)
> 
> 
> In the "EULA & PRIVACY POLICY" page, click "AGREE & CONTINUE".
> 
> In the "Help us get better" page, click CONTINUE.
> 
> In the "Please, grant permissions for app" page, click "GRANT PERMISSIONS".
> 
> Click the slider to allow access to all files.
> 
> At the top left, click the back-arrow.
> 
> In Qute, execute this command:
> 
> > uname -a
> > 
> 
> ![](https://samsclass.info/128/proj/M140-9.png)
> 
> ![image.png](image.png)
> 
> ---
> 

## Creating an Emulated Android 11 Device

In Android Studio, in Device Manager pane, click the plus sign.

Click "**Create Virtual Device**".

![](https://samsclass.info/128/proj/M140-2.png)

In the "Form Factor" screen, click "**Pixel 3a**" and click **Next**.

In the "Configure virtual devide" screen, select an API of "**API 30 :R:, Android 11.0**", as shown below.

In the "System Image" pane, at the bottom of the screen, click the down-arrow icon to download the system image. This arrow is outlined in red in the image below.

![](https://samsclass.info/128/proj/M140-13.png)

When the download completed, click **Finish**.

In the "Configure virtual devide" screen, click **Finish**.

---

Updated 6-9-25