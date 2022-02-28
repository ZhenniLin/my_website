---
title: "Weekly｜Feb.13-Feb.27 "
subtitle: ""
date: 2022-02-27T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- Weekly
categories:
- Expecto Patronum

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

# See details front matter: /theme-documentation-content/#front-matter
---

## 一些问题

一年内跑了六次Ginus Bar，不知道该说Apple产品小毛病多还是Apple售后做得太过细致入微，总之每次售后的体验感基本可以抹除我对它的信任危机，自己也摸索出了几个自我修缮的小tips，顺便分享售后 Carl Chen 告诉我的几个（省钱）方案


**1.mac 触控版问题**

问题：触控板的按压声音不太对劲，从原来的闷响变成了颗粒响，听起来会非常的annoying / 还是要前期说明，这个问题发生前我的小侄女不小心撒了水在我的键盘上（非大量）

搜索关键字：mac touchpad click sound strang

几个方法：

- 使用 “Apple 诊断” 检测您的Mac是否存在硬件问题 [点击这里](https://support.apple.com/zh-cn/HT202731) - 如果最后返回的 Reference Code 为 ADP000, 说明无硬件相关问题 [了解“Apple 诊断”参考代码](https://support.apple.com/zh-cn/HT203747)

- 排除硬件问题后，一些自我修缮的非保证方法集合 [点击这里](https://discussions.apple.com/thread/7409623)

```

//这是一些我尝试过的方法，摘录下来

//----第一个方法----

Had the same issue which was fixed after calling Apple Care

1. Shut down Macbook

2. Press shift + control + option + power button for approx 10 seconds -- release.

3. Press power button 

This resets the power grid, so to speak. It fixed my issue.

Hope it helps

//----第二个方法----

I had seemingly the same issue for quite some time. S
trange clicking noice like something is trap inside/beneath the trackpad, 
which goes away after some hard presses, but will come back and haunt me soon enough.

I just tried to use the corners of an A4 paper, which is thin and strong enough, 
and stick it into the 4 gaps/sides, and then drag along the  gaps/sides. 
Dusts and stuffs (and even one hair) are cleared out, and the click sounds seem to return to normal.

Maybe this helps.

//----第三个方法----本质上跟第二个方法相似，但不建议小白拧螺丝

Hey all I read all the comments.  This was happening to me too.  
I only did two things and I don't have the issue at all anymore.  

1.  Use compressed canned air and blow out any particles in any of the ports or holes all the way around the laptop

2. Flip the laptop over and tighten the screws NOT ALOT only hand tight, I used an eye glass screwdriver.

Works great.  All the screws were lose and a ton of dust flew out.  
I have to believe that one or the combination caused the clicking.  Good Luck!

//尝试了这几个方法后，问题貌似解决，持续了2-3天问题重新出现就选择去Genius Bar

```

**2.mac 触控版方案**

这里巨感谢我的售后 Carl, 提供了好几个方案能够在资金和时间上进行选择，短期方案采取plan A，长期方案应该是plan C, 但是我的这个问题在用了一天plan A之后又自行解决了 (莫名其妙的)

- plan A：（Mac 进入 偏好设置 -> 触控版 -> 轻点来点按）+ 鼠标

- plan B ：如果键盘出现链接里的三个状况，Apple能够免费更换键盘，触控板也就可以被同步更换掉，当然这三种情况 Apple 指定了相应的机型 [点击这里](https://support.apple.com/zh-cn/keyboard-service-program-for-mac-notebooks)

- plan C : 选择电池更换，因为我的电池基本快接近能够更换的临界点了，所以再狂用一两个月，基本就能达到 Apple 电池的要求了，Carl的意思是，电池更换能通同步更换掉键盘/触控板（不确定有没有记错），价格为1600mop左右 [点击这里](https://www.apple.com.cn/batteries/service-and-recycling/)

- plan D : 全换键盘（触控板就可以同步更换），价格为3500mop左右

**3.mac 耳机连接问题**

问题：耳机型号为二代，出现了和mac连接断续问题，主要表现为连接状态正常但声音一直断断续续

解决方法：直接三个办法全都实施一遍，问题解决 [点击这里](https://juejin.cn/post/7026548304146071582)

```

//以下为转载，具体点击链接

//----第一种方法----

1.断开蓝牙耳机/音响
2.然后打开iTerm或者其他终端，输入下面的命令
	sudo defaults write bluetoothaudiod "Enable AAC codec" -bool true
3.因为使用了sudo命令会要求你输入密码，就是你的登陆密码
4.连接蓝牙耳机。然后就会解决大部分断断续续的问题。

//----第二种方法----
1.在连接蓝牙耳机的状态打开系统偏好设置，找到声音
2.打开声音将sound effects改为mifo o5（你的蓝牙设备）
3.输出也改为mifo o5--这里主要我还插着耳机，如果你那边只有一个耳机这一步可以忽略
4.重点来了输入input改为microphone。这个比较重要，能解决剩下一部分断断续续问题。

//----第三种方法----
1.打开终端输入
defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Min (editable)" 35
defaults write com.apple.BluetoothAudioAgent "Apple Initial Bitpool Min (editable)" 53
defaults write com.apple.BluetoothAudioAgent "Apple Initial Bitpool (editable)" 35

```
<br>

## To be continue





