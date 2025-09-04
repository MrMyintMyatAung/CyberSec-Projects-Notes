## What You Need for This Project

-   A computer with Android Studio and an emulator installed, which you prepared in a previous project.

## Purpose

To get Android and Burp working, so you can perform man-in-the-middle traffic interception, to detect SSL certificate validation errors.

## Installing Burp

Burp is a very popular proxy, enabling you to view and alter network traffic.

In a Web browser, go to  [https://portswigger.net/burp/communitydownload](https://portswigger.net/burp/communitydownload)

Download the Community Edition and install it.

> ## Ubuntu Users
> 
> If you are using Ubuntu, execute these commands:
> 
> > cd
> > cd Downloads
> > ls -l
> 
> You should see the name of the downloaded file, which should be something like  **burpsuite_free_v1.6.01.jar**. Use that name in the commands below:
> 
> > cd
> > cd Downloads
> > sudo mkdir /opt/burp
> > sudo mv burpsuite_free_v1.6.01.jar /opt/burp
> > cd /opt/burp
> > sudo touch burp
> > sudo chmod 777 burp
> > sudo echo "java -jar burpsuite_free_v1.6.01.jar" > burp
> > ./burp

> ## Warning
> 
> If you run Burp in Kali, it seems not to properly export the certificate and Chrome on Android refuses to accept it. It can be imported but Chrome gives an error when opening secure pages anyway.
> 
> We succeeded by running Burp directly on the host system instead (Mac OS).

## Starting Burp

When Burp starts, the first window asks you to create a project. Accept the default option of "Temporary project" and click **Next**.

In the next page, click the  **Start Burp**  button.

The main Burp window opens, as shown below.

Click the  **Proxy**  tab. Click the  **Intercept**  sub-tab.

The third button says "**Intercept is on**", as shown below.

![](https://samsclass.info/128/proj/M103-1.png)

## Configuring Burp

In Burp, click the "**Intercept is on**" button. It changes to "**Intercept is off**".

On the  **Proxy**  tab, click the  **Options**  sub-tab.

In the central box, click the Interface address to highlight it, as shown below.

![](https://samsclass.info/128/proj/p3burp3.png)

On the left side, click the  **Edit**  button.

In the "Edit proxy listener" box, click the "**Specific address**" button, and select your computer's IP address that is used to connect to the Internet, as shown below.

![](https://samsclass.info/128/proj/M141-1.png)

Click  **OK**.

Burp shows a proxy listener on your IP address and port 8080, as shown below.

Make a note of this address--you will need it below.

![](https://samsclass.info/128/proj/M141-2.png)

## Adjusting Android Networking to Use the Burp Proxy

In your Emulator, from the Android home screen, click the center button at the bottom and drag it up to show all apps.

Click  **Settings**.

In Settings, click "**Network & internet**".

Click  **Wi-Fi**.

In the  **AndroidWiFi**  line, click the gear icon, outlined in red in the image below.

![](https://samsclass.info/128/proj/M141-3.png)

In the "Network details" screen, at the top right, click the pencil icon, outlined in red in the image below.

![](https://samsclass.info/128/proj/M141-4.png)

In the "AndroidWifi" page, in the "Proxy" field, click the down-arrow and click  **Manual**.

Enter the IP address and port number of the Burp proxy listener, as shown below.

![](https://samsclass.info/128/proj/M141-5.png)

On your Android device, click  **Save**.

At the bottom center of the device, click the round  **Home**  button.

## Testing the Proxy

On your Android device, open a Web browser. In the browser, and go to

[hackazon.samsclass.info](https://samsclass.info/128/proj/hackazon.samsclass.info)

A "Hackazon" shopping site opens, as shown below.

![](https://samsclass.info/128/proj/p3burp11.png)

> ## M 141.1: Server (10 pts)
> 
> In Burp, on the  **Proxy**  tab, click the "**HTTP history**" sub-tab.
> 
> Scroll down and the GET request that loads  **hackazon.samsclass.info**  as shown below.
> 
> Click the GET request. In the lower left pane, click  **Response**.
> 
> Find the text covered by a green box in the image below. That's the flag.
> 
> ![](https://samsclass.info/128/proj/M141-12.png)

## Opening a Secure Page

In the Android device, in the Browser, and go to

**[https://samsclass.info](https://samsclass.info/)** The browser does nothing, as shown below. It's a lousy browser, which is why we installed Chrome.

![](https://samsclass.info/128/proj/p3burp13.png)

## Opening a Secure Page in Chrome

At the bottom center of the device, click the Home button. Open **Chrome**.

When you see the "Sign in to Chrome" page, click "**NO THANKS**".

In Chrome, go to

**[https://samsclass.info](https://samsclass.info/)**

A warning message appears, saying "Your connection is not private", as shown below. Notice the specific error shown:  **NET:ERR_CERT_AUTHORITY_INVALID**. This happens because Burp is performing a man-in-the-middle attack with a self-signed certificate.

![](https://samsclass.info/128/proj/p3burp23.png)

## Exporting the PortSwigger CA Certificate from Burp

This is HTTPS working as it should, warning you that you do not have a secure connection to the end site. Burp is intercepting the traffic.

We want to add PortSwigger as a trusted certificate authority to get rid of these messages.

In Burp, click the  **Proxy**  tab.

Click "**Proxy Setttings**".

Click the "**Import /export CA certificate...**" button.

In the "CA Certificate" box, in the Export setion, click the "**Certificate in DER format**" button, as shown below.

![](https://samsclass.info/128/proj/p2geny4.png)

Click  **Next**.

On the next page, click the "**Select file...**" button. Navigate to a folder you can find, such as your Desktop.

Give the file a name of  **portswigger2022.crt**.

Click  **Next**. Click  **Close**.

## Installing the PortSwigger CA Certificate into Android

Drag the **portswigger2022.crt** file from your host system and drop it on the Android device home page.

A message appears, saying "File copied".

## Importing the Portswigger Certificate

On your Android device, in Settings, click **Security**.

Click  **Advanced**. Click "**Encryption & Credentials**".

Click "**Install a certificate**", as shown below.

![](https://samsclass.info/128/proj/M141-7.png)

Click "**CA certificate**". Click "**Install anyway**".

In the next screen, at the top left, click the three-bar icon, outlined in red in the image below.

Click  **Downloads**.

![](https://samsclass.info/128/proj/M141-8.png)

In the Downloads window, click  **portswigger2022.crt**, as shown below.

A message says "CA Certificate Installed".

![](https://samsclass.info/128/proj/M141-9.png)

## Opening a Secure Page Again

In Android, launch Chrome. Go to

**[https://samsclass.info](https://samsclass.info/)** The page opens, as shown below.

![](https://samsclass.info/128/proj/M141-10.png)

## Viewing HTTPS Requests in Burp

> ## M 141.2: Server (10 pts)
> 
> In Burp, on the  **Proxy**  tab, click the "**HTTP history**" sub-tab.
> 
> Find the line that shows the  **https://samsclass.info**  page loading, as shown below. Click that line.
> 
> In the lower pane, click the  **Response**  tab.
> 
> ![](https://samsclass.info/128/proj/M141-13.png)
> 
> Find the text covered by a green box in the image above. That's the flag.

## Adjusting Android to Bypass the Proxy

While Burp is useful, most of the time you want to bypass it so you can get to Google Play.

From the Android home screen, click the circle at the bottom center.

Open  **Settings**.

In Settings, click "**Network & internet**".

Click  **Wi-Fi**.

In the  **AndroidWiFi**  line, click the gear icon.

In the "Network details" screen, at the top right, click the pencil icon.

In the "AndroidWifi" page, in the "Proxy" field, click the down-arrow and click  **None**.

Then click  **Save**.
