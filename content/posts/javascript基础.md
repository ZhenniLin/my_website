---
title: " JavaScript基础"
subtitle: ""
date: 2023-04-09
draft: false
author: ""
authorLink: ""
description: "basic"
keywords: ""
license: ""
comment: false
weight: 0

tags:
  - javascript
categories:
  - javascript

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

## 1. JS 简史、书写和注释

### Javascript 发展历史

```

1. 1994年，网景公司(Netscape)发布了Navigator浏览器0.9版，这是世界上第一款比较成熟的网络浏览器，轰动一时。但是这是一款名副其实的浏览器--只能浏览页面，浏览器无法与用户互动,当时解决这个问题有两个办法，一个是采用现有的语言,许它们直接嵌入网页。另一个是发明一种全新的语言。
liveScript ==> javaScript ==> ECMAscript

1995年Sun公司将Oak语言改名为Java，正式向市场推出。Sun公司大肆宣传，许诺这种语言可以"一次编写，到处运 行"(Write Once, Run Anywhere)，它看上去很可能成为未来的主宰。 网景公司动了心，决定与Sun公司结成联盟 34岁的系统程序员Brendan Eich登场了。1995年4月，网景公司录用了他,他只用10天时间就把Javascript设计出来了。

(1)借鉴C语言的基本语法
(2)借鉴Java语言的数据类型和内存管理
(3)借鉴Scheme语言，将函数提升到"第一等公民"(first class)的地位
(4)借鉴Self语言，使用基于原型(prototype)的继承机制
```

### Javascript 能干什么

```
1. 常见的网页效果【表单验证，轮播图。。。】
2. 与H5配合实现游戏【水果忍者： http://www.jq22.com/demo/html5-fruit-ninja/】
3. 实现应用级别的程序【http://naotu.baidu.com】
4. 实现图表统计效果【https://echarts.apache.org/examples/zh/】
5. js可以实现人工智能【面部识别】
6. 后端开发，app开发，桌面端开发......
```

### Javascript 代码的书写位置

- 和 `css` 一样，`js` 也可以有很多种方式书写在页面上让其生效
- `js` 也有多种书写方式，分为**行内式**、**内嵌式**、**外链式**

#### 行内式 JS 代码 (不推荐)

- 写在标签上的 js 代码需要依靠事件 (行为) 来出发

```javascript

<!-- 写在 a 标签的 href 属性上 -->
<a href="javascript:alert('我是一个弹出层');">点击一下试试</a>

<!-- 写在其他元素上 -->
<div onclick="alert('我是一个弹出层')">点一下试试看</div>

<!-- 注：onclick 是一个事件（点击事件），当点击元素的时候执行后面的 js 代码 -->

```

#### 内嵌式 JS 代码

- 内嵌式的 js 代码会在页面打开的时候直接触发

```javascript

<!-- 在 html 页面书写一个 script 标签，标签内部书写 js 代码 -->

<script type="text/javascript"> alert('我是一个弹出层') </script>

<!-- 注：script 标签可以放在 head 里面也可以放在 body 里面 -->


```

#### 外链式 JS 代码 (推荐)

- 外链式 js 代码只要引入了 html 页面，就会在页面打开的时候直接触发
- 新建一个  `.js`  后缀的文件，在文件内书写  `js`  代码，把写好的  `js`  文件引入  `html`  页面

```javascript
// 我是 index.js 文件
alert("我是一个弹出层");
```

```javascript
<!-- 我是一个 html 文件 -->
<!-- 通过 script 标签的 src 属性，把写好的 js 文件引入页面 -->

<script src="index.js"></script>

<!-- 一个页面可以引入多个 js 文件 -->

<script src="index1.js"></script>
<script src="index2.js"></script>
<script src="index3.js"></script>

```

### JS 中的注释

- 学习一个语言，先学习一个语言的注释，因为注释是给我们自己看的，也是给开发人员看的
- 写好一个注释，有利于我们以后阅读代码

#### 单行注释

- 一般就是用来描述下面一行代码的作用
- 可以直接写两个  `/` ，也可以按  `ctrl + /`

```javascript
// 我是一个单行注释
// 下面代码表示在浏览器里面出现一个弹出层
alert("我是一个弹出层");
```

#### 多行注释

- 一般用来写一大段话，或者注释一段代码
- 可以直接写  `/**/`  然后在两个星号中间写注释
  - 各个编辑器的快捷键不一样，`vscode`  是  `alt + shift + a`

```javascript
/* 我是一个多行注释 */

/* 注释的代码不会执行
alert('我是一个弹出层')
alert('我是一个弹出层')
*/

alert("我是一个弹出层");
```

</br>

## 2. 变量

</br>

## 3. 数据类型 (重点)

</br>

## 4. 运算符

</br>

## 5. 分支结构 (重点)

</br>

## 6. 循环结构 (重点)

</br>

## 7. 函数的概念

</br>

## 8. 对象

</br>

## 9. 数组

</br>

## 10. 字符串

</br>

## 11. Math

</br>

## 12. Date

</br>

## 13. 定时器

</br>
```
