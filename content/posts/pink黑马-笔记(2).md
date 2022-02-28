---
title: "pink黑马-笔记(2)"
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

## CSS 层叠样式表 一



### 目标

- 什么是CSS
- 使用CSS基础选择器
- 设置字体样式
- 设置文本样式
- CSS三种引入方式
- 使用Chrome调试工具调试样式



### 目录

- CSS简介
- CSS基础选择器
- CSS字体属性
- CSS文本属性
- CSS引入方式
- 综合案例
- Chrome调试工具



### CSS简介

- CSS主要使用场景就是美化与布局页面

1.HTML的局限性

- 只关注内容的语义

2.CSS-网页的美容师

- CSS是层叠样式表(Cascading Style Sheets)的简称
- 有时候也称为CSS样式表或级联样式表
- CSS也是一种标记语言
- CSS主要用于设置HTML页面中的文本内容(字体、大小、对其方式等)、图片的外形(宽高、边框样式、边距等)以及版面的布局和外观显示样式

- HTML主要做结构，显示元素内容
- CSS美化HTML，布局网页
- 由HTML专注做结构呈现，样式交给CSS，即两者分离

3.CSS语法规范

- CSS规则由两个主要部分构成：选择器以及一条或多条声明

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/02/lvROzIXLBwSx7Ar.jpg" alt="1.01" 
width="50%" height="50%">
</div>
{{</md>}}

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /*选择器 {样式}*/
        p {
            color: red;
            font-size: 12px; 
        }
    </style>
</head>
<body>
    <p>内容</p>
</body>
</html>

```

4.CSS代码风格

以下代码风格不是强制规范，而是符合实际开发书写方式

- 样式格式书写
  - 紧凑格式 `h3 {color: deeppink; font-size: 20px; }`
  - 展开格式 (推荐这一种)

```html

h3 {
	color: pink;
	font-size: 20px;
}

```

- 样式大小写风格 - 推荐小写
- 样式空格风格 
  - 属性值前面，冒号后面，保留一个空格
  - 选择器 (标签) 和大括号中间保留空格



### CSS 基础选择器

1.选择器的作用

- 选择器就是根据不同的需求把不同的标签选出来 

2.选择器的分类

- 选择器分为基础选择器和复合选择器两个大类 - 目前先讲基础选择器
- 基础选择器是由单个选择器组成
- 基础选择器又包括：标签选择器、类选择器、id选择器和通配符选择器

3.标签选择器

- 标签选择器（元素选择器）是指用HTML标签名称作为选择器，按标签名称分类，为页面中某一类标签指定统一的CSS样式

```css

标签名{
	属性1: 属性值1;
	属性2: 属性值2;
  属性3: 属性值3;
	....
}

```

- 作用：标签选择器可以把某一类标签全部选择出来，比如所有的 `<div>` 标签和所有的 `<span>` 标签
- 优点：能够快速为页面中同类型的标签统一设置样式
- 缺点：不能差异化设置

4.类选择器

- 如果想要差异化选择不同的标签，单独选一个或者某几个标签，可以使用类选择器

```css

.类名 {
  属性1: 属性值;
}

/*例如*/
.red {
  color: red;
}

------分割线 上边的css内容记住放在<style></style>里

/*另外一边body里要注意定义class*/
<div class="red">内容</dive>

```

- 注意不能用标签选择器的名字命名 - 选择自取名字

- 长名称或词组可以使用中横线为选择器命名
- 避免纯数字、中文命名，尽量使用英文字母表示
- 命名需要意义 
- 命名规范：见附件Web前端开发规范手册

```html

/*课堂练习*/

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .red {
            width: 100px;
            height: 100px;
            background-color: red;
        }

        .green {
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="red">红色</div>
    <div class="green">绿色</div>
    <div class="red">红色</div>
    
</body>
</html>

```

4.类选择器-多类名

- 可以给一个标签指定多个类名，从而达到更多的选择目的 - 这些类名都可以选出这个标签 / 简单理解就是一个标签有多个名字
- 多类名使用方式
  - 多类名之间必须用空格分开

`<div class ="red font20">content</div>`

- 多类名开发中使用场景
  - 可以把一些标签元素相同的样式（共同的部分）放到一个类里面
  - 这些标签都可以调用这个公共的类，然后再调用自己独有的类
  - 节省CSS代码，统一修改也非常方便

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            width: 150px;
            height: 150px;
        }

        .red {
            background-color: red;
        }

        .green {
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="box red">红色</div>
    <div class="box green">绿色</div>
    <div class="box red">红色</div>
</body>
</html>

```

5.id选择器

- id选择器可以为标有特定id的HTML元素指定特定的样式
- html元素以id属性来设置id选择器，CSS中id选择器以"#"来定义

```css

/*语法*/
#id名 {
  属性1: 属性值1;
}

/*例如*/
#nav {
  color: red;
}

```

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #pink {
            color: pink;
        }
    </style>
