---
cover:
 image: /images/lapce.png
 alt: Lapce
 relative: false
title: 'Lapce Setup Guide for Arch Linux'
author: 'iniridwanul'
date: 2025-03-01T15:24:13+06:00
tags:
  - Lapce
  - Customizable
  - Lightweight
  - Syntax Highlighting
  - Vim Keybindings
  - VS Code
  - Rust
  - Open Source
  - IDE
draft: false
categories:
  - Linux
---

Lapce is a modern, lightweight, and high-performance code editor designed for developers who prioritize speed and efficiency. Unlike traditional code editors that rely on Electron or other heavy frameworks, Lapce is written in Rust and uses GPU acceleration to deliver a snappy experience. With its native performance, built-in LSP support, and powerful plugin system, Lapce is gaining popularity as an alternative to VS Code and other editors.

{{< figure align=center alt="Lapce" caption="Lapce Editor: The Fast and Lightweight Code Editor" src="/images/lapce.png" >}}

## Why is Lapce a Good Choice?
Lapce stands out from other editors due to its unique combination of performance, lightweight design, and extensibility. Here are some key reasons why developers are choosing Lapce:
* **Built with Rust for Performance and Safety**: Lapce is written in Rust, a systems programming language known for its speed and memory safety. This makes the editor extremely fast and less prone to crashes or memory leaks compared to Electron-based editors like VS Code.

* **GPU-Accelerated Rendering**: Lapce utilizes OpenGL for GPU-accelerated rendering, making UI interactions and scrolling feel fluid and responsive.

* **Native LSP Support for Intelligent Code Editing**: Lapce has built-in support for the Language Server Protocol (LSP), allowing it to provide features like autocompletion, linting, and syntax highlighting across multiple programming languages.

* **Minimalist and Lightweight**: Unlike VS Code, which relies on Electron and can be resource-hungry, Lapce is lightweight and efficient, consuming significantly less RAM and CPU.

* **Vim Mode and Customization**: Lapce includes Vim keybindings for those who prefer a more efficient, keyboard-driven workflow.

* **Plugin System for Extensibility**: Lapce supports plugins that extend its functionality, allowing users to customize their workflow.

* **Remote Development Support**: With remote workspace capabilities, developers can edit code on remote servers or cloud environments efficiently.

## How to Install Lapce?
Lapce is available for various platforms, including Linux, macOS, and Windows. I have an old laptop with Arch Linux installed as the operating system and an older GPU, **AMD Radeon R2 (Mullins)**. I will install Lapce on this system to test it.

Lapce is a GPU-accelerated code editor that uses the Vulkan API to enhance rendering performance. As a result, it runs much faster than VS Code, especially in compositing, scrolling, and text rendering.

Since the **AMD Radeon R2 (Mullins)** is an older GPU but supports Vulkan, Lapce should perform well. However, if the Vulkan driver is not installed, rendering issues may occur. Therefore, it is essential to check whether the Vulkan driver is installed and install it if necessary.

* Check if Vulkan support is available:
   * ```shell
      vulkaninfo | grep "GPU"
      ```
* If `vulkaninfo` is not present, install `vulkan-tools`:
   * ```shell
      sudo pacman -S vulkan-tools
      ```
* Install AMD Vulkan driver (if not present):
   * ```shell
      sudo pacman -S vulkan-radeon lib32-vulkan-radeon
      ```
* Driver change (if necessary):
   * ```shell
      sudo nano /etc/default/grub
      ```
In the grub file, the `GRUB_CMDLINE_LINUX_DEFAULT` line needs to be modified as follows.
```
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet amdgpu.si_support=1 radeon.si_support=0 amdgpu.cik_support=1 radeon.cik_support=0"
```
* Then update GRUB:
   * ```shell
      sudo grub-mkconfig -o /boot/grub/grub.cfg
      ```
* Update initramfs:
   * ```shell
      sudo mkinitcpio -P
      ```
To get the changes properly, reboot the system using the `reboot` command.
* Install Lapce:
   * ```shell
      sudo pacman -S lapce
      ```
## Conclusion
Lapce is a promising new code editor that combines the speed and efficiency of Rust with a lightweight, GPU-accelerated UI. It provides native LSP support, Vim keybindings, and a plugin system, making it a great choice for developers looking for a fast, efficient, and customizable editor.

If you're looking for an alternative to Electron-based editors like VS Code while keeping powerful development features, Lapce is definitely worth trying.