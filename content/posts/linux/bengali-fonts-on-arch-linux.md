---
cover:
 image: /images/bengali_font.png
 alt: Bengali Fonts on Arch Linux
 relative: false
title: 'Bengali Fonts on Arch Linux'
author: 'iniridwanul'
date: 2025-01-15T02:00:34+06:00
tags:
  - Bengali font
  - Font installation
  - Font configuration
  - Qayyum Book
draft: false
categories:
  - Linux
---

Arch Linux, a widely popular Linux distribution, is known for its simplicity, flexibility, and user freedom. However, Bengali users frequently face issues with broken Bengali characters. As a Bengali user myself, I can personally vouch for the prevalence of this problem. It's essential to understand the causes and solutions to this issue.

## Why Bengali characters break?
The primary cause of this issue often lies in font incompatibility. A font is essentially a set of characters designed in a specific style. Bengali writing requires specialized fonts that can accurately render Bengali characters. If the font being used doesn't support Bengali characters correctly, it can lead to broken or distorted text.

## Font installation
To install a Bengali font, begin by downloading your desired font file. For instance, I recommend the `Qayyum Book` font. Once downloaded, access your Home directory and locate the `.local/share` directory. Create a subdirectory named `fonts` if it's absent. Subsequently, place your downloaded font file within this newly created or existing `fonts` directory.

## Font cache
If you're a user of Linux or other Unix-like operating systems, you're likely familiar with the concept of a cache. A cache is a temporary storage area used to store the results of file system operations, network connections, or other system calls. This significantly speeds up system response times.

Therefore, when a new font is installed, removed, or font settings are changed in a system, it's crucial to update the font cache. Since we've added a new font, we'll use the command `fc-cache -r` to refresh the font cache. The font cache is a database that stores information about all the fonts installed on the system.

## Font configuration
You can configure fonts by modifying the settings in the `.Xresources` file. Alternatively, you can easily configure fonts system-wide using `fontconfig`. In this instance, I'll be resolving the issue using fontconfig.

To properly configure fonts, you need to navigate to the `.config` directory within your home directory. Look for a directory named `fontconfig`. If it doesn't exist, create one with that name. Inside the `fontconfig` directory, create a file named `fonts.conf` and configure it according to your preferences. Below is a sample `fonts.conf` file that you can modify to suit your needs.

```xml
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>

<!-- Define an alias for serif fonts -->
<alias>
  <family>serif</family>
  <!-- Set "Qayyum Book" as the preferred serif font -->
  <prefer>
    <family>Qayyum Book</family>
  </prefer>
</alias>

<!-- Define an alias for sans-serif fonts -->
<alias>
  <family>sans-serif</family>
  <!-- Set "Qayyum Book" as the preferred sans-serif font -->
  <prefer>
    <family>Qayyum Book</family>
  </prefer>
</alias>

<!-- Define an alias for monospace fonts -->
<alias>
  <family>monospace</family>
  <!-- Set "JetBrainsMono Nerd Font" as the preferred monospace font -->
  <prefer>
    <family>JetBrainsMono Nerd Font</family>
  </prefer>
</alias>

</fontconfig>
```
> To ensure that the font changes are applied correctly, it is recommended to restart or log out of the system.

{{< figure align=center alt="Bengali Fonts on Arch Linux" caption="Bengali Fonts on Arch Linux" src="/images/bengali_font.png" >}}

## Conclusion
By following these steps, Bengali users on Arch Linux can effectively resolve issues with broken Bengali characters. Installing a suitable Bengali font like Qayyum Book, updating the font cache, and configuring fonts through `fontconfig` will ensure proper rendering of Bengali text across the system. This guide provides a practical solution for users to enjoy a seamless and hassle-free Bengali language experience on their Arch Linux systems.