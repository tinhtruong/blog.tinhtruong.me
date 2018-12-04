---
title: "Ibus Unikey is now in the AUR"
date: 2009-12-08T21:58:03+11:00
draft: false
tags: ["arch", "linux"]
---
I've uploaded a PKGBUILD for ibus-unikey to the ArchLinux AUR. You can install it with **yaourt** like this:

```shell
yaourt -S ibus-unikey
```

If you don't want to build from the source, you have to install all the dependencies first:

```shell
pacman -Sy gcc gconf gtk2
```
    
And then download and install the [binary package](http://dl.dropbox.com/u/1059802/wordpress-blog/ibus-unikey-0.3-1-i686.pkg.tar.gz)

Then add the following to your *.bash_profile*
 
```shell
export XMODIFIERS=@im=ibus
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
```

PS: Ok, there is no spyware/malware/rootkit in this binary package! If you don't trust me, don't use this method and build the package yourself (this is the way I recommend)
