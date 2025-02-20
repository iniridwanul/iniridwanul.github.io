---
cover:
 image: /images/git_lfs.jpg
 alt: Git Large File Storage
 relative: false
title: 'Git Large File Storage'
author: 'iniridwanul'
date: 2024-11-27T18:30:46+06:00
tags:
  - Git
  - Github
  - LFS
  - Large File Storage
draft: false
categories:
  - GitHub
---

I was trying to create an audio library of the Holy Quran on my blog. I wanted to put the surahs in my GitHub repository and create the facility to stream audio from there. But Git is not designed to handle large files efficiently. It struggles with large files due to its delta-based compression, which works poorly on binary files like images, videos, and audio. This leads to bloated repositories, slow clone times, and inefficient branching and merging.

## Why use Git LFS?
Git Large File Storage (LFS) is a Git extension designed to efficiently manage large files within Git repositories. Unlike traditional Git, which is optimized for text-based files, LFS addresses the limitations of storing large binary files (such as images, videos, and audio) directly in the repository.

LFS operates by replacing large files with text pointers in the Git repository. These pointers reference the actual file content, which is stored in a separate remote storage system. This approach significantly reduces the repository's size, improves performance, and streamlines various Git operations like cloning, fetching, and pushing.

By leveraging LFS, developers can maintain a clean and efficient Git workflow, even when working with large files. This allows for smoother collaboration, faster operations, and a more streamlined development process.

## How to use Git LFS?
Git LFS is a powerful tool that seamlessly integrates with Git to efficiently manage large files. Here is a very easy step-by-step guide on how to use Git LFS.

* **Install Git LFS**: Follow the installation instructions according to your operating system from the Git LFS official website. As I am using Arch Linux, I am installing Git LFS by `sudo pacman -S git-lfs` command.
* **Initialization**: The `git lfs install` command initializes Git LFS and configures it to work with your repositories.
* **Track Large Files**: If you want, you can upload only files of specific extensions to git lfs by the `git lfs track "*.extension"` command.

## Conclusion
Git Large File Storage (LFS) is a powerful tool for managing large files within Git repositories. By storing large files outside of the main repository and replacing them with pointers, LFS significantly reduces repository size and improves performance. This allows for efficient cloning, fetching, and branching operations, even with large assets. With Git LFS, developers can seamlessly manage large files alongside code, making it an invaluable asset for projects involving large media, data files, or other binary assets.