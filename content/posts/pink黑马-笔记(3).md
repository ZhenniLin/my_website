---
title: "pink黑马-笔记(3)"
subtitle: ""
date: 2022-02-27T10:54:15+08:00
draft: false
author: ""
authorLink: ""
description: "主要内容是CSS-盒子模型"
keywords: ""
license: ""
comment: false
weight: 0

tags:
- CSS
categories:
- 前端

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

## 盒子模型



### 目标

- 盒子模型的四个组成部分
- 利用边框复合写法给元素添加边框
- 计算盒子的实际大小
- 利用盒子模型布局模块案例
- 盒子设置圆角边框
- 盒子添加阴影
- 文字添加阴影



### 目录

- 盒子模型
- PS基本操作
- 综合案例
- 圆角边框
- 盒子阴影
- 文字阴影



### 盒子模型

- 网页布局要学习三大核心 - 盒子模型，浮动和定位

**1.网页布局的本质**

- 网页布局过程
  - 先准备好相关的网页元素，网页元素基本都是盒子Box
  - 利用css设置好盒子样式，然后摆放到相应位置
  - 往盒子里面装内容
- 网页布局的本质 - 利用css摆盒子

**2.盒子模型box model组成**

- 就是把html页面中的布局元素看成是一个矩形的盒子，也就是一个盛装内容的容器
- css盒子模型本质上是一个盒子，封装周围的html元素，它包括：边框border、外边距margin、内边距padding、和实际内容content

**3.边框 border**

- border可以设置元素的边框，边框有三部分组成 - 边框宽度(粗细) 边框样式 边框颜色

`boder: border-width || border-style || border-color`

`border-style: solid/dashed/dotted`

- 边框属性允许你指定一个元素边框样式和颜色
- 边框简写 - `border: 1px solid red; 没有顺序`

- 边框分开写法 - `border-top: 1px solid red; /* 只设定上边框，其余同理 */`

```html

border: 1px solid blue;
/* 层叠性 只是层叠了上边框 */
border-top: 1px solid red;

```

**4.表格的细线边框**

```html

<style>
  
  table {
    width: 500px;
    height: 249px;
  }
  
  table,
  td {
    border: 1px solid pink;
    border-collapse: collapse;
  }
  
</style>

```

- border-collapse属性控制浏览器绘制表格边框的方式。它控制相邻单元格的边框 - 合并相邻的边框

**5.边框会影响盒子实际大小**

边框会额外增加盒子的实际大小，两种方案解决

- 测量盒子大小的时候不量边框
- 如果测量的时候包含了边框，则需要width/height减去边框宽度

**6.内边距 padding**

- padding属于设置内边距，即边框与内容之间的距离

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 180px;
            height: 180px;
            background: pink;
            border: 10px solid red;
            padding-left: 20px;
            padding-top: 30px;
        }
    </style>
</head>
<body>
    <div>内容content</div>
</body>
</html>

/*
padding-left 左内间距
padding-right 右内间距
padding-top 上内间距
padding-bottom 下内边距
*/

```

- padding属性（简写属性）可以有四个值

```html

/*
padding: 5px;  - 1个值，代表上下左右都5px内边距
padding: 5px 10px; - 2个值，代表上下内边距是5像素，左右内边距是10像素
padding: 5px 10px 20px; - 3个值，代表上内边距5px，左右内边距10px，下内边距20px
padding: 5px 10px 20px 30px; - 4个值，顺时针代表内间距
*/

```

- 当我们给盒子指定padding值后 - 内容和边框有了距离，添加了内边距 / padding影响了盒子实际大小
- 解决方法：保证盒子跟效果图大小保持一致，则让width/height减去多出来的内边距大小即可

- padding练习

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .nav {
            height: 41px;
            border-top: 3px solid #ff8500;
            border-bottom: 1px solid #edeef0;
            background-color: #fcfcfc;
            line-height: 41px; /* 能够使div中文字对齐居中 */
        }

        .nav a {
            /* a属于行内元素 此时必要转换 行内块元素 */
            display: inline-block;
            height: 41px;
            padding: 0 20px;
            font-size: 12px;
            color: #4c4c4c;
            text-decoration: none; /* 链接下划线没有 */
        }

        .nav a:hover {
            background-color: #eee;
        }

    </style>
</head>
<body>
    <div class="nav">
        <a href="#">新浪导航</a>
        <a href="#">手机新浪网</a>
        <a href="#">移动客户端</a>
        <a href="#">微博</a>
        <a href="#">三个字</a>
    </div>
</body>
</html>

```

