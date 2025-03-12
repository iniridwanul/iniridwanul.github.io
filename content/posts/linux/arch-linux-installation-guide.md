---
cover:
 image: /images/arch_linux.png
 alt: Arch Linux
 relative: false
title: 'Arch Linux Installation Guide'
author: 'iniridwanul'
date: 2024-12-07T05:04:49+06:00
tags:
  - Linux
  - Arch Linux
  - Manually Installation
draft: false
categories:
  - Linux
---

My first Linux journey started with Kali Linux. Being very interested in cybersecurity, I came to know about Kali Linux and started using it. I used Kali Linux for more than a year. Then I decided to change the distro. I used Ubuntu for eight months, Manjaro for two years, EndeavourOS for three months, and Fedora for one year. But for various reasons, these distros did not seem right for my needs. Then I started using Linux Mint. Such a beautiful, lightweight, and amazing distro captured my mind. I have been using Linux Mint for four years with the Xfce Desktop Environment. If I ever have time, I will try to write about Linux Mint.

{{< figure align=center alt="Arch Linux" caption="Arch Linux" src="/images/arch_linux.png" >}}

After four years of using Linux Mint, I felt that I needed a simple, flexible, and clean OS. In which I can organize everything I need as per my mind. So I chose Arch Linux. Arch Linux is the most amazing distro I have seen. I have been using Arch Linux for two years. There is an `archinstall` script available to install Arch Linux, but if you install it manually, you will learn a lot about Arch and Linux. In this article, I am going to guide you through the easiest way to install Arch Linux. Before going straight to the installation process, it is important for us to know some things, so let's get started.

## What is Arch Linux?
Arch Linux is a popular Linux distribution known for its simplicity, flexibility, and focus on user freedom. It's designed to provide the latest stable software versions through a rolling-release model. This means that instead of releasing major updates periodically, Arch Linux continuously updates its packages, ensuring users always have access to the newest features and security patches.

## Why Use Arch Linux?
Arch Linux offers a unique experience for tech-savvy users who value control and customization. Here are some key reasons why people choose Arch Linux:
* **Customization**: Arch Linux provides a minimal base system, allowing users to tailor their system to their exact needs. You can choose your preferred desktop environment, window manager, and software packages, creating a truly personalized experience.
 * **Latest Software**: The rolling-release model ensures that you're always running the latest versions of software, often before other distributions. This means access to new features, performance improvements, and security fixes.
 * **Learning Opportunity**: Installing and configuring Arch Linux is a great way to learn about Linux system administration. It deepens your understanding of how Linux works and how to troubleshoot issues.
 * **Community**: The Arch Linux community is highly active and helpful. You can find assistance with any questions or problems on the official forums and other online resources.
 * **Performance**: Arch Linux is known for its performance and efficiency. The minimal base system and the ability to fine-tune your system can lead to significant performance gains.

## Who Uses Arch Linux?
Arch Linux is primarily used by experienced Linux users who are comfortable with the command line and system administration tasks. It's particularly popular among developers, system administrators, and enthusiasts who appreciate the flexibility and control it offers.

While Arch Linux might not be the best choice for everyone, it's a powerful tool for those who want to take full control of their computing experience. If you're willing to invest time and effort into learning the system, Arch Linux can provide a rewarding and customized Linux experience.

## Preparing to Install Arch Linux
Installing Arch Linux from scratch gives you complete control over what is installed, allowing you to tailor the system to your needs. The installation process also helps you understand how Linux works, from partitioning your disk to configuring the bootloader (GRUB).

You will end up with a minimal installation that ensures no unnecessary software is running, which boosts system performance. Follow the steps outlined below to install Arch Linux.
* **Download the Arch Linux ISO**:
   * First you need to download the Arch Linux ISO. It will be possible to download the ISO file very easily from the download page of the official website of Arch Linux.

* **Create a Live USB**:
   * This software, named balenaEtcher, is available for Linux and Windows systems, making it very easy to create Arch Linux Live USB. But keep in mind that all the data on your USB will be deleted, so you can take a backup of the necessary data.

* **Live Boot Arch Linux**:
   * Insert the installation media into your machine.
   * Now enter the Boot Menu. For that, press ESC, F2, F10, or F12 after power on. It depends on your system which key will help you enter the boot menu.
   * Now select the USB device that has the Arch Linux ISO image written on it and enter the Arch Linux Live ISO.
   * Since I am going to tell how to install Arch Linux through UEFI System, definitely boot Arch Linux in UEFI mode.

