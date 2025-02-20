---
cover:
 image: /images/xfce.jpg
 alt: Installing XFCE on Arch Linux
 relative: false
title: 'Installing XFCE on Arch Linux'
author: 'iniridwanul'
date: 2024-12-13T10:31:18+06:00
tags:
  - Desktop Environment
  - XFCE
  - Arch Linux
draft: false
categories:
  - Linux
---

There are many popular desktop environments for Linux, such as XFCE, KDE Plasma, GNOME, etc. But I have been using the XFCE desktop environment since the beginning of my Linux journey. XFCE is a light and fast desktop environment known for its simplicity and functionality. It also runs smoothly on less powerful hardware, making it a great alternative to older computers or laptops.

## What is a desktop environment?
A desktop environment (DE) in Linux is a collection of software that provides a graphical user interface (GUI). This GUI lets you interact with your Linux system using a mouse and keyboard, making it more user-friendly and visually appealing.
DEs typically include a window manager, file manager, panel or taskbar, desktop, and common applications like web browsers and text editors.

## XFCE installation guide
I have already discussed the process of installing Arch Linux. Now I will install the XFCE desktop environment on Arch Linux and also install the popular display manager LightDM. Follow the below commands exactly.
* **Install XFCE**:
   * ```shell
      sudo pacman -S xfce4 xfce4-goodies
      ```
Executing the above command will install the core package of the XFCE desktop environment as well as some additional tools and utilities for XFCE, which will make the desktop environment more feature-rich.
* **Install Display Manager (Optional)**:
   * ```shell
      sudo pacman -S lightdm lightdm-gtk-greeter
      ```
* **Enable Display Manager**:
   * ```shell
      sudo systemctl enable lightdm
      ```
Executing the above command will install the `lightdm` and `lightdm-gtk-greeter`. LightDM is a display manager, which shows the user login screen after the computer boots. And `lightdm-gtk-greeter` is a graphical user interface (GUI) of lightdm, which allows users to log in with a username and password.

Reboot the system to get the system changes correctly. After the reboot is complete and everything is fine, you will get the login screen. After logging in to the user account, you will see the XFCE interface like below.

{{< figure align=center alt="XFCE" caption="XFCE" src="/images/xfce.jpg" >}}

## Conclusion
In this guide, we explored the XFCE desktop environment, a lightweight and user-friendly option for Linux users. We discussed what a desktop environment is and its role in the Linux system. We then walked through the installation process for XFCE on Arch Linux, including the optional installation of the LightDM display manager.

By following these steps, you can successfully install XFCE on your Arch Linux system, providing a smooth and efficient user experience. With its resource-friendly nature and focus on functionality, XFCE is a great choice for both new and experienced Linux users, especially those working with older hardware.