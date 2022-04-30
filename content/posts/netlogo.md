---
title: "NetLogo｜复习"
subtitle: ""
date: 2022-03-21T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: " "
keywords: ""
license: ""
comment: false
weight: 0

tags:
- 项目
categories:
- 项目

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

<!--more-->


## Netlogo 工具

<br>

Mac 推荐使用 6.2.2 版本

需要用到的网站：

[NetLogo Home Page](https://ccl.northwestern.edu/netlogo/)

[NetLogo 6.2.2 User Manual](https://ccl.northwestern.edu/netlogo/docs/)

[Programming Guide](https://ccl.northwestern.edu/netlogo/docs/programming.html)

[Interface Tab Guide](https://ccl.northwestern.edu/netlogo/docs/interfacetab.html#plots)

[NetLogo Dictionary](http://ccl.northwestern.edu/netlogo/docs/index2.html)

<br>


## Class 01

<br>

### Task_1

先参考了一个山火模型

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kz4px1xqj211z0u0ncw.jpg)

```
  initial-trees   ;; how many trees (green patches) we started with
  burned-trees    ;; how many have burned so far
]

breed [fires fire]    ;; bright red turtles -- the leading edge of the fire
breed [embers ember]  ;; turtles gradually fading from red to near black

to setup
  clear-all
  set-default-shape turtles "square"
  ;; make some green trees
  ask patches with [(random-float 100) < density]
    [ set pcolor green ]
  ;; make a column of burning trees
  ask patches with [pxcor = min-pxcor]
    [ ignite ]
  ;; set tree counts
  set initial-trees count patches with [pcolor = green]
  set burned-trees 0
  reset-ticks
end

to go
  if not any? turtles  ;; either fires or embers
    [ stop ]
  ask fires
    [ ask neighbors4 with [pcolor = green]
        [ ignite ]
      set breed embers ]
  fade-embers
  tick
end

;; creates the fire turtles
to ignite  ;; patch procedure
  sprout-fires 1
    [ set color red ]
  set pcolor black
  set burned-trees burned-trees + 1
end

;; achieve fading color effect for the fire as it burns
to fade-embers
  ask embers
    [ set color color - 0.3  ;; make red darker
      if color < red - 3.5     ;; are we almost at black?
        [ set pcolor color
          die ] ]
end


; Copyright 1997 Uri Wilensky.
; See Info tab for full copyright and license.

```

<br>

### Task_2

要求：牛+草坪

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kz6hjfpaj211p0u0769.jpg)



```
to setup
  clear-all ;把之前所有东西都清掉
  create-turtles 100 [
   setxy random-xcor random-ycor
   set shape "cow"
  ]
  ask patches[
    set pcolor green
  ]
end


to go
  ask turtles[
    set heading random 360
    forward 1 ;表示向前跑一个单位
  ]
end

```


<br>


### Task_3

要求：背景 + 圆形

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kzbc0cocj20zm0u0dhm.jpg)

```
to setup

  clear-all ;reset the scree
  create-turtles 100[ ;create 100 turtles
    set shape "bug"
    forward 10
  ]
  ask patches[ ;想尝试换一下背景颜色
    set pcolor 138
  ]
end

```


<br>


### Task_4

要求：两个圆形 + 小圆绕大圆

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kzd1orwlj210t0u0dh6.jpg)



```
;全部转换了一下颜色

to setup
  clear-all
  create-turtles 1[
    set shape "circle"
    set color 138
    set size 5
  ]

  create-turtles 1[
    set shape "circle"
    set color 4
    setxy 0 8
    set heading 90
  ]

  ask patches [
    set pcolor 132
  ]
end

to go
  ask turtle 1[
    forward 1
    set heading heading + 7.17
  ]
end

```

<br>

## Class 02

<br>

### Task_05

要求：上下两种不同颜色切割

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kzgdvr9ij211c0u00ty.jpg)

```
to setup
  clear-all
  ask patches [
    ifelse pycor > 0
       [set pcolor 38]
       [set pcolor 9.5]
  ]
end

```

<br>

### Task_06

要求：四分之一颜色切割

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kziatwmij211i0u0jsk.jpg)

```
to setup
  clear-all
  ask patches [
    ifelse (pycor > 0) or (pxcor > 0)
       [set pcolor 139.5]
       [set pcolor 9]
  ]
end

```

<br>

### Task_07

要求：条纹颜色切割

