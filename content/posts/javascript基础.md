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

- 变量指的是在程序中**保存数据的一个容器**
- 变量是计算机内存中**存储数据的标识符**，根据变量名称可以获取到内存中存储的数据
- 也就是说，我们向内存中存储了一个数据，然后要给这个数据起一个名字，为了是我们以后再次找到他
- 语法： `var 变量名 = 值`

### 定义变量及赋值

```javascript
//定义一个变量
var num;

// 给一个变量赋值
num = 100;

// 定义一个变量的同时给其赋值
var num2 = 200;
```

- 一个变量名只能存储一个值
- 当再次给一个变量赋值的时候，前面一次的值就没有了
- 变量名称区分大小写（`JS`  严格区分大小写）

### 变量的命名规则

- 规则： 必须遵守的，不遵守就是错

  - 一个变量名称可以由 **数字、字母、英文下划线\_ 、美元符号($)** 组成
  - 严格区分大小写
  - 不能由数字开头
  - 不能是 **保留字** 或 **关键字**
  - 不要出现空格

- 规范：建议遵守的（开发者默认），不遵守不会报错
  - 变量名尽量有意义 (语义化)
  - 遵循驼峰命名规则，由多个单词组成的时候，从第二个单词开始首字母大写
  - 不要使用中文

</br>

## 3. 数据类型 (重点)

- 是指我们存储在内存中的数据的类型
- 我们通常分为两大类  **基本数据类型**  和  **复杂数据类型**

### 基本数据类型

1.  数值类型（number）
    - 一切数字都是数值类型（包括二进制，十进制，十六进制等）
    - `NaN`（not a number），一个非数字
2.  字符串类型（string）
    - 被引号包裹的所有内容（可以是单引号也可以是双引号）
3.  布尔类型（boolean）
    - 只有两个（`true`  或者  `false`）
4.  null 类型（null）
    - 只有一个，就是  `null`，表示空的意思
5.  undefined 类型（undefined）
    - 只有一个，就是  `undefined`，表示没有值的意思

### 判断数据类型

- 既然已经把数据分开了类型，那么我们就要知道我们存储的数据是一个什么类型的数据
- 使用  `typeof`  关键字来进行判断

```javascript
// 第一种使用方式

var n1 = 100;
console.log(typeof n1);

// 第二种使用方式
var s1 = "abcdefg";
console.log(typeof s1);
```

### 数据类型转换

- 数据类型之间的转换，比如数字转成字符串，字符串转成布尔，布尔转成数字等

## 其他数据类型转成数值

1.  `Number(变量)`

    > 可以把一个变量强制转换成数值类型
    >
    > 可以转换小数，会保留小数
    >
    > 遇到不可转换的都会返回  `NaN`
    >
    > true 会转为 1 / false 转为 0
    >
    > null 是对象 会转成 0
    >
    > undefined 会转为 NaN

```javascript
var a = "100"; //100 abc->NaN

var b = Number(a);

console.log(a, b);
```

2.  `parseInt(变量)`

    > 从第一位开始检查，是数字就转换，知道一个不是数字的内容
    >
    > 开头就不是数字，那么直接返回  `NaN`
    >
    > 不认识小数点，只能保留整数

```javascript
var a = "123abc"; //

var b = parseInt(a); //123

console.log(a, b);
```

3.  `parseFloat(变量)`

    > 从第一位开始检查，是数字就转换，知道一个不是数字的内容
    >
    > 开头就不是数字，那么直接返回  `NaN`
    >
    > 认识一次小数点

```javascript
var a = "123.45abc"; //

var b = parseInt(a); //123.45

console.log(a, b);
```

4.  除了加法以外的数学运算

    > 运算符两边都是可运算数字才行
    >
    > 如果运算符任何一遍不是一个可运算数字，那么就会返回  `NaN`
    >
    > 加法不可以用

```javascript
var a = "100"; //

var b = a - 0; //1000

console.log(a, b);
```

#### 其他数据类型转成字符串

1.  `变量.toString()`

    > 有一些数据类型不能使用  `toString()`  方法，比如  `undefined`  和  `null`

```javascript
var a = 100; //

var b = a.toString; //

console.log(a, b);
```

2.  `String(变量)`

    > 所有数据类型都可以
    >
    > null / undefined 都会变成字符串的 'null' 'undefined'

```javascript
var a = 100; //

var b = String(a); //

console.log(a, b);
```

3.  使用加法运算

    > 在 JS 里面，`+`  由两个含义
    >
    > 字符串拼接： 只要  `+`  任意一边是字符串，就会进行字符串拼接
    >
    > 加法运算：只有  `+`  两边都是数字的时候，才会进行数学运算

```javascript
var a = 100; //

var b = a + ""; //'100'

console.log(a, b);
```

#### 其他数据类型转成布尔

1.  `Boolean(变量)`

    > 在 js 中，只有  `''`、`0`、`null`、`undefined`、`NaN`，这些是  `false`
    >
    > 其余都是  `true`

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