## Determining the Boot Mode
Since in this article I am only going to discuss the process of installing Arch Linux on a UEFI system, it is a very important part. First of all, check if we are able to boot Arch Linux Live in UEFI mode. For that, execute the following command: If this is valid and it spits out a number of files on the screen, then you are in UEFI mode.
```shell
ls /sys/firmware/efi/efivars
```

## Internet connection
If you are on a device that has wifi connectivity, then connecting to the internet will be very easy for you. `iwctl` is an amazing tool that can easily connect to a wifi network. Follow the below commands to connect to the wifi network through this tool.
* To get an interactive prompt do:
   * ```shell
      iwctl
      ```
* First, if you do not know your wireless device name, list all Wi-Fi devices:
   * ```shell
      device list
      ```
* Then, to initiate a scan for networks (note that this command will not output anything):
   * ```shell
      station wlan0 scan
      ```
* You can then list all available networks:
   * ```shell
      station wlan0 get-networks
      ```
* Finally, to connect to a network:
   * ```shell
      station wlan0 connect iniridwanul
      ```

Sometimes wifi networks don't want to be shown even after scanning networks by `iwctl`, if you are facing such a problem, follow the below commands.
```shell
device wlan0 set-property Powered off
```
```shell
device wlan0 set-property Powered on
```
Hope you have successfully connected to internet in Live Boot mode of Arch Linux. You can check whether your internet connection is working successfully through ping command.
```shell
ping -c 3 iniridwanul.github.io
```

## Partitioning the Disks
Partitioning in Linux involves dividing a physical disk into logical sections called partitions. This allows for better organization and management of data. Each partition can have its own file system and be used for specific purposes, such as storing the operating system, user data, or swap space. Common partitioning tools include fdisk and gparted, which can be used to create, delete, resize, and format partitions. Proper partitioning is crucial for efficient disk utilization and system performance.

I recommend using `cfdisk` to create partitions very easily. Enter the `cfdisk` command and create partitions according to the partition table below on your preferred device storage with gpt label type.
| Storage | Size | Type |
|---|---|---|
| /dev/sda1 | 512M | EFI System
| /dev/sda2 | 1G | Linux Swap
| /dev/sda3 | All the rest | Linux filesystem

Then select write option to write disk and confirm by writing `yes` then quit.
> Change the serial numbers according to your storage device.

## Create filesystem
The next step is to format the new partitions to install Arch Linux. To do this, create a file system for each of the partitions. Follow the steps below:
* EFI partition:
   * ```shell
      mkfs.fat -F32 /dev/sda1
      ```
* Root partition:
   * ```shell
      mkfs.ext4 /dev/sda3
      ```
## Swap partition
A swap partition is a dedicated portion of your hard drive that acts as an extension to your system's RAM (Random Access Memory). It comes into play when your RAM is fully utilized, allowing the operating system to temporarily store less frequently used data on the swap partition. This process is called swapping or paging. By doing so, swap partitions effectively increase your system's virtual memory, enabling you to run more applications simultaneously. Execute the following command to create and turn on the swap partition.
```shell
mkswap /dev/sda2
```
```shell
swapon /dev/sda2
```
Congrats! The most difficult part is over! Time to move onto the base system installation.

## Installing the Base System
We have come a long way on the path of Arch Linux installation. Since the file system has been set up and properly formatted, now we only need to mount the root partition and instruct the terminal to install the base system there.
* Mount the root partition:
   * ```shell
      mount /dev/sda3 /mnt
      ```
* Base system and necessary software:
   * ```shell
      pacstrap /mnt base linux linux-firmware sudo nano
      ```
Now wait until the installation is complete; you can sit with tea or coffee during this time if you want.

## System Configuration
The fstab file, for file system table file, contains information on how the file system should be mounted. Remember all that mounting and turning swap partitions on we did earlier? This is our way of keeping that on record so the system knows how we want our partitions configured every time it boots up.
* Generate fstab:
   * ```shell
      genfstab -U /mnt >> /mnt/etc/fstab
      ```

## Changing Root
Now we want to change the root we are operating in from that of the live environment to the one on disk. This is done via the following command:
```shell
arch-chroot /mnt
```