![截屏2022-03-24 下午3.05.24](/Users/juanne/Library/Application Support/typora-user-images/截屏2022-03-24 下午3.05.24.png)

```
to setup
  clear-all
  ask patches [
    ifelse (pycor mod 2 = 1)
       [set pcolor 139.5]
       [set pcolor 38]
  ]
end

```

<br>

### Task_08

要求：patches 随机色

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0kzkaiu0xj211s0u0wor.jpg)

```to setup
  
  clear-all
  ask patches [
    let choice random 5 ;0,1,2,3,5 - 5个选一个
    (ifelse
        choice = 0 [
          set pcolor red
          set plabel "r"
        ]
         choice = 1 [
          set pcolor blue
          set plabel "b"
        ]
         choice = 2 [
          set pcolor green
          set plabel "g"
        ]
         choice = 3 [
          set pcolor pink
          set plabel "p"
        ]
        [
          set pcolor yellow
          set plabel "y"
    ])
  ]
end

```

<br>

## Class 03

<br>

### Task_09

要求：草坪 + 土壤 + 小牛 + 3个monitor检测

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0l0k9hkjsj210z0u0n18.jpg)

```
turtles-own [life] ;define a new porperty


to setup
  ca ;clear all

  ;initiate the ground
  ask patches [
    let i int random-normal 0 1
    ;i是变量variable 正态分布 int会将返回的小数取整 增加/减少0的概率
    ifelse i = 0
    [set pcolor green]
    [set pcolor brown]
  ]

  ;initiate the cow
  crt 100 [ ;create turtles
    set shape "cow"
    set color yellow
    set life 5
    setxy random-xcor random-ycor ;所有牛位置随机
  ]

end

to go
  ask turtles [
    right random 360 ;;随机跑 right random 360 和 left random 360 一样
    fd 1 ;;forward 1

    ifelse pcolor = green ;;牛所在位置的pcolor
    [
      set pcolor black
      set life 5
    ]
    [set life life - 1]

    if life = 0 [die]

    ;;print life
    set label life

  ]


end

```

- monitor - No.of cows - count turtles
- monitor - No.of glass - count patches with [pcolor = green]
- monitor - ( cows - life ) - count turtles with [life = 5]

<br>

### Task_10


![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0l1z450knj21060u0wio.jpg)

```
;;以下为主程序

turtles-own [life] ;define a new porperty


to setup
  ca ;clear all
  reset-ticks

  initiate_the_ground

  initiate_the_cow

end

to go
  ask turtles [
    right random 360 ;;随机跑 right random 360 和 left random 360 一样
    fd 1 ;;forward 1

    ifelse pcolor = green ;;牛所在位置的pcolor
    [
      set pcolor black
      set life 5
    ]
    [set life life - 1]

    if life = 0 [die]

    ;;print life
    set label life
  ]

  if count turtles = 0
  [stop] ;;牛数量没有的时候，plot停掉

  regrow_grass

  tick ;;每跑一次go都要tick一下plot

end



;;以下为子程序

to regrow_grass ;;子程序 主程序就留一样的名字
    ask patches [
    if pcolor != green [
      if random 100 < 1 ;百分之一的几率跑下面这个
      [set pcolor green]
    ]
  ]
end

to initiate_the_ground
  ask patches [
    let i int random-normal 0 1
    ;i是变量variable 正态分布 int会将返回的小数取整 增加/减少0的概率
    ifelse i = 0
    [set pcolor green]
    [set pcolor brown]
  ]
end

to initiate_the_cow
  crt 100 [ ;create turtles
    set shape "cow"
    set color yellow
    set life 5
    setxy random-xcor random-ycor ;所有牛位置随机
  ]
end

```

- plot图示

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ql0dsgdgj20y60p6wh8.jpg)


<br>


### Task_11

- 加入plot

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ql1njk61j215m0u0wim.jpg)

