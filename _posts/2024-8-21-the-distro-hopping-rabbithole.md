---
title: "the distro-hopping rabbithole"
categories: [programming, development]
date: 2024-08-21 20:48:09 +0530
toc: true
description: >-
  My history with linux and distro-hopping.
tags: [programming, development, linux, engineering, software]
---

## the beginning

I got my first personal laptop back in 2021, an ASUS TUF F15 with an Nvidia GTX 1650 mobile GPU. It came with Windows 11 pre-installed, which was great for gaming. I was content, using it occasionally for programming, mainly for college assignments. However, I soon realized how challenging the development experience was on Windows. I struggled with getting tools like GCC, Anaconda, and others to work smoothly on my machine.

## wsl2

After some research, I discovered WSL2, which was relatively new at the time. I installed Ubuntu 20.04 LTS and was amazed by how much better the development experience was with WSL2 and VSCode. However, it was frustratingly slow. Running GUI apps was a struggle, and overall, I was a bit disappointed.

## Kali

All my college peers who loved to show off were using Kali Linux, so I decided to give it a try. Kali is undeniably cool, and I experimented with a persistent USB setup. However, I quickly realized it wasn’t ideal as a daily driver. It had too many tools I didn’t use or need.

## Manjaro

A quick Google search for "Best Linux distro" led me to Arch Linux. However, at the time, Arch had a reputation for being one of the hardest distros to install. Intimidated by the traditional installation process, and needing to keep Windows for gaming and as a fallback, I decided to try Manjaro Linux instead. It was beginner-friendly, and I liked the Pamac manager, but I still felt like I was missing something.

## arch: ALG

Using Manjaro made me realize I should try raw Arch Linux. I found Arch Linux GUI (ALG), which came with the Calamares installer. I installed the Plasma flavor and was extremely happy with the experience. The learning curve was steep, but I was eager to learn. Pacman, yay—everything made sense.

![img](https://i.imgur.com/KXx7zK3.png)
*My first Arch setup*

I explored different desktop environments, GTK themes, and window managers and was really content with my setup. I used this setup as my daily driver for over a year.

## Fedora

While using Arch Linux, I started having issues with my Wi-Fi card. I tried various solutions, but nothing worked. Frustrated, I decided to try Fedora (also because Linus Torvalds uses it, lol). I didn't like Fedora at all. It felt basic, and the Wi-Fi issue persisted. However, I did manage to rice my GNOME setup and used it for a week or two.

![img](https://i.imgur.com/BGjgSna.png)
*My GNOME rice*

[View on Reddit](https://www.reddit.com/r/unixporn/comments/z92mm8/gnome_gruvbox_minimal_fedora_37/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

## arch: traditional

It was time to return to Arch Linux, but this time, I did a CLI installation—the way it's supposed to be done. I chose GNOME again, thanks to my experience with Fedora. I riced it and used it for another year. During this time, I even created my own GTK theme, [Cosmos](https://github.com/rumbleftw/cosmos), inspired by the [Ayu color palette](https://github.com/ayu-theme/ayu-colors). Getting touchpad gestures and Nvidia drivers to work was a pain, and Wayland was challenging, especially with basic features like screen sharing.

![img](https://i.imgur.com/PRDgwnU.jpeg)

I dove deep into the ricing rabbit hole and fell in love with [r/unixporn](https://www.reddit.com/r/unixporn/). I even tried out tiling window managers but found them too complicated at the time. This setup was my daily driver for two years, and I used this setup for my full-time job as well.

Some of my favourite rices:
- [reddit](https://www.reddit.com/r/unixporn/comments/12gwt5d/gnome_graphite_and_simplicity/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

- [reddit](https://www.reddit.com/r/unixporn/comments/uxajy5/worm_starring_eww_as_panel_dashboard_and_the/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

- [reddit](https://www.reddit.com/r/unixporn/comments/vnexhe/bspwm_hotfiles_tokyo_night_inspired_by_rxyhns_rice/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

## Pop!_OS

I tried Pop!_OS for a day or two, but it didn’t stand out. It was basic, and I quickly reverted to Arch. Although I liked Cosmic, it wasn’t much different from GNOME at that time. However, with the recent activity around the Cosmic project, I’m looking forward to giving it another try soon.

## NixOS

After using Arch for almost three years, I realized it wasn’t as stable as I needed. Although I could proudly say "I use Arch, btw," the latest packages often broke, especially the desktop environment, the mirrors were not as reliable and falling back was not was straightforward. Then I discovered NixOS and was impressed by the concept—one configuration and easy reproducibility. I formatted my Linux drive and installed NixOS using the Calamares installer. Although the installation felt a bit lackluster, I’m really enjoying NixOS. With NixOS, I finally switched to a tiling window manager (Hyprland) and am actively ricing it. Installing packages using a config file didn’t feel intuitive at first, but it has quickly grown on me. The learning curve is steep, and am still not fully comfortable with the home manager.

![img](https://i.imgur.com/Ca4Lcor.png)
*My NixOS-Hyprland rice*

I’m not completely satisfied with the rice, but my curiosity keeps me going. I’ll be updating my dotfiles [here](https://github.com/rumbleFTW/dotfiles) (Work in Progress).

Although arch holds a special place in my heart, and things are better, easier installation with archinstall and overall better community support, I think it's time for me to try something new.

## closing thoughts

I recently bought a MacBook, which has taken up most of my time due to my day job. Despite the shift in my daily workflow, I still find moments to revisit my Linux setup whenever I can. When the MacBook closes, the Linux environment opens, allowing me to continue exploring and tinkering outside of work. Although it sometimes comes handy when I need to try my rust binaries in x86_64, where I ssh into my machine and quickly test/write rust. The journey isn't over—let's see where it leads next.

![img](https://i.imgur.com/JJsP7af.jpeg)
