---
title: mentohust installation
date: 2017-04-13 17:47:51
tags:
---

  explain how to install mentohust on ubuntu
  
<!-- more -->

## download

  download package mentohust_0.3.4-1_amd64.deb(64 bits machine) on https://code.google.com/archive/p/mentohust/downloads

## install

``` bash
$ sudo dpkg -i mentohust_0.3.4-1_amd64.deb
```

## configure
  make sure that your settings are suitable
  all settings are written in /etc/mentohust.conf
```
...
StartMode=1
DhcpMode=1
...
```

## run
```
$ sudo mentohust
```

## note
  mentohust error, can not open libnotify
``` bash
$ sudo apt-get install libnotify-bin
```
  you can also try the following command
``` bash
$ sudo apt-get install libnotify4
```