```
;;以下为主程序

turtles-own [life energy gender] ;define two new porperties


to setup
  ca ;clear all
  reset-ticks

  initiate_the_ground

  initiate_the_cow

end

to go
  ask turtles [
    right random 360 ;;随机跑 right random 360 和 left random 360 一样
    fd 1 ;;forward 1

    ifelse pcolor = green ;;牛所在位置的pcolor
    [
      set pcolor black
      set life n_life
      set energy energy + 1
    ]
    [set life life - 1]

    if life = 0 [die]

    ;;print life
    set label life
  ]

  if count turtles = 0
  [stop] ;;牛数量没有的时候，plot停掉

  regrow_grass

  reproduce

  tick ;;每跑一次go都要tick一下plot

end


;;以下为子程序

to regrow_grass ;;子程序 主程序就留一样的名字
    ask patches [
    if pcolor != green [
      if random 100 < no_grass ;百分之一的几率跑下面这个
      [set pcolor green]
    ]
  ]
end

to initiate_the_ground
  ask patches [
    let i int random-normal 0 1
    ;i是变量variable 正态分布 int会将返回的小数取整 增加/减少0的概率
    ifelse i = 0
    [set pcolor green]
    [set pcolor brown]
  ]
end

to initiate_the_cow
  crt n_cows [ ;create turtles n_cows是slider
    set shape "cow"
    set color yellow
    set life n_life
    setxy random-xcor random-ycor ;所有牛位置随机
    set energy 0
  ]
end

to reproduce
  ask turtles [
    if energy = 3 [
      hatch 1 [ ;得到一头新牛
        set energy 0 ;新牛baby的energy
        set color red
      ]
     set energy 0 ;已经吃了3次草的牛的energy
    ]
  ]
end
```

- 三个slider设置

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ql5y2rm7j215c0bmq41.jpg)

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ql6gpbqij215i0bymyd.jpg)

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ql6ttksvj215o0bumyh.jpg)

<br>

### Task_12

- slider设置（变量名称code也要对应） + 颜色设置

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0ql3b6cyuj21660u0n1c.jpg)



```
;;以下为主程序
;;新要求：设置分为母牛和公牛，母牛遇到功能且energy为3生下baby

turtles-own [life energy gender] ;define two new porperties


to setup
  ca ;clear all
  reset-ticks

  initiate_the_ground

  initiate_the_cow

end

to go
  ask turtles [
    right random 360 ;;随机跑 right random 360 和 left random 360 一样
    fd 1 ;;forward 1

    ifelse pcolor = green ;;牛所在位置的pcolor
    [
      set pcolor black
      set life n_life
      set energy energy + 1
    ]
    [set life life - 1]

    if life = 0 [die]

    ;;print life
    set label life
  ]

  if count turtles = 0
  [stop] ;;牛数量没有的时候，plot停掉

  regrow_grass

  reproduce

  tick ;;每跑一次go都要tick一下plot

end


;;以下为子程序

to initiate_the_ground
  ask patches [
    let i int random-normal 0 1
    ;i是变量variable 正态分布 int会将返回的小数取整 增加/减少0的概率
    ifelse i = 0
    [set pcolor green]
    [set pcolor brown]
  ]
end

to initiate_the_cow
  crt n_cows [ ;create turtles n_cows是slider
    set shape "cow"
    set color blue
    set life n_life
    setxy random-xcor random-ycor ;所有牛位置随机
    set energy 0
    set gender random 2
    if gender = 1 [set color red];; assign gender: 0 = male 1 = female
  ]

end



to regrow_grass ;;子程序 主程序就留一样的名字
    ask patches [
    if pcolor != green [
      if random 100 < no_grass ;百分之一的几率跑下面这个
      [set pcolor green]
    ]
  ]
end

to reproduce
  ask turtles with [gender = 0][
    ask turtles-here with [gender = 1 and energy >= 3] [
      hatch 1 [ ;得到一头新牛
        set energy 0 ;新牛baby的energy
        set color yellow
        set gender random 2
        print who
      ]
     set energy 0 ;已经吃了3次草的牛的energy
    ]
    set energy 0;
  ]
end

```

<br>

## Class 04

<br>

### Task_13

- 测试 圆周率

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qn3wcvkqj211u0tsgnt.jpg)

```
to setup
  ca
  ;;(1) draw a circle
  ask patches [
    set pcolor red
    if distance patch 0 0 <= 200 [set pcolor yellow]
  ]
end


;;(2) throw beans
to throw_beans
  crt 1000[
    set shape "circle"
    set size 2
    setxy random-xcor random-ycor
  ]
end

```

- Monitor - total beans - count turtles
- Monitor - beans on the circle - count turtles with [pcolor = yellow]
- Monitor - (count turtles with [pcolor = yellow] / count turtles) * 4

<br>

### Task_14

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qsw2ii1sj20z40tu19p.jpg)

