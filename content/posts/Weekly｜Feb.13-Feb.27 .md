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

<br>

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

<br>

**2.mac 触控版方案**

这里巨感谢我的售后 Carl, 提供了好几个方案能够在资金和时间上进行选择，短期方案采取plan A，长期方案应该是plan C, 但是我的这个问题在用了一天plan A之后又自行解决了 (莫名其妙的)

- plan A：（Mac 进入 偏好设置 -> 触控版 -> 轻点来点按）+ 鼠标

- plan B ：如果键盘出现链接里的三个状况，Apple能够免费更换键盘，触控板也就可以被同步更换掉，当然这三种情况 Apple 指定了相应的机型 [点击这里](https://support.apple.com/zh-cn/keyboard-service-program-for-mac-notebooks)

- plan C : 选择电池更换，因为我的电池基本快接近能够更换的临界点了，所以再狂用一两个月，基本就能达到 Apple 电池的要求了，Carl的意思是，电池更换能通同步更换掉键盘/触控板（不确定有没有记错），价格为1600mop左右 [点击这里](https://www.apple.com.cn/batteries/service-and-recycling/)

- plan D : 全换键盘（触控板就可以同步更换），价格为3500mop左右

<br>

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

## 一些有趣的

**1.上课抓住了老师的一个小bug**

这学期选择了一门有关simulation method的课程，上课会用到Netlogo系统编写程序。当时老师小程序的初始设定为turtles生命值=5，每次移动下没有吃到patches生命值自动minus 1，一旦吃到patches则重回生命值5。接着程序里又添加了一个side-bar，创造一个自定义的生命值链接，之后不用修改code转而移动side-bar里的数值就可以自定义turtle的生命值

但在code栏里，老师只置换连接了setup里的初始值，并没有置换turtles一旦吃到patches就重回生命值满格的模块，所以即便我们将side-bar中的值自定义到20，一旦turtle饿过一次后再吃到patches，它的生命值也只能重回到5而不是20

写code真的有察觉到自己的逻辑理解能力与推演能力在上升，有一种稳稳的满足感

<br>

**2.反复审视对数学的态度**

可能也是因为在补CS相关的内容，慢慢地接受与开拓出了一个新的视野与实践领域，发觉自己对 “数学” 的心态发生了太多的改变

我隐约察觉到我对数学的不自信来源于一种恐惧，这样的恐惧长期根植于我的内心，很难说这种恐惧是我自发而生的，我想它更多来自家庭、班级以及学校的整体氛围中，当我是一个数学成绩不好的女孩，似乎更能被大众接受和理解，这比我努力成为一位数学成绩优秀的女生要来得更轻松

我的潜意识好像在告诉我，作为一名文科女生，数学成绩不太好也没有很大的关系，因为有整个透明的意识网在为这样的想法兜底，你可以安安全全地躺在网内。一旦我尝试迈出，那种恐惧就像被吊起在半空凝滞一样，在它面前我失去了一种勇气，永远被悬挂着那样慌慌张张

为什么会这样，为什么曾经我会失去那样的勇气，那个时候的我不曾领悟到数学中抽象与规律之下的渴求，它与多个学科结合下的巧妙，以及作为纯粹知识的光彩

对于数学的理解，在成绩评定的体系之下我并没有做得很好，多半是因为我对它始终抱有应试学科的态度，那么失败和成功便是有标准定义的，我想这也不是我的过失，重新认识它之后， 希望能以纯粹知识的心态去理解它，即便遇到瓶颈，也能够以欣赏的角度意识到我在面对一片富饶之地

<br>

**3.只有影院能停止我快跳的习惯了**

有段时间不太理解为什么室友看剧喜欢开倍速，后来发现自己看剧已经无法克制跳进度条的冲动了，即便我知道或许就在这一秒的停滞里，景深的调度与人物的微表情传达能够让我更加领会到这个镜头的丰富意涵，但我还是选择了跳进度条....

想了想着跟弹幕又有多大的区别呢，想起来戴锦华老师提到这本质上构成了两种图层，当它彼此叠加在一起的时候，我必须做出选择






