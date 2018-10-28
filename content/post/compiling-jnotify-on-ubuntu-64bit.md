---
title: "Compiling JNotify on Ubuntu 64bit"
date: 2012-02-17T22:52:56+11:00
draft: false
tags: ["64bit", "jnotify", "ubuntu"]
author: "Tinh Truong"
---

In my recent project, I have a need to monitor a directory for changes such as a new file created, modified or deleted. Surprisingly, JDK (up to JDK 6) does not have APIs to do that! JDK 7 does support it out of the box but I am stuck with the version 6.

After looking around for an existing solution, I finally found that [jNotify](http://jnotify.sourceforge.net/) seems to fit the need. It supports all the three major platforms (Windows, Linux, and MacOS).The project has not released any update for nearly two years, so it's a little bit tricky to compile the native code. In this post, I will show you how! (at least on a Ubuntu Server 64bit)

In order to build anything serious on Ubuntu, you should install the package build-essentials

```shell
sudo apt-get install build-essential
```

Then download the source code of jNotify from its homepage. Extract it, open a terminal and issue the command: (assuming that you are at the directory jnotify-native-linux-0.93-src)

```shell
cd Release
make
```

On ArchLinux 64bit, the compilation will succeed and you will get a `libjnotify.so` in the same folder. But on my Ubuntu Server 10.04 LTS, I've got this:
 
```shell
/usr/include/asm-generic/fcntl.h:96: error: expected specifier-qualifier-list before ‘pid_t’
```

After Googling around I found this [thread](http://sourceforge.net/projects/jnotify/forums/forum/515553/topic/3770768). Basically, you have to change the file `net_contentobjects_jnotify_linux_JNotify_linux.c` by moving up the `unistd.h` up above the `sys/time.h`. Now issue the command `make`, the compilation will work as expected.  

Happy coding!