```
to setup
  clear-all

  ask patches [
    set pcolor green + random 10 ;;random 10返回0-9的随机数，颜色就会在green基础上变化
    if distance patch -90 0 + distance patch 90 0 <= 210 [set pcolor yellow + random 5]
  ]

end

to throw_beans
  crt 100[
    setxy random-xcor random-ycor
    set shape "circle"
    set size 5
  ]
end
```

- monitor - total turtles - count turtles
- monitor - () - count turtles with [distance patch -90 0 + distance patch 90 0 <= 210]
- monitor - () - count turtles with [distance patch -90 0 + distance patch 90 0 <= 210 ] / count turtles * 100

<br>

### Task_15

- 导入图片 - 算面积

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qusia78aj20u00y2n0f.jpg)

```
to setup
  ca
  import-pcolors "Macau_map.png" ;;可以把图片放在patch的颜色上面
end

to throw_beans
  crt 100 [
    set shape "circle"
    set size 3
    setxy random-xcor random-ycor
  ]
end
```

- monitor - total beans - count turtles with [pcolor != 9.9]
- monitor - beans (Coloane) - count turtles with [pcolor = 117.1]
- monitor - area of Coloane - count turtles with [pcolor = 117.1] / count turtles with [pcolor != 9.9] * 33

<br>

### Task_16

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0quweb7gpj20u00xitbt.jpg)

```
to setup
  ca
  import-pcolors "Macau_map.png" ;;可以把图片放在patch的颜色上面
end

to throw_beans
  crt 100 [
    set shape "circle"
    set size 3
    setxy random-xcor random-ycor
  ]
end

to draw
  if mouse-down? [ ;;return boolean value: true or false
    ask patch mouse-xcor mouse-ycor [
      ;; 半径为5的pat执行commend
      ask patches in-radius pen_size [set pcolor pen_color]
    ]
  ]
end
```

- Input - pen_color (创建了这个全局变量) -  type color 
- Slider - pen_size (创建了这个全局变量) 

<br>

### 课后

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0quzwom5wj20u00ux41d.jpg)

```
to setup
  ca
  import-pcolors "Macau_map.png" ;;可以把图片放在patch的颜色上面
  print choosing_color
end

to throw_beans
  crt 100 [
    set shape "circle"
    set size 3
    setxy random-xcor random-ycor
  ]
end

to draw
  if mouse-down? [ ;;return boolean value: true or false
    ask patch mouse-xcor mouse-ycor [
      ;; 半径为5的pat执行commend
      ask patches in-radius pen_size [set pcolor pen_color]
    ]
  ]
end
```


<br>


## Class 05

<br>

### Task_17

要求：遇到人停车

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qv3uytqgj21me0osdic.jpg)

```
globals [isSafe?] ;;boolean value true or false


;;setup和go主程序

to setup
  ca
  draw_road
  add_car
  add_person
  set isSafe? true
end


to go
  car_move
  person_walk
end


;;setup子程序

to draw_road
  ask patches [
    set pcolor green - random-float 0.5 ;;返回随机数颜色数 减去0-0.5 达成随机效果
  ]

  ask patches with [abs pycor < 5] [ ;;abs 绝对值取值
    set pcolor grey - 2.5 + random-float 0.25
  ]

  ask patches with [ (abs pycor < 5 and pycor mod 2 = 1) and abs pxcor < 6 ] [
    set pcolor white
  ]
end

to add_car
  crt 1 [
    setxy -19 0
    set size 3
    set shape "car"
    set heading 90
    set color orange
  ]
end

to add_person
  crt 1 [
    setxy 0 -7
    set size 3
    set shape "person"
    set heading 0 ;;不改的话就是随机数
    set color red
  ]
end

;;go子程序

to car_move
  ask turtle 0 [
    ifelse isSafe?
    [fd 1]
    [
      if xcor < -6 or xcor > 0 [fd 1]
    ]
  ]
end

to person_walk
  ask turtle 1 [
    forward 0.1 ;;fd

    ifelse abs ycor < 5
    [set isSafe? false]
    [set isSafe? true]

    print isSafe?
  ]
end
```

<br>

### Task_18

要求：遇到多人停车

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qv4w76cbj21me0q0tb8.jpg)

