## What You Need for This Project

-   A Rooted Android Emulator

## Purpose

To observe network transmissions from an insecure app, and prove that they are not encrypted properly.

## Background

This problem is gaining recognition, so few apps still have this flaw. The app below used plaintext network transmission on Mar 26, 2021, but eventually it may be fixed or removed.

## Use Android 11

The app won't run on more modern Android versions, such as Android 16.

## Installing a Vulnerable App

This App is no longer available in Google Play, as of August, 2022, so we'll use an archived APK file.

Download this APK file:

**[traveler.apk](https://samsclass.info/128/proj/traveler.apk)**

Drag and drop that file onto your Android Emulator to install the app.

> The website this app uses for logging in went down in 2025, so this process is necessary to redirect to a server that is up.
> 
> ## Installing Platform-Tools
> 
> Launch Android Studio. From the menu bar, click  **Tools**, "**SDK Manager**".
> 
> In the Preferences box, click the "**SDK Tools**" tab.
> 
> Make sure both these items are installed, as shown below:
> 
> -   **Android SDK Command-line Tools**
> -   **Android SDK Platform-Tools**
> 
> ![](https://samsclass.info/128/proj/M200-1.png)
> 
> ## Launching ADB
> 
> In the SDK Manager window, notice the Android SDK Location, outlined in green in the image above.
> 
> Open a Terminal or Command Prompt window and execute these commands, as shown below, replacing the path in the first command with the Android SDK Location on your system:
> 
> > cd /Users/sambowne/Library/Android/sdk
> > cd platform-tools
> > ./adb version
> 
> You see an adb version number, as shown below.
> 
> ![](https://samsclass.info/128/proj/M105a-9.png)
> 
> ## Changing the Hosts File
> 
> Execute these commands:
> 
> > ./adb shell
> > su
> > reboot -p
> > ../emulator/emulator -list-avds
> 
> Note the name of your Android Virtual Device (AVD), as shown below.
> 
> ![](https://samsclass.info/128/proj/M105a-6.png)
> 
> Execute this command, making sure the name of your AVD is correct:
> 
> > ../emulator/emulator -writable-system -avd Pixel_3a_XL_API_30_2
> 
> Your emulator launches.
> 
> On your host system, open a new Terminal and execute these commands, adjusting the first one to correctly find the sdk on your system:
> 
> > cd /Users/sambowne/Library/Android/sdk
> > cd platform-tools
> > ./adb root
> > ./adb remount
> > ./adb shell
> > su
> > cat /etc/hosts
> 
> You should see your hosts file, as shown below.
> 
> ![](https://samsclass.info/128/proj/M105a-7.png)
> 
> Execute these commands:
> 
> > echo 1.1.1.1 traveler247.com >> /etc/hosts
> > cat /etc/hosts
> 
> The hosts file now contains a line for traveler247.com, as shown below.
> 
> ![](https://samsclass.info/128/proj/M105a-8.png)

## Starting Wireshark

On your host system, launch Wireshark. If you don't have it, get it at:

[**https://www.wireshark.org/**](https://www.wireshark.org/)

In the main Wireshark window, double-click the network interface that is being used to reach the Internet. On my system, it is "**Wi-Fi: en0**", outlined in green in the image below.

![](https://samsclass.info/128/proj/p2ask6.png)

Wirehark starts displaying packets. At the top, in the Filter bar, enter this display filter:

> http

Press **Enter** to filter the traffic.

On your Android device, in the vulnerable app, enter any email and password into the login page, as shown below.

![](https://samsclass.info/128/proj/M105a-1.png)

Wireshark shows a GET request to  **/Webservice/user_login.ashx**. Click that line and expand the "**Hypertext Transfer Protocol**  item in the lower pane, as shown below.

![](https://samsclass.info/128/proj/M105a-2.png)

> ## M 105.1: Host (15 pts)
> 
> Find the text covered by a green box in the image above. That's the flag.