**7.外边距 margin**

margin属性用于设置外边距，即控制盒子和盒子之间的距离

```html

/*
margin-left  - 左外边距
margin-right - 右外边距
margin-top   - 上外边距
margin-bottom - 下外边距
*/

```

外边距典型应用

- 可以让块级盒子水平居中，满足条件 - 盒子必须指定宽度width
- 盒子左右的外边距都设置为auto

`.header {width: 960px; margin: 0 auto; }`

​	常见写法

- margin-left: auto;
- margin-right: auto;
- margin: auto;
- margin: 0 auto; (常用这个)

注意：以上方法是让块级元素水平居中，行内元素或者行内块元素水平居中给其父元素添加text-align: center即可

**8.外边距合并**

使用margin定义块元素的垂直外边距时，可能会出现外边距的合并

- 相邻元素垂直外边距的合并 - 当上下相连的两个块元素相遇时，如果上边的元素有下外边距margin-bottom，下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和。<u>取两个值中的较大者这种现象被称为相邻块元素垂直外边距的合并</u>
  - 解决方法 - 尽量只给一个盒子添加margin值
- 嵌套块元素垂直外边距 - 对于两个嵌套关系的块元素，外元素上有外边距同时内元素上也有外边距，此时外元素会塌陷较大的外边距值
  - 解决方案 - 为外元素定义上边框 / 为外元素定义内边距 / <u>可以为父元素添加overflow: hidden</u> / 还有其他方法，比如浮动、固定，绝对定位的盒子不会有塌陷问题，后面咱们再总结

**9.清除内外边距**

网页元素很多都带有默认的内外边距，而且不同浏览器默认的也不一致。因此我们在布局前，首先要清楚下网页元素的内外边距

```html

<style>
  /* 这句话也是我们CSS的第一行代码 */
  * {
    margin: 0; /* 清楚内边距 */
    padding: 0; /* 清楚外边距 */
  }
</style>

```

- 注意：行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距。但是转换为块级和行内块元素即可


### PS基本操作

因为网页美工大部分效果都是利用PS（photoshop）来做的，所以以后我们大部分切图工作都是在PS里面完成

- 文件-打开: 可以打开我们要测量的图片
- Ctrl+R: 可以打开标尺，或者 视图 - 标尺
- 右击标尺，把里面的单位改为像素
- Ctrl+ 加号(+) 可以放大视图，Ctrl+ 减号(-)可以缩小试图
- 用选取拖动测量大小


### 综合案例

**案例-产品模块**

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>综合案例-产品模块</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #f5f5f5;
        }

        a {
            color: #333;
            text-decoration: none;
        }

        .box {
            width: 298px;
            height: 415px;
            background-color: #fff;
            /* 让块级盒子水平居中对齐 */
            margin: 100px auto;
        }

        .box img {
            /* 宽度与外元素百分之百宽 */
            width: 100%;
            height: 50%;
        }

        .review {
            height: 70px;
            font-size: 14px;
            /* 这个段落没有width属性，所以padding不会撑开盒子的宽度 */
            padding: 0 28px;
            margin-top: 30px;
        }

        .appraise {
            font-size: 12px;
            color: #b0b0b0;
            margin-top: 20px;
            padding: 0 20px;
        }

        .info {
            font-size: 14px;
            margin-top: 15px;
            padding: 0 20px;
        }

        .info h4 {
            font-weight: 400;
            display: inline-block;
        }

        .info span {
            color: #ff6700;
        }

        .info em {
            font-style: normal;
            color: #ebe4e0;
            margin: 0 6px 0 15px;
        }


    </style>
</head>
<body>
   <div class="box">
       <img src="https://s2.loli.net/2022/02/10/Y5AvxDSFw4o8TJb.jpg" alt="photo">
       <p class="review">巴洛克时期画家作品</p>
       <div class="appraise">来自于xx美术馆的评价</div>
       <div class="info">
            <h4><a href="#">XX画家作品</a></h4>
            <em>|</em>
            <span>XX国家</span>
        </div>
   </div>
</body>
</html>