```
globals [isSafe?] ;;boolean value true or false
breed [cars car]
breed [persons person]



;;setup和go主程序

to setup
  ca
  draw_road
  add_car
  add_person
  set isSafe? true
end


to go
  car_move
  person_walk
end


;;setup子程序

to draw_road
  ask patches [
    set pcolor green - random-float 0.5 ;;返回随机数颜色数 减去0-0.5 达成随机效果
  ]

  ask patches with [abs pycor < 5] [ ;;abs 绝对值取值
    set pcolor grey - 2.5 + random-float 0.25
  ]

  ask patches with [ (abs pycor < 5 and pycor mod 2 = 1) and abs pxcor < 6 ] [
    set pcolor white
  ]
end

to add_car
  create-cars 1 [
    setxy -19 0
    set size 1
    set shape "car"
    set heading 90
    set color orange
  ]
end

to add_person
  create-persons 5 [
    setxy random-normal 0 2 random-normal 0 3 ;;产生以0为mean 3为sd的随机数
    set size 1
    set shape "person"
    set heading 0 ;;不改的话就是随机数
    set color red
  ]
end

;;go子程序

to car_move
  ask car 0 [
    ifelse isSafe?
    [fd 1]
    [
      if xcor < -6 or xcor > 0 [fd 1]
    ]
  ]
end

to person_walk
  ask persons [
    forward random-normal 0.1 0.2;;fd

    ifelse any? persons-on patches with [abs pxcor < 5 and abs pycor < 4] ;;any是在后面的是不是一个空集
    [set isSafe? false]
    [set isSafe? true]

    print isSafe?
  ]
end

```


<br>


### Task_19

- 遇到红灯停，但是车会重叠

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvewntpyj21lm0poju4.jpg)

```
breed [lights light]
breed [cars car]
globals [isGreen?]
;;分享函数 one-of [-1 0 1] 随机数


;;setup主程序

to setup
  ca
  reset-ticks
  draw_road
  add_light
  add_car
end

;;go主程序

to go
  move_car
  run_light
  tick
end

;;setup子程序

to draw_road
  ask patches [
    set pcolor green - random-float 0.5 ;;返回随机数颜色数 减去0-0.5 达成随机效果
  ]

  ask patches with [abs pycor < 2] [ ;;abs 绝对值取值
    set pcolor grey - 2.5 + random-float 0.25
  ]

end

to add_light
  create-lights 1 [
    setxy 0 2
    set shape "circle"
    set size 0.8
    set color green
    set isGreen? true
    set pcolor black
  ]
end

to add_car
  ;create-cars 10 [
   ; setxy random -41 + 20 one-of [-1 0 1] ;-15 到 15 之间 ｜ one-of [-1 0 1]产生这三个值的其中一个 或者用 random 3 - 1;;
   ;set shape "car"
   ; set heading 90
  ;]

  ;;这个方法不会产生重叠的情况
  ask n-of 10 patches with [abs pycor < 2][ ;; 10 of patches with this condition
    sprout-cars 1 [
      set heading 90
      set shape "car"
    ]
  ]
end

;;go 子程序

to move_car
  ask cars [
    ifelse xcor < -1 or xcor > 0
    [fd 1]
    [if isGreen?[fd 1]]
  ]
end

to run_light
  ask lights [
    if ticks mod 50 = 0 [
      ifelse color = green [
        set color red
        set isGreen? false
      ]
    [
      set color green
      set isGreen? true
    ]
   ]
  ]
end

```




<br>


## Class 06

<br>

### Task 20

要求：遇到红灯停，并且车不会重叠

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvkfmo8jj21lw0putba.jpg)

```
breed [lights light]
breed [cars car]
globals [isGreen?]
;;分享函数 one-of [-1 0 1] 随机数


;;setup主程序

to setup
  ca
  reset-ticks
  draw_road
  add_light
  add_car
end

;;go主程序

to go
  move_car
  run_light
  tick
end

;;setup子程序

to draw_road
  ask patches [
    set pcolor green - random-float 0.5 ;;返回随机数颜色数 减去0-0.5 达成随机效果
  ]

  ask patches with [abs pycor < 2] [ ;;abs 绝对值取值
    set pcolor grey - 2.5 + random-float 0.25
  ]

end

to add_light
  create-lights 1 [
    setxy 0 2
    set shape "circle"
    set size 0.8
    set color green
    set isGreen? true
    set pcolor black
  ]
end

to add_car
  ;create-cars 10 [
   ; setxy random -41 + 20 one-of [-1 0 1] ;-15 到 15 之间 ｜ one-of [-1 0 1]产生这三个值的其中一个 或者用 random 3 - 1;;
   ;set shape "car"
   ; set heading 90
  ;]

  ;;这个方法不会产生重叠的情况
  ask n-of 10 patches with [abs pycor < 2][ ;; 10 of patches with this condition
    sprout-cars 1 [
      set heading 90
      set shape "car"
    ]
  ]
end

;;go 子程序

to move_car
  ask cars [
    if count cars-on patch-ahead 1 = 0 [ ;;patch-ahead count cars-on
      ifelse xcor < -1 or xcor > 0
      [fd 1]
      [if isGreen?[fd 1]]
     ]
  ]
end

to run_light
  ask lights [
    if ticks mod 50 = 0 [
      ifelse color = green [
        set color red
        set isGreen? false
      ]
    [
      set color green
      set isGreen? true
    ]
   ]
  ]
end
```