## Localization
You need to determine which languages and regions your Linux system supports. The `/etc/locale.gen` file lists the different locales. A locale is a set of languages and regions that specify a specific language, date and time format, currency, etc. Open this file with the `nano /etc/locale.gen` command and uncomment your preferred locale. I am uncommenting `en_US.UTF-8 UTF-8`.

Follow the commands below to generate the locale and set the preferred language.
* To Generate Locale:
   * ```shell
      locale-gen
      ```
* Set the language:
   * ```shell
      echo "LANG=en_US.UTF-8" > /etc/locale.conf
      ```

## Time Zone Setup
All of the timezone information on Linux is stored in `/usr/share/zoneinfo` with the subdirectories therein containing specific regions and locations within those regions. Select a file path to a region that falls within your timezone and create a symbolic link between that path and `/etc/localtime`.
* Set the Time Zone:
   * ```shell
      ln -sf /usr/share/zoneinfo/Asia/Dhaka /etc/localtime
      ```
* Update time via the Internet:
   * ```shell
      timedatectl set-ntp true
      ```
* Update hardware clock:
   * ```shell
      hwclock --systohc
      ```

## Set the Hostname File
Now we need to set the hostname. This is the name that will identify your computer when it is connected to a network.
* Add hostname:
   * ```shell
      echo archlinux > /etc/hostname
      ```
* Open hosts file:
   * ```shell
      nano /etc/hosts
      ```
* Configure the hosts file:
   * ```shell
      127.0.0.1	localhost
      ::1		localhost
      127.0.1.1	archlinux.localdomain	archlinux
      ```

## Set your Root Password
This step is fairly straight forward and consists of a single command, passwd. Run that command and there will be a prompt for you to enter your password and another one for you to verify it. Note that none of the text you type will show up in an effort to obfuscate your security credential but rest assured your keystrokes are being registered.
* Set Password:
   * ```shell
      passwd
      ```

## Creating a User
I recommend not using the root account all the time. In Linux, the root account is an account with the highest privileges. If you log in as root, you can modify any file on the system, install any program, and change system settings. However, with this privilege comes a big risk.

If you accidentally modify any important system file or install any virus or malware, the entire system may crash. Therefore, to maintain the security and stability of the system, you should work as a normal user. Therefore, to keep our system safe, we will create a user.
* Create user:
   * ```shell
      useradd -m -G wheel iniridwanul
      ```
* Set the user password:
   * ```shell
      passwd iniridwanul
      ```

## Adding Superuser Privileges
We will need to make a small modification to the `/etc/sudoers` file. By default, the line allowing members of the wheel group to act as sudoers is commented out. Uncomment it and exit the file to gain superuser access.
* Open sudoers:
   * ```shell
      EDITOR=nano visudo
      ```

## Install GRUB Bootloader on a UEFI System
A UEFI system is a modern firmware standard that replaces the traditional BIOS. It provides enhanced boot, security, and system management capabilities.
* Add the GRUB bootloader packages with the pacman manager:
   * ```shell
      pacman -S grub efibootmgr
      ```
* Create a directory for the EFI partition:
   * ```shell
      mkdir /boot/efi
      ```
* Mount the EFI partition to the directory you created:
   * ```shell
      mount /dev/sda1 /boot/efi
      ```
* Install GRUB with:
   * ```shell
      grub-install --target=x86_64-efi --bootloader-id=GRUB --efi-directory=/boot/efi
      ```
* Finally, create a GRUB configuration file:
   * ```shell
      grub-mkconfig -o /boot/grub/grub.cfg
      ```

## Setup NetworkManager
NetworkManager is a system network service that manages your network devices and connections and attempts to keep network connectivity active when available.
* Install NetworkManager:
   * ```shell
      pacman -S networkmanager network-manager-applet
      ```
* Enable NetworkManager:
   * ```shell
      systemctl enable NetworkManager
      ```

## Exit Arch-Chroot Environment and Reboot
If you have followed all the steps correctly, then congratulations. You have successfully installed Arch Linux. Now exit the Arch-Chroot Environment and reboot your system.
* Exit Arch-Chroot Environment:
   * ```shell
      exit
      ```
* Unmount the root partition:
   * ```shell
      umount -R /mnt
      ```
* Then, remove the USB and reboot the system:
   * ```shell
      reboot
      ```

## Conclusion
By following this guide, you have successfully installed and configured Arch Linux on your system. A highly customizable and minimalist Linux distribution, Arch Linux provides users with granular control over their operating environment. It is well-suited for experienced users who desire a tailored computing experience.