</head>
<body>
    <div id="pink">content</div>
</body>
</html>

```

- id选择器和类class选择器的区别
  - 类选择器能够被多次使用
  - id选择器只能使用一次
  - 类选择器在修改样式中用的最多，id选择器一般用于页面唯一性的元素上，经常和JavaScript搭配使用

6.通配符选择器

- 使用"*"定义，它表示选取页面中所有的元素(标签)

```css

/*语法*/
* {
  属性1: 属性值1;
}

/*例如*/
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            color: pink;
        }
        /* 这里把html body等等的标签都改为了红色 */
    </style>
</head>
<body>
    <div id="pink">content</div>
</body>
</html>

/* 通配符不需要调用，自动就给所有的元素使用样式 */
/* 特殊情况 */

* {
  margin: 0;
  padding: 0;
}

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/05/hXVrxnSLFlY3QPE.jpg" alt="1.02">
</div>
{{</md>}}





### CSS字体属性

1.font - family设置字体系列

- CSS Font (字体) 属性用于定义字体系列、大小、粗细和文字样式 (如斜体)

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        h2 {
            font-family: 'Microsoft Yahei';
        }
        p {
            font-family: 'Microsoft Yahei', Arial, Helvetica, sans-serif;
        }
    </style>
</head>
<body>
    <h2>content</h2>
    <p>content</p>
</body>
</html>

```

- 各种字体之间必须使用英文状态下的逗号隔开
- 一般情况下，如果有空格隔开的多个单词组成的字体，加引号

2.font - size 字号大小

```css

p {
  font-size: 20px;
}

```

- px(像素)大小是我们网页的常用单位
- 谷歌浏览器默认的文字大小为16px

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            font-size: 16px;
        }
        /* 标题标签比较特殊，需要单独指定文字大小 */
        h2 {
            font-size: 18px;
        }
    </style>
</head>
<body>
    <h2>content</h2>
    <p>content</p>
</body>
</html>

```

3.字体粗细

- 使用font-weight属性设置文本字体的粗细
- 实际开发中提倡数字

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .bold {
            /* 700 等价于 bold */
            font-weight: 700;
        }

        h2 {
            font-weight: 400;
            /* 等价font-weight: normal; */
        }
    </style>
</head>
<body>
    <h2>content</h2>
    <p class="bold">content</p>
</body>
</html>

```

4.文字样式

- CSS使用font-style属性设置文本的风格

```css

p {
  font-style: normal;  
}

```

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        em {
            font-style: normal;
        }
    </style>
</head>
<body>
    <h2>content</h2>
    <p class="bold">content</p>
    <em>content</em>
</body>
</html>

```

5.字体复合属性

- 字体属性可以把以上文字样式综合来写，更节约代码

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            /* 复合顺序 style weight size/height family */
            font: italic 700 16px 'Microsoft yahei'
        }
    </style>
</head>
<body>
    <h2>content</h2>
    <p class="bold">content</p>
    <em>content</em>
    <div>content</div>
</body>
</html>

```

- 使用font属性时，必须按上面语法格式中的顺序写，不能更换顺序，并且各个属性间以空格隔开
- 不需要设置的属性可以省略，但必须保留font-size和font-family属性，否则font属性将不起作用

6.文字属性总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/05/pNZjrFVC7deURBm.jpg" alt="1.03">
</div>
{{</md>}}





### CSS文本属性

- CSS text属性可定义文本的外观，比如文本的颜色、对其文本、文本缩进、行间距等

1.文本颜色

- color属性用于定义文本的颜色

```css

div{
  color: red;
}

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/05/94hrCiPLSacxuF1.jpg" alt="1.04">
</div>
{{</md>}}

- 日常开发中多用十六进制

2.对其文本

