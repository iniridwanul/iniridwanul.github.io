---
cover:
 image: /images/grub_shell.jpg
 alt: Recovering Arch Linux from a Black Screen Boot Without a Live USB
 relative: false
title: 'Recovering Arch Linux from a Black Screen Boot Without a Live USB'
author: 'iniridwanul'
date: 2025-05-08T15:18:02+06:00
tags:
  - Black Screen
  - GRUB
  - Shell
  - TTY
  - Kernel
  - Arch Linux
draft: false
categories:
  - Linux
---

When using Arch Linux, sometimes the system may break in such a way that it boots into a black screen and doesn't even allow TTY (terminal) access using typical key combinations like `Ctrl + Alt + F2`. This can be a frustrating situation especially if you don't have a bootable USB to access a live environment for troubleshooting.

Fortunately, there is a way to recover from this kind of issue using the GRUB bootloader. This article will walk you through how to bypass the graphical boot and access a working terminal by modifying boot parameters directly in GRUB.

## Symptoms
System powers on, but instead of reaching the login screen, it displays a black screen that blinks or remains completely unresponsive.
- You are unable to access TTY by pressing Ctrl + Alt + F2, F3, etc.
- No bootable USB or live environment is available for rescue.

## Cause
This usually happens due to:
- Misconfiguration in the display manager (like GDM, LightDM, etc.)
- Broken graphical drivers (e.g., after a package update)
- Corrupted graphical target

When the system attempts to boot into the graphical target (graphical UI) and fails, it doesn't automatically fall back to a safe mode or CLI interface.

## Boot into Multi-User Target from GRUB
Instead of booting into the graphical interface, you can instruct your system to boot directly into the multi-user target, which gives you terminal (TTY) access.

- Reboot your system and enter the BIOS/UEFI boot menu (usually by pressing F12, ESC, or DEL, depending on your system).
- Select the disk where your Arch Linux system is installed.
- When the GRUB menu appears, highlight the default boot option (don’t press Enter yet).
- Press `e` to edit the selected boot entry.
- You will see a number of lines. Look for the line that starts with linux. It will look something like:
`linux /boot/vmlinuz-linux root=UUID=xxxxxx rw loglevel=3 quiet`
- At the end of that line, add the following:
`systemd.unit=multi-user.target`
The full line might look like:
`linux /boot/vmlinuz-linux root=UUID=xxxxxx rw loglevel=3 quiet systemd.unit=multi-user.target`
- Press `Ctrl + X` to boot with the modified settings.

## What Happens Next
Your system will boot into TTY mode (non-graphical terminal).

You will see a login prompt. Use your username and password to log in.

From here, you can troubleshoot the graphical environment or any other system issue.

## Conclusion
Even without a live USB, it's possible to recover a non-booting Arch Linux system stuck at a black screen. Using GRUB to boot into multi-user.target provides a safe and accessible environment for recovery. This technique is invaluable for system administrators and users who frequently work with minimal or broken systems.