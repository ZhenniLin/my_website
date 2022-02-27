---
title: "前端 | pink黑马-笔记(4)"
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
- CSS
categories:
- 有求必应屋

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

## CSS 浮动



### 目标

- 为什么需要浮动
- 浮动的排列特性
- 3种最常见的布局方式
- 为什么需要清除浮动
- 2种清除浮动的方法
- 利用photoshop实现基本的切图
- 利用photoshop插件实现切图
- 完成学成在线的页面布局



### 目录

- 浮动
- 常见网页布局
- 清楚浮动
- PS 切图
- 学成在线案例



### 浮动

**1.传统网页布局的三种方式**

网页布局的本质——用CSS来摆放盒子，把盒子摆放到相应位置

CSS提供了三种传统布局方式 (简单说，就是盒子如何进行排列顺序)：

- 普通流 - 标准流
- 浮动
- 定位

**2.标准流（普通流/文档流）**

标签按照规定好默认方式进行排列

- 块级元素会独占一行，从上向下排列 - 常用元素div hr p h1-h6 ul ol dl form table
- 行内元素会按照顺序，从左到右顺序排列，碰到父元素边缘自动换行 - span a i em

以上都是标准流布局，前面学习的就是标准流，标准流就是最基本的布局方式

这三种布局方式都是用来摆放盒子的，盒子摆放到合适位置，布局自然就完成了

- 实际开发中，一个页面基本包含了这三种布局方式

**3.为什么需要浮动？**

总结：有很多的布局效果，标准流没办法完成，此时就可以利用浮动完成布局。因为浮动可以改变元素标签默认的排列方式

浮动最典型的应用：可以让多个块级元素一行内排列显示

网页布局第一准则：多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动

**4.什么是浮动？**

float 属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含块或另一个浮动框的边缘

语法：

`选择器 {float: 属性值; }`

```html

/* 

none 元素不浮动(默认值)
left 元素向左浮动
right 元素向右浮动

*/

```

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .left,
        .right {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .right {
            float: right;
        }
    </style>
</head>
<body>
    <div class="left">试验1</div>
    <div class="right">试验2</div>
</body>
</html>

```

**5.浮动特性（重难点）**

加了浮动之后的元素，会具有很多特性，需要我们掌握

- 浮动元素会脱离标准流
  - 脱离标准流的控制(浮)移动到指定位置(动)，俗称脱标 - 设置了浮动的元素，漂浮在普通流的上面，不占位置，脱标
  - 浮动的盒子不再保留原先的位置
- 浮动的元素会一行内显示并且元素顶部对齐 
  - 如果多个盒子都设置了浮动
  - 浮动的元素是相互贴靠在一起的（不会有缝隙），如果父级宽度装不下这些浮动的盒子，多出的盒子会另起一行对齐
- 浮动的元素会具有行内块元素的特性
  - 任何元素都可以浮动，不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性
  - 如果块级盒子没有设置宽度，默认宽度和父级一样宽，但是添加浮动后，它的大小根据内容来决定

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div,
        span {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }
        /* 如果行内元素有了浮动，则不需要转换块级/行内块元素 就可以直接给高度和宽度 */

        p {
            /* 因为没有给p设置宽度，就看里边的内容，内容多宽，盒子就有多宽（行内块元素特点） */
            float: right;
            height: 200px;
            background-color: purple;
        }
    </style>
</head>
<body>
    <span>1</span>
    <span>2</span> 
    <div>div</div>
    <p>p</p>
</body>
</html>

```

**6.浮动元素经常和标准流父级搭配使用**

为了约束浮动元素位置，我们网页布局一般采取的策略是：

先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置，符合网页布局第一准则

案例1：小米布局案例

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
       .box {
           width: 1200px;
           height: 460px;
           /* 盒子在页面居中 */
           margin: 0 auto; 
       }

       .left {
           float: left;
           width: 230px;
           height: 460px;
           background-color: purple;
       }
       
       .right {
           float: left;
           width: 970px;
           height: 460px;
           background-color: skyblue;
       }
    
    </style>
</head>
<body>
    <div class="box">
        <div class="left">左侧</div>
        <div class="right">右侧</div>
    </div>
</body>
</html>

```

案例2: 小米布局案例

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 清除内外边距 */
       * {
           margin: 0;
           padding: 0;
       }

       /* 清除li的小圆点 */
       li {
           list-style: none;
       }

       .box {
           width: 1226px;
           height: 285px;
           background-color: pink;
           margin: 0 auto;
       }

       .box li {
           float: left;
           margin-right: 14px;
           width: 296px;
           height: 285px;
           background-color: purple;
       }

       /* 必需这样写 - 注意提权 - 权重 */
       .box .last {
           margin-right: 0;
       }
    
    </style>
</head>
<body>
    <!-- ul 和 li 有默认内外边距 -->
    <ul class="box">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li class="last">4</li>
    </ul>
</body>
</html>

```

案例3 - 小米布局案例

网页布局第二准则：先设置盒子大小，之后设置盒子位置

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
       .box {
           width: 1226px;
           height: 615px;
           background-color: pink;
       }

       .left {
           float: left;
           height: 615px;
           width: 234px;
           background-color: purple;
       }

       .right {
           float: left;
           height: 615px;
           width: 992px;
           background-color: skyblue;
       }

       .right>div {
           float: left;
           width: 234px;
           height: 300px;
           background-color: pink;
           margin-left: 14px;
           margin-bottom: 14px;
       }
    </style>
</head>
<body>
    <div class="box">
        <div class="left">左侧</div>
        <div class="right">
            <div>1</div>
            <div>2</div>
            <div>3</div>
            <div>4</div>
            <div>5</div>
            <div>6</div>
            <div>7</div>
            <div>8</div>
        </div>
    </div>
</body>
</html>

```



