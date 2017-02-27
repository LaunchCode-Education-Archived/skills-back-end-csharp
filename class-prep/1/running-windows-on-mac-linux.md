---
title: Running Windows on Mac or Linux
currentMenu: classes
---

For this unit we'll need to run Visual Studio for Windows. If you use macOS or a Linux-based operating system, you can install an application called a **hypervisor** that allows you to run **virtual machines** that contain other operating systems. This is what we'll do to get Windows running on your machine.

<aside class="aside-note" markdown="1"> You may noticed on the Microsoft site that there is a preview version Microsoft Visual Studio for Mac. The .NET development environment on macOS isn't mature enough yet to warrant us to use it in this class.
</aside>

## Install VirtualBox

The hypervisor we'll use is VirtualBox. [Visit their download page](https://www.virtualbox.org/wiki/Downloads) and download the installer for your particular host system (Mac or Linux).

## Install A Windows Virtual Machine

Download a free Windows 10 Development Virtual Machine (VM) at the [Windows Dev Center](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines). Choose the VirtualBox edition of Windows 10 Enterprise.

Unzip the downloaded file and install the VM by double-clicking on the resulting .ova or .ovf file. Follow the prompts within the VM to complete the Windows setup process.

### Guest Additions and Other Tweaks

Let's do a few things to make our experience working in this VM a little better.

Install VirtualBox Guest Additions by selecting the Guest Additions icon from the system tray in the lower right of your Windows VM. This additional package will enable a better experience and closer integration between the host and guest operating systems. You'll then need to restart the VM for the changes to take effect.

> *NOTE:* Whenever you want to "shut down" the virtual operating system, you have three choices:
    - *Save the machine state* - The equivalent to putting the VM to sleep, or shutting your laptop. You'll want to do this most often. We'll call this *pausing* your VM.
    - *Send the shutdown signal* - The equivalent to shutting down the operating system via the Start Menu's *Power Off* item. You'll want to do this when you want to reboot your VM, such as after installing the Guest Additions.
    - *Power off the machine* - The equivalent of turning off the VM by holding down a physical power button on a computer until it "force quits". Don't do this unless you absolutely have to.

It's very handy to be able to copy/paste between your host operating system (Mac or Linux) and the guest operating system (Windows). To enable this, pause your VM, and from the main VirtualBox window, select the Settings icon to access the VM's settings. From the *General* section, choose the *Advanced* tab, and choose *Bidirectional* from the *Shared Clipboard* menu. This will allow you to copy/paste back and forth.

> *NOTE:* On a Mac, the copy/paste shortcuts (among others) use the *command* key, while in Windows they use the *control* key. Keep this in mind. You'll need to use *ctrl+c* and *ctrl+v* from your Mac keyboard to copy/paste within the Windows VM.

### Visual Studio Setup

Add the GitHub Visual Studio extension by downloading and installing from [visualstudio.github.com](https://visualstudio.github.com/) (do this inside your VM). After installation, follow the prompt to sign in to your GitHub account.

Open Visual Studio. On the view that opens, "Sign in to Visual Studio", go ahead and create an account (or sign in if you already have one). It's free, and it will unlock the full features of the application.

### Install Dropbox

From within the Windows VM, visit [dropbox.com](https://www.dropbox.com/) and install the Dropbox App, creating a free account if you don't already have one. Once the app is installed, create a new folder named `lc101` within the Dropbox folder.

**Pre-existing Dropbox account**: You likely don't want everything you've stored in Dropbox to download to your VM. To prevent this, open up Dropbox preferences and choose the Account tab. Then click on *Selective Sync*. From this window, you can make sure that only the `lc101` folder (and any others you might want) is selected to sync to your VM.

Why are we doing this? As you may have noticed, the Windows VM that you installed will eventually expire. Microsoft doesn't give out free copies of Windows for indefinite use, and this is the mechanism they put in place to prevent indefinite free usage. Once the VM expires, you will be forced to get a new Windows development VM in order to continue developing on Windows. By storing your project files within Dropbox, you'll have a backup of your files, and it will be easy to sync all of your projects down to your new VM and continue working, with the minimal amount of hassle.

**If you don't store your project files in Dropbox, they will be inaccesible once the VM expires.**

To setup a new image after the current one expires, revisit this page and follow all steps, skipping the VirtualBox install step.

### Install Other Apps

At this point, you'll probably want to install a few more apps that you use frequently, such as [Firefox](https://www.mozilla.org/en-US/firefox/new/) and [Atom](https://atom.io/).
