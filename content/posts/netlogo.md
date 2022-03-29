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

## Programming guide 前提须知

<br>

### Agents

1.四类agents：**turtles**, **patches**, **links**, and the **observer**.

- Turtles are agents that move around in the world
- Each patch is a square piece of “ground” over which turtles can move
- Links are agents that connect two turtles
- The observer doesn’t have a location – you can imagine it as looking out over the world of turtles and patches / The observer doesn’t observe passively – **it gives instructions to the other agents**.

2.patches

- The patch at coordinates (0, 0) is called the origin and the coordinates of the other patches are the horizontal and vertical distances from this one
- patch’s coordinates [`pxcor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#pcor) and [`pycor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#pcor) - 能够衡量坐标

- patches的总量由the settings [`min-pxcor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#min-pcor), [`max-pxcor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#max-pcor), [`min-pycor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#min-pcor) and [`max-pycor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#max-pcor) 所决定

3.turtles 

- Turtles have coordinates too: [`xcor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#xcor) and [`ycor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ycor).
- A patch’s coordinates are always integers, but <u>a turtle’s coordinates can have decimals</u>. - 意味着可以被定位在patches中的任何一个point，而不是center of patches

4.links

- 没有坐标
- Every link has two ends, and each end is a turtle. 
- If either turtle dies, the link dies too. 
- A link is represented visually as a line connecting the two turtles.

<br>

### Procedure

1.**commands** and **reporters** tell agents what to do

- A <u>command</u> is an action for an agent to carry out, resulting in some effect. （verb）
- A <u>reporter</u> is instructions for computing a value, which the agent then “reports” to whoever asked it. （noun）

2.Commands and reporters built into NetLogo are called **primitives**

- [The NetLogo Dictionary](https://ccl.northwestern.edu/netlogo/docs/dictionary.html) has a complete list of <u>built-in</u> commands and reporters.

3.Commands and reporters you define yourself are called **procedures**

- Each procedure has a name, preceded by the keyword [`to`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#to) or [`to-report`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#to-report), depending on whether it is <u>a command procedure</u> or <u>a reporter procedure</u>
- The keyword [`end`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#end) marks the end of the commands in the procedure

4.Many commands and reporters take **inputs**

- values that the command or reporter uses in carrying out its actions or computing its result

```
to setup
  clear-all
  create-turtles 10
  reset-ticks
end

to go
  ask turtles [
    fd 1            ;; forward 1 step - 这个标志符号 “;” 表示注释comment
    rt random 10    ;; turn right
    lt random 10    ;; turn left
  ]
  tick
end

;; setup and go are user-defined commands.

;; clear-all, create-turtles, reset-ticks, ask, lt (“left turn”), rt (“right turn”) and tick, are all primitive commands

;;random and turtles are primitive reporters
;; - random takes a single number as an input and reports a random integer that is less than the input (in this case, between 0 and 9). 
;; - turtles reports the agentset consisting of all the turtles. (We’ll explain about agentsets later.)

```

- you may specify which agents – turtles, patches, or links – are to run each command，如果不specify，code就会由observer执行，在上面的代码里，the observer uses [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) to make the set of all turtles run the commands between the square brackets
- [`clear-all`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#clear-all) and [`create-turtles`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#create-turtles) can only be run by the observer

5.Procedure with inputs

- To create a procedure that accepts inputs, put their names in square brackets after the procedure name

```
to draw-polygon [num-sides len]  ;; turtle procedure
  pen-down
  repeat num-sides [
    fd len
    rt 360 / num-sides
  ]
end

```

- Elsewhere in the program, you might use the procedure by asking the turtles to each draw an octagon with a side length equal to its who number

```
ask turtles [ draw-polygon 8 who ]

```

6.Reporter procedures

- define your own reporters
- use [`to-report`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#to-report) instead of [`to`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#to) to begin your procedure
- in the body of the procedure, use [`report`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#report) to report the value you want to report

```
to-report absolute-value [number]
  ifelse number >= 0
    [ report number ]
    [ report (- number) ]
end

```

<br>

### Variables

1.Agent variables

- Agent variables are places to store values (such as numbers) in an agent

- can be a global variable, a turtle variable, a patch variable, or a link variable

  - If a variable is a global variable 全局变量, there is only one value for the variable, and every agent can access it
  - Each turtle has its *own* value for every turtle variable. The same goes for patches and links.

- Some variables are built into NetLogo

  - all turtles and links have a [`color`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#color) variable, and all patches have a [`pcolor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#pcolor) variable.
  - Other built-in turtle variables including [`xcor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#xcor), [`ycor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ycor), and [`heading`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#heading)
  - Other built-in patch variables include [`pxcor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#pcor) and [`pycor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#pcor). (There is a complete list [`here`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#builtinvariables).)

- define your own variables

  - make a global variable by adding a switch, slider, chooser, or input box to your model
  - by using the [`globals`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#globals) keyword at the beginning of your code, like this: `globals [score]`

- define new turtle, patch and link variables

  - using the [`turtles-own`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-own), [`patches-own`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#patches-own) and [`links-own`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#links-own) keywords, like this:

    ```
    turtles-own [energy speed]
    patches-own [friction]
    links-own [strength]
    ```

- Use the [`set`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#set) command to set them. (Any variable you don’t set has a starting value of zero.)

  `ask turtles [ set pcolor red ]` - 将turtles脚下的patches变成红色

- use “of ” - agent to read a different agent’s variable - 下一个例子可能更明显

  ```
  show [xcor + ycor] of turtle 5
  ;; prints the sum of the x and y coordinates of
  ;; turtle with who number 5
  
  show [xcor + ycor] of turtle 5
  ;; prints the sum of the x and y coordinates of
  ;; turtle with who number 5
  
  ```

2.Local variable - 局部变量

- A local variable is defined and used only in the context of a particular procedure or part of a procedure
- To create a local variable, use the [`let`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#let) command

```java
to swap-colors [turtle1 turtle2]
  let temp [color] of turtle1
  ask turtle1 [ set color [color] of turtle2 ]
  ask turtle2 [ set color temp ]
end
  
```

<br>

### Tick counter

1.In many NetLogo models, time passes in discrete steps, called **“ticks”**. NetLogo includes a **built-in tick counter** so you can keep track of how many ticks have passed

2.to retrieve the current value of the tick counter, use the [`ticks`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ticks) reporter.

- The [`tick`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#tick) command advances the tick counter by 1
- The [`clear-all`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#clear-all) command clears the tick counter along with everything else.
- Use the **reset-ticks command** when your model is done setting up, to start the tick counter. 当你的模型完成设置后, 使用reset-ticks命令来启动tick计数器

3.when to tick

- Use [`reset-ticks`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#reset-ticks) at the <u>end</u> of your setup procedure.
- Use [`tick`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#tick) at the <u>end</u> of your go procedure.

```
to setup
  clear-all
  create-turtles 10
  reset-ticks
end

to go
  ask turtles [ fd 1 ]
  tick
end

```

4.fractional ticks 

<br>

### Colors

1.Color primitive

​	(了解)

- the [`wrap-color`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#wrap-color) primitive.
- The [`scale-color`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#scale-color) primitive is useful for converting numeric data into colors.
- [`shade-of?`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#shade-of) will tell you if two colors are both “shades” of the same basic hue. For example, `shade-of? orange 27` is true, because 27 is a lighter shade of orange

2.RGB and RGBA Colors

- When using RGB colors the full range of colors is available to you. RGBA colors allow all the colors that RGB allows and you can also vary the transparency of a color
- You can set any color variables in NetLogo ([`color`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#color) for turtles and links and [`pcolor`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#pcolor) for patches) to an RGB list and that agent will be rendered appropriately
- Turtles, links, and labels can all contain RGBA lists as their color variables

```
;;examples
set pcolor [255 0 0]
set color [255 0 0 125]

```

- You can convert from a NetLogo color to RGB or HSB (hue/saturation/brightness) using [`extract-hsb`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#extract-hsb) and [`extract-rgb`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#extract-rgb). You can use [`rgb`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#rgb) to generate rgb lists and [`hsb`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#hsb) to convert from an HSB color to RGB.

3.Palette extension

4.Color Swatches dialog 

<br>

### Ask

1.NetLogo uses the [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) command to give commands to turtles, patches, and links

2.Because agentset members are always read in a random order, when [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) is used with an agentset each agent will take its turn in a random order

```
to setup
  clear-all
  create-turtles 100   ;; create 100 turtles with random headings
  ask turtles
    [ set color red    ;; turn them red
      fd 50 ]          ;; spread them around
  ask patches
    [ if pxcor > 0         ;; patches on the right side
        [ set pcolor green ] ]  ;; of the view turn green
  reset-ticks
end

```

3.Usually, the observer uses [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) to ask all turtles, all patches or all links to run commands. You can also use [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) to have <u>an individual turtle, patch or link</u> run commands

```
to setup
  clear-all
  crt 3                           ;; make 3 turtles
  ask turtle 0                    ;; tell the first one...
    [ fd 1 ]                      ;; ...to go forward
  ask turtle 1                    ;; tell the second one...
    [ set color green ]           ;; ...to become green
  ask turtle 2                    ;; tell the third one...
    [ rt 90 ]                     ;; ...to turn right
  ask patch 2 -2                  ;; ask the patch at (2,-2)
    [ set pcolor blue ]           ;; ...to become blue
  ask turtle 0                    ;; ask the first turtle
    [ ask patch-at 1 0            ;; ...to ask patch to the east
      [ set pcolor red ] ]        ;; ...to become red
  ask turtle 0                    ;; tell the first turtle...
    [ create-link-with turtle 1 ] ;; ...make a link with the second
  ask link 0 1                    ;; tell the link between turtle 0 and 1
    [ set color blue ]            ;; ...to become blue
  reset-ticks
end

```

4.Every turtle created has a <u>who number</u>     0 -> n

5.执行指令的顺序

```
;;first one turtle moves and turns red, 
;;then another turtle moves and turns red, and so on ask turtles
  [ fd 1
    set color red ]

;;first all the turtles move, then they all turn red.
ask turtles [ fd 1 ]
ask turtles [ set color red ]

```

<br>

### Agentsets

- An agentset is exactly what its name implies, <u>a set of agents</u>

- An agentset is not in any particular order. In fact, it’s always in a random order

- you can construct agentsets that contain only *some* turtles, *some* patches or *some* links / These agentsets can then be used by [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) or by various reporters that take agentsets as inputs.

- One way is to use [`turtles-here`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-here) or [`turtles-at`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-at), to make an agentset containing only the turtles on my patch, or only the turtles on some other patch at some x and y offsets. T

- here’s also [`turtles-on`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-on) so you can get the set of turtles standing on a given patch or set of patches, or the set of turtles standing on the same patch as a given turtle or set of turtles

  (more examples of how to make agentsets)

```
;; all other turtles:
other turtles

;; all other turtles on this patch:
other turtles-here

;; all red turtles:
turtles with [color = red]

;; all red turtles on my patch
turtles-here with [color = red]

;; patches on right side of view
patches with [pxcor > 0]

;; all turtles less than 3 patches away
turtles in-radius 3

;; the four patches to the east, north, west, and south
patches at-points [[1 0] [0 1] [-1 0] [0 -1]]

;; shorthand for those four patches
neighbors4

;; turtles in the first quadrant that are on a green patch
turtles with [(xcor > 0) and (ycor > 0)
              and (pcolor = green)]
              
;; turtles standing on my neighboring four patches
turtles-on neighbors4

;; all the links connected to turtle 0
[my-links] of turtle 0

```

- Once you have created an agentset, here are some simple things you can do

  - Use [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) to make the agents in the agentset do something
  - Use [`any?`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#any) to see if the agentset is empty
  - Use [`all?`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#all) to see if every agent in an agentset satisfies a condition.
  - Use [`count`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#count) to find out exactly how many agents are in the set

- here are some more complex things you can do

  - Pick a random agent from the set using [`one-of`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#one-of) 

    `ask one-of turtles [ set color green ]`

  - tell a randomly chosen patch to [`sprout`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sprout) a new turtle

    `ask one-of patches [ sprout 1 ]`

  - Use the [`max-one-of`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#max-one-of) or [`min-one-of`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#min-one-of) reporters to find out which agent is the most or least along some scale

    `ask max-one-of turtles [sum assets] [ die ]`

  - Use [`turtle-set`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtle-set), [`patch-set`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#patch-set) and [`link-set`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#link-set) reporters to make new agentsets by gathering together agents from a variety of possible sources.

  - Use [`no-turtles`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#no-turtles), [`no-patches`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#no-patches) and [`no-links`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#no-links) reporters to make empty agentsets.

  - Check whether two agentsets are equal using [`=`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#Symbols) or [`!=`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#Symbols).

  - Use [`member?`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#member) to see whether a particular agent is a member of an agentset.

1.Special agentsets

- The agentsets `turtles` and `links` have special behavior because they always hold the sets of *all* turtles and *all* links
- Assume the Code tab has `globals [g]`

```
observer> clear-all
observer> create-turtles 5
observer> set g turtles
observer> print count g
5
observer> create-turtles 5
observer> print count g
10
observer> set g turtle-set turtles
observer> print count g
10
observer> create-turtles 5
observer> print count g
10
observer> print count turtles
15

```

- The `turtles` agentset grows when new turtles are born, but other agentsets don’t grow. If I write `turtle-set turtles`, I get a new, normal agentset containing just the turtles that *currently* exist. New turtles don’t join when they’re born.

2.Agentsets and lists

- If you need your agents to do something in a fixed order, you need to make a list of the agents instead

<br>

### Breeds

```
breed [wolves wolf]
breed [sheep a-sheep]

```

- 注意单复数使用
- 叠加的顺序 - 覆盖型
- The following new primitives are also automatically available once you define a breed: [`create-sheep`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#create-turtles), [`hatch-sheep`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#hatch), [`sprout-sheep`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sprout), [`sheep-here`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-here), [`sheep-at`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-at), [`sheep-on`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-on), and [`is-a-sheep?`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#is-of-type).
- Also, you can use [`sheep-own`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#turtles-own) to define new turtle variables that only turtles of the given breed have. (It’s allowed for more than one breed to own the same variable.)
- Note also that turtles can change breeds. A wolf doesn’t have to remain a wolf its whole life. Let’s change a random wolf into a sheep: `ask one-of wolves [ set breed sheep ]`

- Who numbers are assigned irrespective of breeds. If you already have a frog 0, then the first mouse will be mouse 1, not mouse 0, since the who number 0 is already taken - who号码排序不论品种breed
- Quick example of using breeds 

```
breed [mice mouse]
breed [frogs frog]
mice-own [cheese]
to setup
  clear-all
  create-mice 50
    [ set color white
      set cheese random 10 ]
  create-frogs 50
    [ set color green ]
  reset-ticks
end

```

<br>

### Buttons

- Buttons in the interface tab provide an easy way to control the model.  - 运行buttons内代码
- Typically a model will have at least a “setup” button, to set up the initial state of the world, and a “go” button to make the model run continuously
- A button may be either a “once button”, or a “forever button”. 
- A forever button can also be stopped from code
- “action key”

1.buttons take turns

- More than one button can be pressed at a time. If this happens, the buttons “take turns”, which means that only one button runs at a time

- 例子1：用户按了 "setup"，然后在 "setup "重新弹出之前，立即按了 "go"。result: 在 "go "之前，"setup "就完成了。

- 例子2：当 "go "的按钮下降时，用户按了 "setup"。result："go "按钮完成了它当前的迭代, 然后 "setup "按钮运行。然后 "go "又开始运行。

- 例子#3：用户同时有两个forever buttons同时按下来。result：先是一个按钮全程运行其代码，然后另一个按钮全程运行其代码，如此交替进行。 

2.turtle, patch, and link forever buttons 

- difference - putting commands in a turtle, patch or link forever button / putting the same commands in an observer button that does `ask turtles`, `ask patches` or `ask links`
  - An “ask” doesn’t complete until all of the agents have finished running all of the commands in the “ask”. So the agents, as they all run the commands concurrently, can be out of sync with each other, but they all sync up again at the end of the ask
  - The same isn’t true of turtle, patch and link forever buttons. Since ask was not used, each turtle or patch runs the given code over and over again, so they can become (and remain) out of sync with each other

<br>

### Lists

- Each value in the list can be any type of value: a number, or a string, an agent or agentset, or even another list.

<br>

#### Constant lists

- `set mylist [2 4 6 8]` 
- the individual values are separated by spaces
- You can make lists that contain numbers and strings this way, as well as lists within lists, for example `[[2 4] [3 5]]`
- The empty list is written by putting nothing between the brackets, like this: `[]`

<br>

#### Building list on the fly 

- If you want to make a list in which the values are determined by reporters, as opposed to being a series of constants, use the [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list) reporter. The [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list) reporter accepts two other reporters, runs them, and reports the results as a list.

- a list to contain two random values - `set random-list list (random 10) (random 20)`

- using the [`n-values`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#n-values) reporter

- The [`of`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#of) primitive lets you construct a list from an agentset - It reports a list containing each agent’s value for the given reporter

  ```
  max [...] of turtles
  sum [...] of turtles
  ```

- You can combine two or more lists using the [`sentence`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sentence) reporter, which concatenates lists by combining their contents into a single, larger list. Like [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list), [`sentence`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sentence) normally takes two inputs, but can accept any number of inputs if the call is surrounded by parentheses.

<br>

#### Changing list items

- If you want the new list to replace the old list, use [`set`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#set).

  ```
  set mylist [2 7 5 Bob [3 0 -2]]
  ; mylist is now [2 7 5 Bob [3 0 -2]]
  set mylist replace-item 2 mylist 10 
  ; mylist is now [2 7 10 Bob [3 0 -2]] / 2是指的序列数
  ```

- add an item - to the end of a list -  use the [`lput`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#lput) reporter

  ```
  set mylist lput 42 mylist
  ; mylist is now [2 7 10 Bob [3 0 -2] 42]
  ```

- But what if you changed your mind? -  The [`but-last`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#but-first-and-last) (`bl` for short) reporter reports all the list items but the last

  ```
  set mylist but-last mylist
  ; mylist is now [2 7 10 Bob [3 0 -2]]
  ```

- Get rid of item 0, the 2 at the begining of the list

  ```
  set mylist but-first mylist
  ; mylist is now [7 10 Bob [3 0 -2]]
  ```

- the [`replace-item`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#replace-item) reporter can be nested to change the list-within-a-list

  ```
  set mylist (replace-item 3 mylist
                    (replace-item 2 (item 3 mylist) 9))
  ; mylist is now [7 10 Bob [3 0 9]]
  ```

<br>

#### Iterating over lists

- If you want to do some operation on each item in a list in turn, the [`foreach`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#foreach) command and the [`map`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#map) reporter may be helpful.

  - [`foreach`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#foreach) is used to run a command or commands on each item in a list
  - 组成 - input list + a command name / block of commands
  - In the block, the variable `n` holds the current value from the input list - 可以自己命名

  ```
  foreach [1 2 3] show
  => 1
  => 2
  => 3
  foreach [2 4 6]
    [ n -> crt n
      show (word "created " n " turtles") ]
  => created 2 turtles
  => created 4 turtles
  => created 6 turtles
  ```

  ```
  foreach [1 2 3] [ steps -> ask turtles [ fd steps ] ]
  ;; turtles move forward 6 patches
  
  foreach [true false true true] [
  	should-move? -> ask turtles [ 
  		if should-move? [ fd 1 ] 
  	] 
  ]
  ;; turtles move forward 3 patches
  ```

  - [`map`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#map) is similar to [`foreach`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#foreach), but it is a reporter - It takes an input list and a reporter name or reporter block
  - 组成 - a command name / block of commands + input list 

  ```
  show map round [1.2 2.2 2.7]
  ;; prints [1 2 3]
  
  show map [ x -> x < 0 ] [1 -1 3 4 -2 -10]
  ;; prints [false true false false true true]
  
  show map [ x -> x * x ] [1 2 3]
  ;; prints [1 4 9]
  ```

- other primitives for processing whole lists

  -  [`filter`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#filter), [`reduce`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#reduce), and [`sort-by`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort-by)
  -  [`repeat`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#repeat) or [`while`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#while)

<br>

#### Varing number of inputs

- In these cases, in order to pass them a number of inputs other than their default,  the primitive and its inputs must be surrounded by parentheses

```
show list 1 2
=> [1 2]
show (list 1 2 3 4)
=> [1 2 3 4]
show (list)
=> []
```

- Note that each of these special primitives has a default number of inputs for which no parentheses are required
- The primitives which have this capability - [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list), [`word`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#word), [`sentence`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sentence), [`map`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#map), [`foreach`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#foreach), [`run`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#run), and [`runresult`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#run)

<br>

#### Lists of agents

- agentsets are always in random order - If you need your agents to do something in a fixed order, you need to make a list of the agents instead
- There are two primitives that help you do this, [`sort`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort) and [`sort-by`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort-by)
- If you use [`sort`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort) on an agentset of turtles, the result is a list of turtles sorted in ascending order by [`who`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#who) number
- If you use [`sort`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort) on an agentset of patches, the result is a list of patches sorted left-to-right, top-to-bottom
- If you need descending order instead, you can combine [`reverse`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#reverse) with [`sort`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort), for example `reverse sort turtles`.

- If you want your agents to be ordered by some other criterion than the standard ones [`sort`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort) uses, you’ll need to use [`sort-by`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sort-by) instead.

```
sort-by [ [a b] -> [size] of a < [size] of b ] turtles
;; This returns a list of turtles sorted in ascending order by their turtle variable size.
```

- There’s a common pattern to get a list of agents in a random order, using a combination of [`of`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#of) and [`self`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#self), in the rare case that you cannot just use [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask):

```
[self] of my-agentset
```
<br>

#### Asking a list of agents

- Once you have a list of agents, you might want to ask them each to do something. To do this, use the [`foreach`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#foreach) and [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) commands in combination, like this:
- Note that you can’t use [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) directly on a list of turtles. [`ask`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#ask) only works with agentsets and single agents.

```
foreach sort turtles [ the-turtle ->
  ask the-turtle [
    ...
  ]
]

;;This will ask each turtle in ascending order by who number
;;Substitute “patches” for “turtles” to ask patches in left-to-right, top-to-bottom order
```
<br>

#### Performance of lists

<br>

### Math

- All numbers in NetLogo are stored internally as double precision floating point numbers
- An “integer” in NetLogo is simply a number that happens to have no fractional part
- Integers are always printed by NetLogo without the trailing “.0”:

```
show 1.5 + 1.5
// -> result - observer: 3
// 如果出现浮点数，0.后的数字会被discard
```

- 如果涉及到小数的计算，不是所有的分数都可以精确表示，而且可能会出现四舍五入的情况

```
show 1 / 6 + 1 / 6 + 1 / 6 + 1 / 6 + 1 / 6 + 1 / 6
=> 0.9999999999999999
show 1 / 9 + 1 / 9 + 1 / 9 + 1 / 9 + 1 / 9 + 1 / 9 + 1 / 9 + 1 / 9 + 1 / 9
=> 1.0000000000000002
```

<br>

#### scientific notation

- Very large or very small floating point numbers are displayed by NetLogo using “scientific notation”

```
show 0.000000000001
=> 1.0E-12
show 50000000000000000000
=> 5.0E19
```

- Numbers in scientific notation are distinguished by the presence of the letter E (for “exponent”). It means “times ten to the power of”, so for example, 1.0E-12 means 1.0 times 10 to the -12 power

```
show 1.0 * 10 ^ -12
=> 1.0E-12
```

- When entering a number, the letter E may be either upper or lowercase. When printing a number, NetLogo always uses an uppercase E

```
show 4.5e20
=> 4.5E20
```

<br>

#### floating point accuracy 

- 由于NetLogo中的数字受到浮点数字在二进制中的表示方式的限制，您可能会得到略微不准确的答案

```
show 0.1 + 0.1 + 0.1
=> 0.30000000000000004
show cos 90
=> 6.123233995736766E-17
```

- 这是浮点运算的一个固有问题；它发生在所有使用浮点数字的编程语言中。如果你正在处理固定精度的数量，例如美元和美分，一个常见的技术是在内部只使用整数（美分），然后除以100，得到一个以美元为单位的结果，以便显示。
- 如果你必须使用浮点数，那么在某些情况下，你可能需要用一个能容忍轻微不精确的测试来代替直接的等价测试，如 if x = 1 [ ... ] ，例如 if abs (x - 1) < 0.0001 [ ... ] 。
- 另外，the precision primitive 对于为显示目的对数字进行四舍五入很方便。NetLogo显示器也会把它们显示的数字四舍五入到可配置的小数位数

<br>

### Random numbers

(未完成)

- The random numbers used by NetLogo are what is called “pseudo-random”. (This is typical in computer programming.) That means they appear random, but are in fact generated by a deterministic process. “Deterministic” means that you get the same results every time
- NetLogo’s random number generator can be started with a certain seed value, which must be an integer in the range -2147483648 to 2147483647
- Once the generator has been “seeded” with the [`random-seed`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#random-seed) command, it always generates the same sequence of random numbers from then on

```
random-seed 137
show random 100
show random 100
show random 100
```

- Sometimes when we make a new version of NetLogo the random number generator changes
- To create a number suitable for seeding the random number generator, use the [`new-seed`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#new-seed) reporter. [`new-seed`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#new-seed) creates a seed, evenly distributed over the space of possible seeds, based on the current date and time. It never reports the same seed twice in a row

<br>

### Turtle shapes

- A turtle’s shape is stored in its [`shape`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#shape) variable and can be set using the [`set`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#set) command.
- New turtles have a shape of “default”. The [`set-default-shape`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#set-default-shape) primitive is useful for changing the default turtle shape to a different shape, or having a different default turtle shape for each breed of turtle
- The [`shapes`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#shapes) primitive reports a list of currently available turtle shapes in the model

```
ask turtles [ set shape one-of shapes ]
;; to assign a random shape to a turtle
```

- Shapes Editor [section](https://ccl.northwestern.edu/netlogo/docs/shapes.html) 
- The thickness of the lines used to draw the vector shapes can be controlled by the [`__set-line-thickness`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#set-line-thickness) primitive.

<br>

### Plotting 

- Before you can plot, you need to create one or more plots in the Interface tab

<br>

#### Plotting points

- `plot` / `plotxy`
- With `plot` you need only specify the y value you want plotted. The x value will automatically be 0 for the first point you plot, 1 for the second, and so on
- `plot` command - `plot count turtles`

- If you need to specify both the x and y values of the point you want plotted, then use `plotxy` instead - `plotxy time count-turtles`

<br>

#### Plot commands

- Plot setup/update commands and pen setup/update commands are run when the either reset-ticks or setup-plots commands are run. If the stop command is run in the body of the plot setup commands then the pen setup commands will not run.
- Four commands that trigger plotting explained 
  - `setup-plots` executes commands for one plot at a time.
  - `update-plots` is very similar to `setup-plots`.
  - `tick` is exactly the same as `update-plots` except that the tick counter is incremented before the plot commands are executed
  - `reset-ticks` first resets the tick counter to 0, and then does the equivalent of `setup-plots` followed by `update-plots`

```
;;A typical model will use reset-ticks and tick
to setup
  clear-all
  ...
  reset-ticks
end

to go
  ...
  tick
end

```

- 不使用ticks但仍想进行绘图的模型将使用setup-plots和update-plots。在前面的代码中，用setup-plots update-plots代替reset-ticks，用update-plots代替tick

<br>

### Strings

- Most of the list primitives work on strings as well

```
but-first "string" => "tring"
but-last "string" => "strin"
empty? "" => true
empty? "string" => false
first "string" => "s"
item 2 "string" => "r"
last "string" => "g"
length "string" => 6
member? "s" "string" => true
member? "rin" "string" => true
member? "ron" "string" => false
position "s" "string" => 0
position "rin" "string" => 2
position "ron" "string" => false
remove "r" "string" => "sting"
remove "s" "strings" => "tring"
replace-item 3 "string" "o" => "strong"
reverse "string" => "gnirts"
```

- A few primitives are specific to strings

```
is-string? "string" => true
is-string? 37 => false
substring "string" 2 5 => "rin"
word "tur" "tle" => "turtle"
```

- Strings can be compared using the =, !=, <, >, <=, and >= operators
- f you need to embed a special character in a string, use the following escape sequences
  - `\n` = newline
  - `\t` = tab
  - `\"` = double quote
  - `\\` = backslash

<br>

### Output

- Output to the screen can also be later saved to a file using the [`export-output`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#export-cmds) command

- The basic commands for generating output to the screen in NetLogo are [`print`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#print), [`show`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#show), [`type`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#type), and [`write`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#write) - these commands send their output to the Command Center

  - [`print`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#print) is useful in most situations.
  - [`show`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#show) lets you see which agent is printing what.
  - [`type`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#type) lets you print several things on the same line.
  - [`write`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#write) lets you print values in a format which can be read back in using [`file-read`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#file-read).

- To send output there instead of the Command Center, use the [`output-print`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#output-cmds), [`output-show`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#output-cmds), [`output-type`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#output-cmds), and [`output-write`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#output-cmds) commands

  

### File I/O



### Movies



### Drawing 



### Topology



### Links



### Ask-Concurrent



### Tie



### Multiple source files



### Syntax



#### Color

- Keywords are green
- Constants are orange
- Comments are gray
- Primitive commands are blue
- Primitive reporters are purple
- Everything else is black


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