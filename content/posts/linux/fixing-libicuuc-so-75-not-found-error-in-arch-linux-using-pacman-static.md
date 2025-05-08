---
cover:
 image: /images/fix_pacman.jpg
 alt: Fixing "libicuuc.so.75 Not Found" Error in Arch Linux Using Pacman Static
 relative: false
title: 'Fixing "libicuuc.so.75 Not Found" Error in Arch Linux Using Pacman Static'
author: 'iniridwanul'
date: 2025-05-08T15:06:54+06:00
tags:
  - Pacman Static
  - ICU
  - libicuuc.so.75
  - Arch Linux
draft: false
categories:
  - Linux 
---

Sometimes after an update or partial upgrade in Arch Linux, you may run into the following error when trying to use pacman:
```shell
error while loading shared libraries:
libicuuc.so.75: cannot open shared object file:
No such file or directory
```
This occurs when the ICU (International Components for Unicode) library has been updated, but pacman is still linked against an older version. Since pacman can't run without that specific library, you're effectively locked out of using the package manager in the usual way.

## Use a Static Version of Pacman
A static binary doesn't rely on system libraries, so you can use it even if shared library dependencies are broken.

Fortunately, this issue can be fixed using a statically compiled version of pacman.

* Download pacman-static:
   * ```shell
      curl https://pkgbuild.com/~morganamilo/pacman-static/x86_64/bin/pacman-static --output pacman-static
      ```
* Make it executable:
   * ```shell
      chmod +x pacman-static
      ```

* Update ICU and fix the broken dependency:

Run the following command to forcefully upgrade ICU and overwrite any conflicting files
   * ```shell
      ./pacman-static -Syu --overwrite "*" icu
      ```
This command performs a system upgrade `-Syu` and overwrites any conflicting files to ensure the ICU package installs correctly.

## Optional: Reinstall pacman (if needed)
If pacman itself is broken or not functioning after the ICU fix, you can reinstall it with:
```shell
./pacman-static -S --overwrite "*" pacman
```

## Reboot
After completing the upgrade, reboot your system:
```shell
reboot
```
pacman should now work normally, and the missing libicuuc.so.75 error should be resolved.

## Conclusion
When critical shared libraries like libicuuc.so.75 go missing, it can break core tools like pacman. But thanks to the availability of a statically compiled version of pacman, you can recover quickly without needing a live environment. This method is simple, fast, and effective for getting your system back in shape.