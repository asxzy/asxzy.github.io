---
layout: post
title: 解决 Android Read-only file system 错误，并设置个性铃声
date: '2011-1-27'
comments: true
---
Android Read-only file system 错误

root之后su

mount -o remount rw（空格）（挂载点）

好了..随便改吧..

其实我就把铃声塞进去了而已。。其他没动。。呵呵

重新挂载/system

cp /mnt/sdcard/(要拷贝的铃声) /system/media/audio/(铃声类型)

“ringtones”（来电铃声）"alarms”（闹钟铃声） “notifications”（短信通知铃声）

好了，进入设置-声音，选择刚才塞进去的铃声吧