- text-align属性用于设置元素内文本内容的水平对其方式

```css

/* 本质是让盒子里的文字水平居中对其 */
h1 {
  text-align: center;
}

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/05/PFxdHeoaKDnR6uk.jpg" alt="1.05">
</div>
{{</md>}}


3.装饰文本

- text-decoration属性规定添加到文本的修饰，可以给文本添加下划线、删除线、上划线等

```css

div {
  text-decoration: underline;
}

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/05/b9MYREt3mBHaKoI.jpg" alt="1.06">
</div>
{{</md>}}


```css

/* 链接就没有下划线了 */
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        a {
            text-decoration: none;
        }
    </style>
</head>
<body>
    <a href="#">content</a>
</body>
</html>

```

4.文本缩进

- text-indent属性用来指定文本的第一行的缩减，通常是将段落的首行缩进

```css

div {
  text-indent: 10px;
}

```

```css

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        p {
            text-indent: 10px;
        }
    </style>
</head>
<body>
    <p>content</p>
</body>
</html>

```

- em是一个相对单位，就是当前元素(font-size)1个文字的大小，如果当前元素没有设置大小，则会按照父元素的1个文字大小

```css

p {
  text-indent: 20em;
}

```

5.行间距

- line-height属性用于设置行间的距离(行高)，可以控制文字行与行之间的距离

```css

/* 文本高度16px */
p {
  line-height: 26px;
}

```

- 行间距组成：上间距+文本高度+下间距

6.文本属性总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/05/l8tfnS2KiJbMmFO.jpg" alt="1.07" >
</div>
{{</md>}}

### CSS引入方式

1.CSS三种样式表

- 按照CSS样式书写的位置 (或者引入的方式)，CSS样式表可以分为三大类
- 行内样式表-行内式
  - 在元素标签内部的style属性中设定css，适合于修改简单样式
  - style其实就是标签的属性
  - 在双引号中间，写法要符合CSS规范
  - 可以控制当前的标签设置样式
  - 由于书写繁琐，并且没有体现出结构与样式相分离的思想，所以不推荐大量使用，只有对当前元素添加简单样式的时候，可以考虑使用

​		`<div style="color: red; font-size: 12px;">`

- 内部样式表-嵌入式
  - 位于html页面内部，将所有css代码抽取出来，单独放置在 `<style>` 标签中
  - 这个标签理论上可以放在html文档的任何地方，但一般会放在文档的`<head>` 标签中
  - 通过此种方式，可以放便控制当前整个页面中的元素样式设置 
  - 代码结构清晰，但是并没有实现结构与样式完全分离
- 外部样式表-链接式
  - 实际开发都是外部样式表，适合于样式比较多的情况 核心是：样式单独写到CSS文件中，之后把CSS文件引入到HTML页面中使用
  - 引入外部样式表分为两步：
    - 新建一个后缀名为.css的样式文件，把所有css代码都放入此文件中
    - 在html页面中，使用 `<link>` 标签引入这个文件 `<link rel="stylesheet" href="css文件路径">`
    - rel - 定义当前文档与被链接文档之间的关系，在这里需要指定为"stylesheet"，表示被链接的文档是一个样式表文件
    - href - 定义所链接外部样式表文件的URL，可以是相对路径，也可以是绝对路径

2.CSS引入方式总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/08/dpPyU1OVbaflx2q.jpg" alt="1.08" >
</div>
{{</md>}}


### Chrome调试工具

1.打开调试工具 F12 或者 右键检查

2.使用调试工具

- 左边是html元素结构，右边是css样式
- 如果点击元素，发现右侧没有样式引入，极有可能是类名或者样式引入错误
- 如果有样式，但是样式前面有黄色叹号提示，则是样式属性书写错误


## CSS 层叠样式表 二


### 目标

- 使用emmet语法
- 使用css复合选择器
- 写出伪类选择器的使用规范
- 元素有几种模式
- 元素显示模式的相互转换代码
- 写出背景图片的设置方式
- 计算css权重


### 目录

- emmet语法
- css复合选择器
- css元素显示模式
- css背景
- css三大特性
- css注释


### Emmet语法

- 前身是Zen coding，它使用缩写，来提高html/css的编写速度，Vscode内部已经集成该语法

1.快速生成html语法结构