<br>

### Task 21

要求：能画圈把飞机框住

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvnl12frj20z80u00u4.jpg)

```
to setup
  ca
  crt 1 [
    set size 3
    set color yellow
    set shape "airplane"
  ]

end

to draw
  if mouse-down? [
    ask patch mouse-xcor mouse-ycor [
      ask patches in-radius 1 [set pcolor grey]
    ]
  ]
end

to go
  ask turtles [
    fd 1
    set heading heading + random-normal 0 5 ;0为1 standard deviation 5 正负5
    ;; 想要turtle能够使用neighbors辨别
    if count neighbors with [pcolor = grey] > 3[
      set heading heading + 90
    ]
  ]
end
```

<br>

### Task 22

- 用到foreach 创建乌龟

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvqg4nxcj210t0u0abo.jpg)

```
turtles-own [speed]


to setup
  ca

  foreach [1 2 3 4 5 6 7 8 9 10][
  x ->
  crt 1[
    set shape "turtle"
    setxy random-xcor random-ycor
    set heading 0
    set size x / 2
    set speed x
  ]
 ]

end

to go
  ask turtles [
    forward speed
  ]
end
```


<br>

### Task 23

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvsj3ob6j20u00v30uj.jpg)

```
turtles-own [income]
globals [i j]

to setup
  ca
  set i 1 ;初始化值
  set j 0;

  crt 10 [
    set shape "person"
    setxy random-xcor random-ycor
    ;;set income int (random-float 1) * (2000 - 10000) + 10000
    set income random 1001 + 1000 ;1000-2000
    set label income
  ]

  foreach [income] of turtles [;;创建了一个income的list
    x ->
    print (word "Income#" i ": " x)
    set i i + 1
    set j j + x
  ] print (word "Total = " j "!")


end
```

<br>

## Class 07

<br>

### Task_24

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvzw9tdzj214n0u042c.jpg)

```
to setup
  ca

  ;;从左到右 从下到上的顺序
  foreach [-15 -12 -9 -6 -3 0 3 6 9 12 15][
    x ->
    foreach [-12 -9 -6 -3 0 3 6 9 12] [
      y ->

      ifelse x = 0 or y = 0 [
         crt 1 [
      set shape "tree"
      set size 2
      setxy x y

      ]
      ]
        [
          crt 1 [
      set shape "house"
      set size 2
      setxy x y

        ]
     ]
    ]
  ]


end
```

<br>

### Task_25

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qw0ldc7gj21c60u00vi.jpg)

```
breed [roadsigns roadsign]

to setup
  ca

  draw_road



end

to draw_road
  ask patches [
    set pcolor 2 - random-float 1
  ]

  ask patches with [abs pycor = 1 or abs pxcor = 8 or abs pxcor = 10] [
    set pcolor white
  ]

  ask patches with [pycor = 0] [
    set pcolor 2
  ]

  add_roadsign
end

to add_roadsign
  foreach [-25 -20 -15 -10 -5 0 5 10 15 20 25] [
    x ->
    create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      setxy x 1
      set heading 90
    ]
  ]

  foreach [-23 -18 -13 -8 -3 2 8 12 17 22] [
    x ->
    create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      setxy x -1
      set heading 270
  ]
 ]

  foreach [-8 8] [
    x ->
    foreach [-15 -10 -5 5 10 15][
      y ->
      create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      set heading 180
      setxy x y
      ]
    ]
  ]

  foreach [-10 10] [
    x ->
    foreach [-15 -10 -5 5 10 15][
      y ->
      create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      set heading 0
      setxy x y
      ]
    ]
  ]

  foreach [-10 10] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 90
      setxy x 1
      ]
  ]

  foreach [-8 8] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 270
      setxy x -1
      ]
  ]

  foreach [-8 8] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 180
      setxy x 2
      ]
  ]

  foreach [-10 10] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 0
      setxy x -2
      ]
  ]
end

```

