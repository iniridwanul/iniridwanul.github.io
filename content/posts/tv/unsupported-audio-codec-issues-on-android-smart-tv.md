---
cover:
 image: /images/smart_tv.jpg
 alt: Unsupported Audio Codec Issues on Android Smart TV
 relative: false
title: 'Unsupported Audio Codec Issues on Android Smart TV'
author: 'iniridwanul'
date: 2025-05-06T11:10:41+06:00
tags:
  - Audio Codec
  - Smart TV
  - Android TV
draft: false
categories:
  - Smart TV
---

Many users face a common problem while playing `.mkv` or other video files on their smart TV, the video plays but there is no sound. Interestingly, the same file works perfectly on a laptop or smartphone. This usually points to an unsupported audio codec on the smart TV.

## Understanding the Problem
Smart TVs, especially budget models, support a limited range of audio and video codecs. While formats like `.mkv` and `.mp4` are widely supported, the underlying audio codec (e.g., AC3, DTS) may not be. Most Android TVs support `AAC` and `MP3` audio codecs natively, but not AC3/DTS unless licensed.

## Convert the Audio Codec
Instead of converting the entire video (which is time-consuming), you can simply re-encode the audio stream using a tool like `FFmpeg`, leaving the video stream untouched.

## Installing FFmpeg
* You will install FFmpeg according to your system. I use Arch Linux. If you are also using Arch Linux like me, then use the following command to install FFmpeg on your system:
   * ```shell
      sudo pacman -S ffmpeg
      ```
## Solution
* If you're on Linux (or any system with FFmpeg installed), run:
   * ```shell
      ffmpeg -i input.mkv -c:v copy -c:a aac output.mkv
      ```
`-c:v copy`: keeps the original video stream untouched.

`-c:a aac`: converts the audio stream to AAC, which is widely supported by smart TVs.

This process is fast because only the audio is being re-encoded, and the video is copied directly.

## Check Your Files Codecs
* To inspect the original file and confirm the audio codec:
   * ```shell
      ffprobe input.mkv
      ```
* Look for lines like:
   * `Stream #0:1: Audio: ac3 (AC-3)`

If you see AC3 or DTS, converting to AAC is a smart move.

## Final Thoughts
If your smart TV doesn't play the audio in a video file, don't assume the file is corrupted. A quick codec conversion using FFmpeg can save hours of frustration. It's a simple fix that works reliably especially for budget Android TVs that don't license premium codecs by default.