- 生成多个标签 加上*就可以 比如div * 3 - 快速生成3个div
- ul>li - 快速生成
- div+p - 快速生成
- 如果生成带有类名或者id名字的，直接写 .demo 或者 #two tab键即可
- 如果生成的div类名是有顺序的 .demo$*5
- 如果想要在生成的标签内部写内容可以用{}表示 例如: div{content}*5 / div{$} *5

2.快速生成css样式语法

- 基本采取简写形式即可 - 首字母简写自动补充

3.快速格式化代码


### CSS复合选择器

- 在css中，可以根据选择器的类型把选择器分为基础选择器和复合选择器，复合选择器是建立在基础选择器之上，对基本选择器进行组合形成
- 复合选择器可以更准确、更高效的选择目标元素(标签)
- 复合选择器是由多个基础选择器，通过不同的方式组合而成

2.后代选择器（重要）

- 后代选择器又称为包含选择器，写法就是把外层标签写在前面，内层标签写在后面，中间用空格分隔，当标签发生嵌套时，内层标签就成为外层标签的后代

```html

<style>
  ol il {
    color: pink;
  }
  
  .nav li a {
    color: yellow;
  }
</style>

```

- 元素1和元素2之间空格隔开
- 最终选择的是元素2
- 元素1和元素2可以是任意选择器

3.子元素选择器（重要）

- 子元素选择器只能选择作为某元素的最近一级子元素

`元素1>元素2 {样式声明}`

- 上述语法表示选择元素1里面的所有直接子元素-元素2

`<div > p {样式声明} /* 选择div里面所有最近一级p标签元素 */>`

- 元素1和元素2中间用大于号隔开
- 元素1是父母级，元素2是子级，最终选择的是元素2

4.并集选择器（重要）

- 并集选择器可以选择多组标签，同时为他们定义相同的样式，通常用于集体声明

```css

<style>
	div,
  p {
    color: pink;
  }
</style>

```

- 并集选择器是各选择器通过英文逗号 ( , ) 连接而成，任何形式的选择器都可以作为并集选择器的一部分
- 竖着写，最后一个选择器不需要加逗号

5.伪类选择器

- 用于某些选择器添加特殊的效果，比如给链接添加特殊效果，或选择第1个，第n个元素
- 伪类选择器书写最大的特点是用冒号 ( : ) 表示，比如 :hover、:first-child
- 因为伪类选择器很多，比如有链接伪类、结构伪类，所以这里先给大家讲解常用的链接伪类选择器

```html

a:link /* 选择所有未被访问的链接 */
a:visited /* 选择所有已被访问的链接 */
a:hover /* 选择鼠标指针位于其上的链接 */
a:active /* 选择活动链接（鼠标按下未弹起的链接） */

```

- 链接伪类注意事项
  - 为了确保生效，请按照LVHA的顺序
  - 因为a链接在浏览器中具有默认样式，所以我们实际工作中都需要给链接单独指定样式
- 链接伪类选择器实际开发工作中的写法

```html

/* a是标签选择器 所有链接 */
a {
	color: pink;
}

/* :hover是链接伪类选择器 鼠标经过 */
a: hover {
	color: red; /* 鼠标经过的时候，由原来的灰色变成了红色 */
}

```

6.focuse 伪类选择器

- :focus 伪类选择器用于选取获得焦点的表单元素
- 焦点就是光标，一般情况 `<input>` 类表单元素才能获取，因此这个选择器也主要针对于表单元素

```html

input: focus {
	background-color: yellow;
	color: red;
}

```

7.复合选择器总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/08/NwUJLPQVaT6IdHD.jpg" alt="1.09" >
</div>
{{</md>}}

- 重要 - 后代选择器/并集选择器/链接伪类选择器



### CSS元素显示模式

1.什么是元素显示模式

- 作用：网页的标签非常多，在不同地方会用到不同类型的标签，了解他们的特点可以更好的布局我们的网页
- 元素显示模式就是元素（标签）以什么方式进行显示，比如 `<div>` 自己占一行，比如一行可以放多个 `<span>`
- html元素一般分为块元素和行内元素两种类型

2.快元素

- 常见的块元素有 `<h1>～<h6> <p> <div> <ul> <ol> <li>` 等，其中 `<div>` 标签是最典型的块元素
- 块级元素特点
  - 独占一行
  - 宽度、高度、内外边距都可以控制
  - 宽度默认是容器的100%
  - 是一个容器及盒子，里边可以放行内或者块级元素