<br>



### Task_26

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qw2htf27j21bs0u0n01.jpg)

```
breed [roadsigns roadsign]
breed [cars car]


to setup
  ca
  draw_road
  add_car
end

to go
  move_forward

end

to move_forward
  ask cars [
    if count other turtles-here = 2 [
      if random 100 < 50 [lt 90] ;; set heading heading - 90    or    leftturn 90
    ]

    if count other turtles-here = 1 and count other turtles-here with [shape = "leftturn_forwad"] = 1 [
      fd 1
      lt 90

    ]
    fd 1


  ]
end


to add_car
  create-cars 1 [
    set shape "car top"
    setxy 0 1
    set size 2
    set heading 90
  ]
end

to draw_road
  ask patches [
    set pcolor 2 - random-float 1
  ]

  ask patches with [abs pycor = 1 or abs pxcor = 8 or abs pxcor = 10] [
    set pcolor white
  ]

  ask patches with [pycor = 0] [
    set pcolor 2
  ]

  add_roadsign
end

to add_roadsign
  foreach [-25 -20 -15 -10 -5 0 5 10 15 20 25] [
    x ->
    create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      setxy x 1
      set heading 90
    ]
  ]

  foreach [-23 -18 -13 -8 -3 2 8 12 17 22] [
    x ->
    create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      setxy x -1
      set heading 270
  ]
 ]

  foreach [-8 8] [
    x ->
    foreach [-15 -10 -5 5 10 15][
      y ->
      create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      set heading 180
      setxy x y
      ]
    ]
  ]

  foreach [-10 10] [
    x ->
    foreach [-15 -10 -5 5 10 15][
      y ->
      create-roadsigns 1[
      set shape "forward_sign"
      set color grey
      set heading 0
      setxy x y
      ]
    ]
  ]

  foreach [-10 10] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 90
      setxy x 1
      ]
  ]

  foreach [-8 8] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 270
      setxy x -1
      ]
  ]

  foreach [-8 8] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 180
      setxy x 2
      ]
  ]

  foreach [-10 10] [
    x ->
    create-roadsigns 1[
      set shape "leftturn_sign"
      set color grey
      set heading 0
      setxy x -2
      ]
  ]
end
```


<br>


### 练习

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qw1nbiw0j21090u0794.jpg)

```
globals [i j]

to setup
  ca


  foreach [-18 -15 -12 -9 -6 -3 0 3 6 9 12 15 18] [
    x ->
    foreach [-15 -12 -9 -6 -3 0 3 6 9 12 15] [
      y ->

      foreach [5 4 3 2 1][
        z ->
      create-turtles 1 [
        set shape "circle"
        setxy x y
        set size z / 2
        set color z ;;

      ]
     ]
    ]
  ]



end
```

<br>

## Class 08

<br>

### Task_27

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qw4d79hpj20zc0u040y.jpg)

```
globals[step ]

to setup
  ca
  ask n-of 100 patches [ set pcolor green ]

  crt 1[
    set shape "bug"
    setxy -16 16
    set color yellow
    set heading 90
  ]
end

to go
  ask turtles[
    pen-down;;画出轨迹；；pen-up停止画
    while[ pcolor != green][
      if count patches with [pcolor = green] = 0 [stop]
      set heading one-of [0 90 180 270]
      fd 1
      set step step + 1
     ]
    set pcolor black
  ]
end
```

<br>

### Task_28

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qw6aj2lwj20yu0u0q5w.jpg)

```
globals[step]

to setup
  ca
  ask n-of 100 patches [ set pcolor green ]

  crt 1[
    set shape "bug"
    setxy -16 16
    set color yellow
    set heading 90
  ]
end

to go
  ask turtles[

    pen-down;;画出轨迹；；pen-up停止画

    while[pycor >= -16][;;算的是16的那一个状况，跑一个
      fd 1
      set step step + 1
      if pcolor = green[set pcolor black]
      while[abs pxcor < 16][;;-15~15；；中间的大直线的状况
        fd 1
        set step step + 1
        if pcolor = green[set pcolor black]
        if count patches with [pcolor = green] = 0 [stop]
      ]
        move_down
    ]
  ]

end

to move_down
  set heading 180
  fd 1
  set step step + 1
  if pcolor = green[set pcolor black]
  ifelse pxcor = 16 [set heading -90][set heading 90 ]
end
```

