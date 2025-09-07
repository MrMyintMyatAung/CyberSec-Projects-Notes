## What You Need for This Project

-   A computer with an Internet connection.

## Purpose

This gives you a Debian Linux system to use on top of a Mac or Windows box.

# Task 1: Install a Hypervisor

Install VMware, VirtualBox, or some other virtualization software on your machine.

If you are new to virtualization, I recommend these products, which are both free:

-   For Windows:  [**VMware Workstation Player**](https://www.vmware.com/products/workstation-player.html)
-   For Mac:  [**VMware Fusion**](https://www.vmware.com/products/fusion.html)

# Task 2: Download and Import a Linux Virtual Machine

> ## Mac M1, M2, or M3 Users
> 
> You need to download an ARM64 version of Debian instead of the prebuilt machines referenced below.
> 
> You can get the ISO here:
> 
> > [https://cdimage.debian.org/debian-cd/current/arm64/iso-cd/](https://cdimage.debian.org/debian-cd/current/arm64/iso-cd/)

Download the VMWare image for the latest version of Debian 12 from [**https://www.linuxvmimages.com/images/debian-12/**](https://www.linuxvmimages.com/images/debian-12/).

Unzip the file. A folder is created with several files, including an  **.ovf**  file.

Open VMware. From the menu bar, click  **File**,  **Import**. Import the  **.ovf**  file.

Launch your Linux machine.

Log in with the username  **debian**  and a password of  **debian**

## Installing Android Debug Bridge

On your Debian machine, at the top left of the desktop, click **Activities** and search for Terminal.

In the Terminal, execute these commands:

> sudo apt update
> sudo apt install android-tools-adb -y

> ## M 111.1: adb Version (15 pts)
> 
> In your Debian machine, open a Terminal window and execute this command:
> 
> > adb version
> 
> The flag is covered by a green rectangle in the image below.
> 
> ![](https://samsclass.info/127/proj/M111-1.png)