- 注意
  - 文字类的元素内不能使用块级元素
  - `<p>` 标签主要用于存放文字，因此 `<p>` 里面不能放块级元素，特别是不能放`<div>` 
  - 同理，`<h1>～<h2>` 等都是文字类块级标签，里面也不能放其他块级元素

3.行内元素

- 常见的行内元素 `<a> <strong> <b> <em> <i> <del> <s> <ins> <u> <span>` 等，其中`<span>` 标签是最典型的行内元素。有的地方也将行内元素称为内联元素
- 行内元素特点
  - 相邻行内元素在一行上，一行可以显示多个
  - 宽、高直接设置是无效的
  - 默认宽度就是它本身内容的宽度
  - 行内元素只能容纳文本或其他行内元素

- 注意
  - 链接里面不能再放链接
  - 特殊情况链接 `<a>` 里面可以放块级元素，但是给 `<a>` 转换一下块级模式最安全

4.行内块元素

- 在行内元素中有几个特殊的标签— `<img/> <input/> <td>` 它们同时具有块元素和行内元素的特点，有些资料称他们为行内块元素
- 行内块元素特点
  - 和相邻行内元素（行内块）在一行上，但是他们之间会有空白缝隙。一行可以显示多个（行内元素特点）
  - 默认高度就是它本身内容的宽度（行内元素特点）
  - 高度、行高、内外边距都可以控制（块级元素特点）

5.元素显示模式总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/08/5fsRHd3EuwCWxAL.jpg" alt="1.10" >
</div>
{{</md>}}

6.元素显示模式转换

- 特殊情况下，我们需要元素模式的转换，简单理解：一个模式的元素需要另外一种模式的特性
- 比如想要增加链接 `<a>` 的触发范围
- 行内元素转换为块元素 display: block; （使用多）
- 块元素转换为行内元素 display: inline;
- 转换为行内块元素 diaplay: inline-block; （使用多）

7.一个小工具的使用 snipaste 

8.练习

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* a转换为块级元素, 这样链接就可以独占一行，并且有宽度和高度 */
        a {
            display: block;
            width: 230px;
            height: 40px;
            background-color: #55585a;
            font-size: 14px;
            color: #fff;
            text-decoration: none;
            text-indent: 2em;
        }

        /* 鼠标经过链接变换背景颜色 */
        a:hover {
            background-color: #ff6700;
        }
    </style>
</head>
<body>
    <a href="#">手机 电话卡</a>
    <a href="#">电视 盒子</a>
    <a href="#">笔记本 平板</a>
    <a href="#">出行 穿戴</a>
    <a href="#">智能 路由器</a>
    <a href="#">健康 儿童</a>
    <a href="#">耳机 音响</a>
</body>
</html>

```

9.小技巧 - 单行文字垂直居中的代码

- 让文字的行高等于盒子的高度，就可以让文字在当前盒子内垂直居中 `line-height: 40px;`
- 理解 - 行高的上空隙和下空隙把文字挤到中间，如果行高小于盒子高度，文字会偏上，如果行高大雨盒子高度，则文字偏下（上下空隙平均分配）



### CSS背景

- 通过CSS背景属性，可以给页面元素添加背景样式
- 背景属性可以设置背景颜色、背景图片、背景平铺、背景图片位置、背景图像固定等

1.背景颜色

`<background-color: 颜色值;>` 

- 一般情况下元素背景颜色默认值是transparent (透明)，我们也可以手动指定背景颜色为透明色

2.背景图片

- Background-image 属性描述了元素的背景图像 - 实际开发常见于logo或者一些装饰性的小图片或者是超大的背景图片，优点是非常便于控制位置

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
            width: 300px;
            height: 300px;
            background-image: url();
        }
        
    </style>
</head>
<body>
    <div></div>
</body>
</html>

```

3.背景平铺

- 如果需要在html页面上对背景图像进行平铺，可以使用background-repeat属性

`background-repeat: repeat | no-repeat | repeat-x | repeat-y`

- background-image会压住background-color

4.背景图片位置

- 利用background-position属性改变图片在背景中的位置

`background-position: x y;`

- 参数代表的意思是：x坐标和y坐标。可以使用方位名词或者精确单位

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/08/3JY8HVNjqgAI7kS.jpg" alt="1.11" >
</div>
{{</md>}}

