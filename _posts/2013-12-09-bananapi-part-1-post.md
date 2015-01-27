---
layout: post
title: Banana Pi
cover: bpi.jpg
date:   2015-01-27 11:08:00
categories: posts
---

## The Banana Pi

For the last year and a half I've been working at my own startup. Recently we decided to call it quits and I set out to find a job. With my added free time I decided to build my own router. I didn't want to learn LUA and I felt the Raspberry Pi was a little underpowered so I decided on the Banana Pi.

For whatever reason I didn't like having to use the supplied Kernel with my device. I wanted to use the mainline kernel. The learning curve was pretty steep, I had never compiled my own kernel. With some work and patience I have the 3.19 rc2 kernel running a clean Arch rootfs.

Here are some of the things I used.

## U-Boot

I used the mainline u-boot from git://git.denx.de/u-boot.git 

The video out works and it supports DTS (Device Tree). I used the Banana Pi DTS file included in the 3.19 kernel.

### Boot.cmd

{% gist ptolts/517e99171e921a1f1111 %}

Here is my boot.cmd. I have various configs depending on what I want. It's easiest to develop on the RPi if you use a network filesystem. That way you can hvae unlimited writes and not worry about corrupting your card.

## Linux 3.19

I used the source from the linux github acct. https://github.com/torvalds/linux

## Arch

I used the following rootfs http://archlinuxarm.org/os/ArchLinuxARM-sun7i-latest.tar.gz

