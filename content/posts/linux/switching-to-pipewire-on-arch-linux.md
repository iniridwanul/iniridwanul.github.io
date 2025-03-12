---
cover:
 image: /images/pw-top.png
 alt: pw-top
 relative: false
title: 'Switching to PipeWire on Arch Linux'
author: 'iniridwanul'
date: 2025-01-20T18:45:10+06:00
tags:
  - PipeWire
  - PulseAudio
  - Audio Server
draft: false
categories:
  - Linux
---

In 2017, PipeWire emerged as a promising alternative to the long-standing PulseAudio. While it initially faced stability issues, it has since matured into a reliable and feature-rich audio server for Linux. Many users are now considering the switch.

## What is PipeWire?
PipeWire is a server for handling audio and video streams on Linux systems. It aims to improve multimedia handling by providing a flexible and efficient framework for routing and processing audio and video data. PipeWire can be used for various purposes, such as playing audio from applications, capturing audio from microphones, and mixing audio streams together. It is designed to be compatible with existing audio and video applications and libraries, making it easy to integrate into existing systems.

## How to install PipeWire?
All PipeWire installations begin with the core service. This may already be included in your distribution, but if not, you can install it using the following commands.
* **Installing the service**:
   * ```shell
      sudo pacman -S pipewire pipewire-alsa
      ```
PipeWire doesn't handle audio connections on its own; you'll need a session manager like WirePlumber. WirePlumber provides more customization options and extra plugins for a better audio experience.
* **Installing the session manager**:
   * ```shell
      sudo pacman -S wireplumber
      ```
To ensure optimal audio performance, given that many of your system's applications rely on PulseAudio, you'll need to install the PipeWire daemon. This daemon will intercept and handle PulseAudio communications.
* **Installing the PulseAudio daemon**:
   * ```shell
      sudo pacman -S pipewire-pulse
      ```
Installation of PipeWire is finished. Let's start the service.
* **Getting services ready**:
   * ```shell
      systemctl --user --now enable pipewire pipewire-pulse wireplumber
      ```
## Conclusion
PipeWire has matured significantly since its initial release, evolving into a robust and capable audio server for Linux systems. By offering a flexible and efficient framework for handling audio and video streams, PipeWire addresses many of the limitations of its predecessor, PulseAudio.

While the initial installation process might seem slightly more involved than simply installing PulseAudio, the benefits of using PipeWire, such as improved performance, greater flexibility, and better integration with modern multimedia technologies, make it a compelling option for many Linux users.

By following the steps outlined in this guide, users can successfully install and configure PipeWire, including the essential WirePlumber session manager and the PipeWire PulseAudio daemon, enabling a smooth transition from PulseAudio to this modern audio server.