- 参数是方位名词
  - 如果指定的两个值都是方位名词，则两个值前后顺序无关，比如left top 和 top left 效果一致
  - 如果只指定了一个方位名词，另一个值省略，则第二个值默认居中对齐
- 参数是精确单位
  - 如果参数是精确单位，第一个肯定是x坐标，第二个肯定是y坐标
  - 如果只指定一个数值，那该数值一定是x坐标，另一个默认垂直居中

- 参数是混合单位
  - 如果指定的两个值是精确单位和方向名词混合使用，则第一个值是x坐标，第二个值是y坐标

5.背景图像固定（背景附着）

- background-attachment 属性设置背景图像是否固定或者随着页面的其余部分滚动
- background-attachment 后期可以制作视差滚动的效果

`background-attachment: scroll|fixed`

- scroll - 背景图像是随对象内容滚动（默认）
- fixed - 背景图像固定

6.背景复合写法

- 为了简化背景属性的代码，我们可以将这些属性合并间歇在同一个属性background中从而节约代码量
- 当使用简写属性时，没有特定的书写顺序，一般习惯约定顺序为
  - background: 背景颜色 背景图片地址 背景平铺 背景图像滚动 背景图片位置 - 实际开发更提倡的写法

​			`background: transparent url(image.jpg) repeat-y fixed top;`

7.背景色半透明

- CSS3为我们提供了背景颜色半透明的效果

  `background: rgba(0,0,0,0.3);`

- 最后一个参数是alpha透明度，取值范围0-1之间

- 习惯把0.3的0省略掉，写为background: rgba(0,0,0,.3)

- 注意：背景半透明时指盒子背景半透明，盒子里面的内容不受影响

- CSS3新增属性，是IE9+版本浏览器才支持

- 实际开发中，不太关注兼容性写法

8.背景总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/08/hW4R8YsrzEtOp7U.jpg" alt="1.12" >
</div>
{{</md>}}


### CSS三大特性

- 三个特性：层叠性、继承性、优先级

1.层叠性

- 相同选择器设置相同样式，此时一个样式就会覆盖另一个冲突的样式，层叠性主要解决样式冲突的问题
- 层叠性原则
  - 样式冲突，遵循的原则为就近原则，哪个样式离结构近，就执行哪个样式
  - 样式不冲突，不会层叠

2.继承性

- 子标签继承父母标签的某些样式，如文本颜色和字号
- 恰当使用可以简化代码，降低CSS样式的复杂性
- 子元素可以继承父母元素的样式（text-，font-，line-这些元素开头的可以继承，以及color属性）

- 继承性-行高的继承

```html

body {
	font: 12px/1.5 Microsoft YaHei;
}

div {
	/* 子元素继承了父元素body的行高1.5
			这个1.5就是当前元素文字大小font-size的1.5倍，当前div的行高就是21px*/
	font-size: 14px
}

p {
	/* 行高1.5*16=24px */
	font-size: 16px
}

```

- 行高可以跟单位也可以不跟单位
- 如果子元素没有设置行高，则会继承父元素的行高为1.5
- 此时子元素的行高是：当前子元素的文字大小*1.5

3.优先级

- 当同一个元素指定多个选择器，就会有优先级的产生

  - 选择性相同，则执行层叠性
  - 选择器不同，则根据选择器权重执行

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/08/AxMRacgUXP9QNsF.jpg" alt="1.13" >
</div>
{{</md>}}

- 优先级注意点
  - 权重是有4组数字组成，但是不会有进位
  - 类选择器永远大于元素选择器，id选择器永远大于类选择器，以此类推
  - 等级判断从左向右，如果某一位数值相同，则判断下一位数值
  - 继承的权重是0，如果该元素没有直接选中，不管父元素权重有多高，子元素得到的权重都是0

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #test {
            color: red;
        }

        p {
            color: pink;
        }
      
     /* a链接浏览器默认指定了一个样式，蓝色下划线 a {color: blue} */
    </style>
</head>
<body>
    <div id="test">
        <p>content</p>
    </div>
  <a href="#">unique</a>
</body>
</html>

/* 以后看标签到底执行哪个样式，就先看这个标签有没有直接被选出来 */

```

- 权重叠加 - 如果是复合选择器，则会有权重叠加，需要计算权重








