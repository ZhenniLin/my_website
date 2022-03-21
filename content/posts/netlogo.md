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



Mac 推荐使用 6.2.2 版本

需要用到的网站：

[NetLogo Home Page](https://ccl.northwestern.edu/netlogo/)

[NetLogo 6.2.2 User Manual](https://ccl.northwestern.edu/netlogo/docs/)

[Programming Guide](https://ccl.northwestern.edu/netlogo/docs/programming.html)

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

1.Constant lists

- `set mylist [2 4 6 8]` 
- the individual values are separated by spaces
- You can make lists that contain numbers and strings this way, as well as lists within lists, for example `[[2 4] [3 5]]`
- The empty list is written by putting nothing between the brackets, like this: `[]`

2.Building list on the fly 

- If you want to make a list in which the values are determined by reporters, as opposed to being a series of constants, use the [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list) reporter. The [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list) reporter accepts two other reporters, runs them, and reports the results as a list.

- a list to contain two random values - `set random-list list (random 10) (random 20)`

- using the [`n-values`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#n-values) reporter

- The [`of`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#of) primitive lets you construct a list from an agentset - It reports a list containing each agent’s value for the given reporter

  ```
  max [...] of turtles
  sum [...] of turtles
  ```

- You can combine two or more lists using the [`sentence`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sentence) reporter, which concatenates lists by combining their contents into a single, larger list. Like [`list`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#list), [`sentence`](https://ccl.northwestern.edu/netlogo/docs/dictionary.html#sentence) normally takes two inputs, but can accept any number of inputs if the call is surrounded by parentheses.

3.Changing list items

4.Iterating over lists

5.Varing number of inputs

6.Lists of agents

7.Asking a list of agents

8.Performance of lists

<br>



## class 01


<br>