```

**案例-快报模块头部制作**

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>综合案例-快报模块头部制作</title>
    <style>
       * {
           margin: 0;
           padding: 0;
       }

          /* 新知识点-去掉li前面的项目符号（小圆点）
          语法：list-style: none;  */
       li {
           list-style: none;
       }   

       .box {
           width: 248px;
           height: 163px;
           border: 1px solid #ccc;
           margin: 100px auto;
       }

       .box h3 {
           height: 32px;
           border-bottom: 1px dotted #ccc;
           font-size: 14px;
           font-weight: 400;
           /* 垂直居中 */
           line-height: 32px;
           /* h3没有宽度属性所以不会撑开 */
           padding-left: 15px;
       }

       .box ul li a {
           font-size: 12px;
           color: #666;
           text-decoration: none;
       }

       .box ul li a:hover {
           text-decoration: underline;
       }

       .box ul li {
           height: 23px;
           line-height: 23px;
           padding-left: 20px;
       }

       .box ul {
           margin-top: 7px;
       }



    </style>
</head>
<body>
    <div class="box">
        <h3>品优购快报</h3>
        <ul>
            <li><a href="#">特惠1</a></li>
            <li><a href="#">特惠2</a></li>
            <li><a href="#">特惠3</a></li>
            <li><a href="#">特惠4</a></li>
            <li><a href="#">特惠5</a></li>
        </ul>
    </div>
</body>
</html>

```

### 圆角边框

border-radius属性用于设置元素的外边框圆角

语法：

`border-radius: length;`

radius半径(圆的半径)原理: (椭)圆与边框的交集形成圆角效果 - 半径越大弧度越明显

- 参数值可以为数值或百分比形式
- 如果是正方形，想要设置为一个圆，把数值修改为高度或者宽度的一半即可，或者直接为50%
- 如果是一个矩形，设置高度的一半就可以做u形槽
- 该属性是一个简写属性，可以跟四个值，分别代表左上角、右上角、右下角、左下角
- 分开写：border-top-left-radius、border-top-right-radius、border-bottom-right-radius和border- bottom-left-radius

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .yuanxing {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* 设置高度宽度的一半 等价于 50%  */
            border-radius: 100px;
        }

        .jvxing {
            width: 300px;
            height: 100px;
            background-color: pink;
            /* 设置高度的一半 */
            border-radius: 50px;
        }

        .radius {
            width: 200px;
            height: 200px;
            border-radius: 10px 20px 30px 40px;
            /* 两个值 - 对角线关系 */
            background-color: pink;
        }
    </style>
</head>
<body>
    1.圆形的做法
    <div class="yuanxing"></div>
    2.矩形的做法
    <div class="jvxing"></div>
    3.设置不同的圆角
    <div class="radius"></div>
</body>
</html>

```

### 盒子阴影

CSS中新增了盒子阴影，可以用box-shadow属性为盒子添加阴影

语法：

`box-shadow: h-shadow v-shadow blur spread color inset;`

```html

/* 

h-shadow 必需 水平阴影的位置 允许负值
v-shadow 必需 垂直阴影的位置 允许负值
blur 		 可选 模糊距离
spread	 可选 阴影的尺寸
color		 可选 阴影的颜色
inset		 可选 将外部阴影outset改为内部阴影 

*/

```

- 默认的是外阴影outset，但是不可以写这个单词，否则导致阴影无效
- 盒子阴影不占用空间，不会影响其他盒子排列

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin: 100px auto;
            /* box-shadow: 10px 10px 10px 10px rgba(0, 0, 0, 0.3); */
        }

        /* 原先盒子没有影子，但鼠标经过出现影子效果 */
        div:hover {
            box-shadow: 10px 10px 10px -4px rgba(0, 0, 0, 0.3);
        }
    </style>
</head>
<body>
    <div></div>
</body>
</html>

```



### 文字阴影

在CSS3中，我们可以使用text- shadow属性将阴影应用于文本

`text-shadow: h-shadow v-shadow blur color;`

```html

/* 

h-shadow 必需 水平阴影的位置 允许负值
v-shadow 必需 垂直阴影的位置 允许负值
blur 		 可选 模糊距离
color		 可选 阴影的颜色

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
        div {
            font-size: 50px;
            color: pink;
            font-weight: 700;
            text-shadow: 5px 5px 6px rgba(0, 0, 0, .3);
        }
    </style>
</head>
<body>
    <div>文字阴影</div>
</body>
</html>

```