<br>

### Task_29

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qw7hu40wj20zp0u0tb9.jpg)

```
globals[step target-patch]

to setup
  ca
  ask n-of 100 patches [ set pcolor green ]

  crt 1[
    set shape "bug"
    setxy -16 16
    set color yellow
    set heading 90
  ]
end

to go
  ask turtles[

    pen-down;;画出轨迹；；pen-up停止画

    if count patches with [pcolor = green ] = 0 [stop]
    set target-patch min-one-of(patches with [pcolor = green])[distance myself]
    set step step + [distance myself] of target-patch
    face target-patch ;;no face就会一直保持一个方向
    move-to target-patch
    set pcolor black
  ]
end

```



<br>



## Class 09

<br>

### Task_30

要求：构建links 狼吃羊 羊吃虫

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qpfmlhs0j210t0u0juj.jpg)

```
;;with 无方向 to/from 有方向-相反
;;记住shape用string要"" 并且是单数
breed [wolves wolf]
breed [sheeps sheep]
breed [bugs bug]

to setup
  ca

  create-wolves 2 [
    setxy random-xcor random-ycor
    set shape "wolf"
    set size 2
  ]

  create-sheeps 4 [
    setxy random-xcor random-ycor
    set shape "sheep"
    set size 2
  ]

  create-bugs 10 [
    setxy random-xcor random-ycor
    set shape "bug"
    set size 2
  ]

  ask wolves [create-links-to sheeps]
  ask sheeps [create-links-to bugs]


end

to eat
  ask one-of wolves [
    ask one-of out-link-neighbors [die]
  ]

end
```

<br>



### Task_31

要求：分开两个区域 / 传递方向和颜色

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qpdzhd47j211q0u0qei.jpg)

```
turtles-own [gender]
links-own [score]


to setup
  ca 
  ask patches [sprout 1] ;;每个格子都有一个turtle
  
  ask turtles with [xcor < 0] [
    ;;在patch上有turtle的neighbors
    create-links-with turtles-on neighbors [
      set score sum [color] of both-ends ]
  ]
  
  ask turtles with [xcor > 1] [
    ;;在patch上有turtle的neighbors
    create-links-with turtles-on neighbors 
  ]

end  

to diffuse_
  ask turtles [
    ask link-neighbors [set color (color + [color] of myself) / 2] ;;neighbors的color和我的color
    ask link-neighbors [set heading (heading + [heading] of myself) / 2]
  ]
  
end  
```

<br>

### Task 32

要求：满足三种link情况

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvwixvymj211t0u075x.jpg)

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvwoygw8j21020pq42e.jpg)

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvwtt8s8j21000q0dh1.jpg)

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvxc8ngwj20zk0pgacc.jpg)

```
to setup
  ca
  create-turtles n_nodes [
    set shape "circle"
    set color 8
    set size 1
  ]

  layout-circle turtles (world-width / 2 - 2)


end

to link_1
  ask turtles [
    create-links-with other turtles
  ]
end

to link_2
  ask turtles [
    create-links-with other turtles
    ]

  while [count links > n_links ] [
    ask one-of links [die]
  ]
end

to link_3
  ;;ask turtle 0 [print distance turtle 2 ;;28.55]

  ask turtles [
    create-links-with other turtles with [distance myself > 28]
  ]


end
```

<br>

### 课后

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h0qvywjox5j20z30u0abr.jpg)

```
globals [last_node]

to setup
  ca
  ask patches [
    set pcolor white
  ]


  create-turtles 1 [
    set shape "circle"
    set last_node self
  ]

  repeat 10 [
    crt 1 [
      set shape "circle"
      setxy random-xcor random-ycor
      create-link-from last_node [tie]
      set last_node self
    ]
  ]

end
```

```
globals [last_node last_node_id]

to setup
  ca
  ask patches [
    set pcolor white
  ]


  create-turtles 1 [
    set shape "circle"
    set last_node self
  ]

  repeat 5 [
    crt 1 [
      set shape "circle"
      setxy random-xcor random-ycor
      ;create-link-from last_node [tie]
      ;set last_node self
      create-link-from turtle last_node_id
      set last_node_id who
    ]
  ]

end
```

<br>