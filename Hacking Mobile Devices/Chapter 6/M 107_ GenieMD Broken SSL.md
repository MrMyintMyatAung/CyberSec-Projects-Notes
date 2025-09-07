## What You Need for This Project

You need one of thest two systems:

-   A Mac or Linux computer computer with the Genymotion Android emulator installed, or
-   A Windows system capable of running VirtualBox.

## Summary

The GenieMD Android app sends login credentials over broken HTTPS, without verifying the SSL certificate.

This is such a serious security flaw that the  [FTC punished Fandango and Credit Karma for doing the same thing in 2014](https://www.ftc.gov/news-events/press-releases/2014/03/fandango-credit-karma-settle-ftc-charges-they-deceived-consumers).

## Preparing an Android Emulator and Burp

You need an Android emulator running traffic through the Burp proxy, which you should have already set up in previous projects.

If your host machine uses Mac or Linux, use Genymotion.

If your host system runs Windows, use Burp and Nox.

## Installing the GenieMD Android App

Download this APK file, and drag it onto your emulator.

Then drag the round button up from the bottom center of the home page, click the "Harvard" icon, and grant it the permissions it needs.

This worked with my Android 11 emulator on Sept 12, 2022, using Android Studio.

[**geniemd.apk**](https://www.bowneconsultingcontent.com/pub/Attack/proj/geniemd.apk)

## Adjusting Android Networking to Use the Burp Proxy

On your Android device, in Settings, tap **Wi-Fi** and adjust your proxy settings to route traffic through Burp, as shown below.

![](https://www.bowneconsultingcontent.com/pub/Attack/proj/p3burp9.png)

On your Android device, click  **SAVE**.

At the bottom center of the device, click the round  **Home**  button.

## Observing the HTTPS Traffic

On your Android device, open the **Harvard...** app.

Click "**Sign in**" and enter test credentials, as shown below.

![](https://www.bowneconsultingcontent.com/pub/Attack/proj/p4genie2.png)

Click "**SIGN IN**".

In Burp, on the Proxy tab, click the "**HTTP Requests**" sub-tab.

Find the POST method going to /GenieMD.Com/resources/Email/SignIn.

The username and password appear in Burp, as shown below:

![](https://www.bowneconsultingcontent.com/pub/Attack/proj/p4genie3.png)

If you have been doing these projects in order, and you are using a Mac, this is not a security problem, because you have the PortSwigger certificate installed--your Android device has been told to trust Burp.

In Burp, on the  **Proxy**  tab, on the "**HTTP history**" sub-tab, right-click any entry and click "**Clear history**". Click  **Yes**.

## Removing the PortSwigger Certificate

On your Android device, in Settings, click **Security**, **Advanced**, "**Encryption & credentials**", "**Clear credentials**".

Click  **OK**.

## Testing HTTPS Connections

On your Android device, open Chrome. Go to any secure page, such as **https://bowneconsulting.com**.

You should see an error message, as shown below.

![](https://www.bowneconsultingcontent.com/pub/Attack/proj/M107-4.png)

No valid HTTPS connections can be made from your device now, because it no longer trusts Burp.

> ## Using the Android Studio Emulator
> 
> My Android 11 emulator refused to send any HTTPS traffic to the Burp proxy. To fix that problem, in Settings, remove the proxy settings.
> 
> Then close Android Studio and the emulator and execute this command from a Terminal:
> 
> (The path is for a Mac; on a Windows machine the path will be something like C:\Users\{User}\AppData\Local\Android\Sdk\emulator\emulator )
> 
> > ~/Library/Android/sdk/emulator/emulator -list-avds
> 
> You see a list of your available emulators, as shown below.
> 
> ![](https://www.bowneconsultingcontent.com/pub/Attack/proj/M107-7.png)
> 
> Execute this command to start your emulator with a http-proxy, using the correct name for your emulator and changing the IP address to the listening address you set in Burp:
> 
> > ~/Library/Android/sdk/emulator/emulator -avd Pixel_3a_API_30 -no-snapshot-load -http-proxy 192.168.11.5:8080
> 
> This should redirect HTTP and HTTPS traffic to the proxy.

## Logging In Again

On your Android device, open **Harvard...** again.

Click "**Sign in**" and enter test credentials, including your name, as shown below.

![](https://www.bowneconsultingcontent.com/pub/Attack/proj/p4genie5.png)

## Capturing Credentials in Burp

In Burp, on the Proxy tab, click the "**HTTP Requests**" sub-tab.

Find the POST method going to /GenieMD.Com/resources/Email/SignIn.

The username and password still appear in Burp, as shown below:

![](https://www.bowneconsultingcontent.com/pub/Attack/proj/M107-5.png)

This is a big problem--the MITM attack is allowed. GenieMD exposes its users to this attack, because they don't bother to validate SSL certificates.

> ## M 107.1: Server (15 pts)
> 
> In Burp, in the lower pane, click the  **Response**  tab.
> 
> The flag is the text covered by a green box in the image below.
> 
> ![](https://www.bowneconsultingcontent.com/pub/Attack/proj/M107-6.png)

> ## M 107.2: Find the Server (5 pts extra)
> 
> Uninstall the original app and install this app instead:
> 
> [**A31.2.apk**](https://www.bowneconsultingcontent.com/pub/Attack/proj/A31.2.apk)
> 
> Execute a login request. The flag is the domain name of the server it sends a POST request to.

> ## M 107.3: Registration (15 pts extra)
> 
> Use the same A31.2.apk app. Launch the app. Click "**Join Now**".
> 
> It asks for a registration code, as shown below.
> 
> ![](https://www.bowneconsultingcontent.com/pub/Attack/proj/M107-1.png)
> 
> On your Kali machine, execute this command to unpack the app:
> 
> > apktool d A31.2.apk
> 
> Find the registration code. Use it in the app to see the flag, as shown below.
> 
> ![](https://www.bowneconsultingcontent.com/pub/Attack/proj/M107-2.png)
> 
> _Hint: it's easier to just find the flag message than the registration code itself.  
> But if you want to find the registration code easily, do project M 304._

> ## M 107.4: Registration (20 pts extra)
> 
> Examine the code-signing certificate for the A31.2.apk app. The company name is in leetspeak. That company name is the flag.


