---
layout: post
title: AUFS Read Only Filesystem
cover: bpi.jpg
date:   2015-01-27 13:48:00
categories: banana-pi
---

## Intro

Aufs is a layered filesystem. You could use it to make 4 disks look like 1 among other things. I used it to make the SD card on a SBC read only which protects it from corruption. Once implemented, I haven't had a corrupted card since. 

Obviously nothing will persist to disk, but it wouldnt be hard to create another partition to persist too. I believe this would still protect the essential parts of the filesystem.

## Aufs

Aufs can be acquired from git://git.code.sf.net/p/aufs/aufs3-linux 

Clone that into the root of your Kernel source and follow the Aufs instructions. I have used the linux-3.x-rcN branch on 3.19 rc2 with no problems.

## The magic

The following init script is to be executed by the kernel. This will write everything written to the rootfs to RAM. It's possible somebody could come up with a way of safely persisting this to the card, or maybe to a network fs. Either way, it makes the whole system stable.

{% gist  ptolts/67930e4110193b3f4657 %}

Now you must pass the kernel a bootarg something like this:

{% highlight make %}
setenv bootargs console=ttyS0,115200 console=tty0 consoleblank=0 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait ro noatime init=/sbin/router-init.sh
{% endhighlight %}

## Improvements

I think maybe using a tmpfs with a set limit would allow for things like df to work correctly. If you have any others, please let me know!