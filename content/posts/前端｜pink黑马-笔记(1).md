---
title: "前端｜pink黑马-笔记(1)"
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
- HTML
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


## HTML 简介导读

<br>



### 目标

- 网页的基本组成
- 什么是HTML
- 常用的游览器
- Web标准的三大组成部分

<br>



### 网页

1.什么是网页

- 网站是指在因特网上根据一定的规则，使用html制作的用于展示特性内容相关的网页合集
- 网页时网站中的一“页”，通常是html格式的文件，它要通过浏览器来阅读
- 网页时构成网站的基本元素，它通常由图片、链接、文字、声音、视频等元素组成
- 通常我们看到的网页，常见以.htm或.html后缀结尾的文件，因此将其俗称为HTML文件

2.什么是html

- 超文本标记语言 Hyper Text Markup Language - 用来描述网页的一种语言

- html不是一种编程语言，而是一种标记语言markup language

- 标记语言是一套标记标签markup tag

  超文本 - 2层含义

- 它可以加入图片、声音、动画、多媒体等内容 - 超越了文本限制

- 它还可以从一个文件跳转到另一个文件，与世界各地主机的文件连接-超级连接文本

3.网页的形成

- 网页是由网页元素(图片、链接、文字、声音、视频)组成，这些元素是利用html标签描述出来，然后通过浏览器来显示给用户的

<br>



### 常用浏览器

1.常用浏览器

- 浏览器是网页显示、运行的平台。常用的浏览器有IE、火狐(Firefox)、谷歌(Chrome)、Safari和Opera等，平时称为五大浏览器

2.浏览器内核

- 浏览器内核-渲染引擎：负责读取网页，整理讯息，计算网页的显示方式并显示网页

![](https://s2.loli.net/2022/02/01/k4BlQIo7NfZsUpA.jpg)


<br>



### Web 标准

1.Web 标准是由W3C组织和其他标准化组织制定的一系列标准的集合 - W3C万维网联盟是国际最著名的标准化组织

2.为什么需要Web标准

- 浏览器不同，它们显示页面或者排版就有些许差异

3.Web标准的构成

- 包括结构structure、表现presentation和行为behavior三个方面

![](https://s2.loli.net/2022/02/01/YfUpjnOKM7yZRNA.jpg)


<br>

<hr>



## HTML标签(上)

<br>



### 目标

- 标签的书写注意规范
- HTML骨架标签
- 超链接标签
- 写出图片标签并说出alt和title的区别
- 相对路径的三种形式

<br>



### HTML语法规范

- 双标签 `<html></html>`
- 单标签(较少) `<br>`

1.基本语法概述

- html标签是由尖括号包围的关键词，例如`<html>`
- html标签通常是成对出现，例如双标签，标签对中的第一个标签是开始标签，第二个标签是结束标签
- 有些特殊的标签必须是单个标签(极少情况) - 单标签

2.标签关系

- 包含关系

```html

<head>
  <title></title>
</head>

```

- 并列关系

```html

<head></head>
<body></body>

```

<br>



### HTML基本结构标签

1.第一个html网页

- 每个网页都会有一个基本的结构标签(也称为骨架标签)，页面内容也是在这些基本标签上书写

- html页面也称为html文档

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>

```

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/01/iOv6q2Z3chX4Jxj.jpg" alt="03" >
</div>
{{</md>}}

2.基本结构标签总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/01/RgZP7AcwtVJLFQe.jpg" alt="04" >
</div>
{{</md>}}

<br>



### 开发工具

1.VSCode的使用

- 双击打开软件
- 新建文件 command+N
- 保存 command+S - 注意移动要保存为.html文件
- command +  放大 / command - 缩小
- 生成页面骨架结构 - ! 或者html + return
- 预览页面

2.文档类型的声明标签 - <!DOCTYPE>

- <!DOCTYPE> 文档类型声明，作用为告知浏览器使用哪种HTML版本来显示网页 - html5

- 声明位于文档中的最前面位置，处于`<html>` 标签之前

3.lang语言种类 - `<html lang="en">`

- 用来定义当前文档显示的语言
- en为英语/zh-CN为中文
- 对于文档显示来说，定义en的文档也可以显示中文，定义zh-CN文档也可以显示英文

4.字符集

- 字符集character set 是多个字符的集合，以便计算能够识别和存储各种文字
- `head` 标签内，可以通过`meta` 标签的charset属性来规定html文档应该使用哪种字符编码

5.总结

- `<!DOCTYPE html>` - 文档类型声明标签、告诉浏览器这个页面采取html15版本来显示页面
- `<html lang="en">` - 告诉浏览器或者搜索引擎这是一个英文网站 - 本页面采取英文显示
- `<meta charset="UTF-8">` - 采取UTF-8来保存文字 - 如果不写则会乱码 - 具体原理后面分析

<br>



### HTML 常用标签

1.标签语义

- 学习标签是有技巧的，重点是记住每个标签的语义。简单理解就是指标签的含义，即这个标签的用处
- 根据标签的语义，在合适的地方放置合理标签让页面结构更加清晰

2.标题标签 `<h1>` - `<h6>` (重要)

​	`<h1></h1>`

- 为了使网页更具语义化，页面中经常用到标题标签 - HTML提供了6个等级的网页标题
- 单词head的缩写 - 意为头部、标题
- 作为标题使用，并且依据重要性递减
- 由大到小依次减小，一个标题独占一行

3.段落和换行标签(重要)

- 在网页中，文字有条理显示 - `<p>`
- `<p>` 标签用于定义段落，它可以将整个网页分为若干个段落 - 单词paragrah的缩写 - 
- 文本在一个段落中会根据浏览器窗口的大小自动换行
- 每个段落之间有较大空隙
- 强制换行显示 - `<br>` - break缩写
- 换行之间不会有较大空隙

4.文本格式化标签

- 有时需要文字设置加粗、斜体或下划线等效果，需要用到html中的文本格式化标签，使文字以特殊的方式显示

- 标签语义：突出重要性，比普通文字更重要 

- 加粗 - 重要

   `<strong></strong>` - 语义更强调

  `<b></b>`

- 倾斜 - 重要 

  `<em></em>` - 推荐

  `<i></i>` 

- 删除线

  `<del></del>`  - 推荐

  `<s></s>` 

- 下划线

  `<ins></ins>` - 推荐

  `<u></u>`

<br>



### `<div>`和`<span>`标签

- 这两个标签没有语义，它们就是一个盒子，用来装内容
- `<div></div>`
- `<span></span>` 

1.`<div></div>` 标签用来布局，但是现在一行只能放一个`<div>` - 大盒子 

2.`<span></span>` 标签用来布局，但是一行可以放多个 - 小盒子

<br>



### 图像标签和路径(重点)

1.图像标签

- 在html中，`<img>` 标签用来定义html页面中的图像

  `<img src="">`

- img单词image的缩写，意思为图像

- src是`<img>` 标签的必须属性，它用于指定图像文件的路径和文件名

- 所谓属性：简单理解就是属于这个图像标签的特性

- image其他属性

  (待补充)

2.图像标签注意点

- 图像标签可以拥有多个属性，必须写在标签名的后面
- 属性之间不分顺序，标签名与属性、属性与属性之间均以空格分开
- 属性采取健值对的格式，即key=”value“的格式，属性=“属性值”

3.路径

(前期铺垫知识

目录文件夹和根目录

- 目录文件夹：就是普通文件夹，里面只不过存放了我们做页面所需要的相关材料，比如html文件、图片等
- 根目录：打开目录文件夹的第一层就是根目录

- VSCode打开目录文件)

需要采用“路径”方式来指定图像文件的位置

- 相对路径 - 以引用文件所在位置为参考基础，建立出的目录路径，这里简单来说，图片相对于HTML页面的位置 - 符号 - /

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/01/nsMg1R2zEeWAZHd.jpg" alt="05" >
</div>
{{</md>}}

- 绝对路径 - 指目录下的绝对位置，直接达到目标位置，通常从盘符开始的路径 - 符号 - \

<br>



### 超链接标签(重点)

在html标签中，`<a>` 	标签用于定义超链接，作用是从一个页面链接到另一个页面

1.超链接的语法规范

`<a href="跳转目标" target="目标窗口弹出方式">文本或者图像</a>`

- 单词anchor的缩写

- 两个属性作用如下

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/11/I6Ejxnw5FGysecz.jpg" alt="06" >
</div>
{{</md>}}

2.链接分类

- 外部链接 - 非自创页面 

- 内部链接 - 网站内部页面之间的相互链接 直接链接内部页面名称即可 `<a href="index.html"></a>`

- 空链接 - 没有确定链接目标时 `<a href="#"></a>`

- 下载链接 - 如果href里面是一个文件或者压缩包，会下载这个文件 `<a href="目标名称"></a>`

- 网页元素链接 - 在网页中的各种网页元素，如文本、图像、表哥、音频和视频等都可以添加超链接

  例如给图片添加链接

  `<a href="网址"><img src=""></a>`

- 锚点链接 - 点击链接可以快速定位到页面中的某个位置

  - 在连接文本的href位置中，设置属性值为#名字的形式，如`<a href="#two"></a>` 
  - 找到目标位置标签，里面添加一个id属性 = 刚才的名字，如`<h3 id="two"></h3>`

<br>



### HTML中的注释和特殊字符

1.注释

- 如果要在HTML文档中添加一些便于阅读和理解但又不需要显示在页面中的注释文字，就需要使用注释标签
- HTML中的注释 `<!--注释内容-->`
- command + / - 自动添加注释

2.特殊字符

- 记住 空格/大于号/小于号

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/01/rCREaIjwzPqAgNn.jpg" alt="07" >
</div>
{{</md>}}
<br>
<hr>

## HTML标签(下)导读

<br>



### 目标

- 书写列表
- 书写无序列表
- 3～4个常用input表单 类型
- 写出下拉列表表单
- 使用表单元素实现注册页面
- 独立查阅W3C文档

<br>



### 表格标签

1.表格的主要作用

- 表格不是用来布局页面的，而是用来展示数据的

2.表格的基本语法

```html

<table>
  <tr>
    <td>单元格内的文字</td>
    ...
  </tr>
  ...
</table>

```

- `<table></table>` 用来定义表格的标签
- `<tr></tr>` 定义表格中的行，必须嵌套在`<table></table>` 中
- `<td></td>` 定义表格中的单元格，必须嵌套在 `<tr></tr>` 
- 字母td指table data，即数据单元格的内容

3.表头单元格标签

- 一般表头单元格位于表格的第一行或者第一列，表头单元格里面的文本内容加粗居中显示

- `<th>` 标签表示HTML表格的表头部分(table head的缩写)
```html

<table>
  <tr>
    <th>姓名</th>
    ...
  </tr>
    ...
</table>

```

4.表格属性

- 表格标签这部分属性我们实际开发不常用，后面通过CSS来设置

  目的有两个：

- 直观感受表格的外观形态

- 记住这些英语单词，后面CSS会使用

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/01/Xj2x3vTIAJHdYpV.jpg" alt="08" >
</div>
{{</md>}}

5.表格结构标签

- 使用场景：因为表格可能很长，为了更好的表示表格的语义，可以将表格分割成表格头部和表格主体两大部分
- 在表格标签中，分别用：`<thead>` 标签 表格的头部、`<tbody>` 标签 表格的主体区域，这样可以更好的分清表格结构
- `<thead></thead>` - 用于定义表格的头部 - `<head>` 内必须拥有`<tr>` 标签，一般是位于第一行
- `<tbody></tbody>` - 用于定义表格的主体，主要用于放数据本体
- 以上标签都放置于  `<table></table>` 

6.合并单元格

- 合并单元格方式

  - 跨行合并：rowspan = "合并单元格的个数"

  - 跨列合并：colspan = ”合并单元格的个数“

    {{<md>}}
    <div align="center">
    <img src="https://s2.loli.net/2022/02/01/3fHXNmWuhoJs2KQ.jpg" alt="09" >
    </div>
    {{</md>}}

- 目标单元格：写合并代码

  - 跨行：最上侧单元格为目标单元格，写合并代码
  - 跨列：最左侧单元格为目标单元格，写合并代码

- 合并单元格的步骤

  - 确定跨行还是跨列
  - 找到目标单元格 写上合并方式 = 合并的单元格数量 比如 `<td colspan= "2"></td>`
  - 删除多余的单元格

7.表格总结

- 表格的相关标签
- 表格的相关属性
- 合并单元格

<br>



### 列表标签

- 列表-布局
- 根据使用场景不同，列表可以分为三大类：无序列表、有序列表和自定义列表

1.无序列表(重点)

- `<ul>` 标签表示html页面中项目的无序列表，一般会以项目符号呈现列表项，而列表项使用`<li>` 标签定义

```html
<ul>

  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ...
</ul>

```

- 无序列表的各个列表项之间没有顺序级别之分，是并列的
- `<ul></ul>` 中只能嵌套 `<li></li>` ，其他的标签和文字都不可以

-  `<li></li>` 之间相当于一个容器，可以容纳所有元素
- 无序列表会带有自己的样式属性，但在实际使用中，我们会使用CSS来设置

2.有序列表

- 有序列表即有排列顺序的列表，其各个列表项会按照一定的顺序排列定义

- 在HTML标签中，`<ol>` 标签用于定义有序列表，列表排序以数字来显示，并且使用`<li>` 标签来定义列表项

```html

<ol>
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ...
</ol>

```

- `<ul></ul>` 中只能嵌套 `<li></li>` ，其他的标签和文字都不可以
-  `<li></li>` 之间相当于一个容器，可以容纳所有元素
- 有序列表会带有自己的样式属性，但在实际使用中，我们会使用CSS来设置

3.自定义列表

- 自定义列表常用于对术语或名词进行解释和描述，定义列表的列表项前没有任何项目符号

- 在HTML标签中，`<dl>` 标签用于定义描述列表，该标签会与`<dt>` (定义项目/名字) 和 `<dd>` (描述每一个项目/名字) 一起使用

```html

<dl>
  <dt>名词1</dt>
  <dd>名词1解释1</dd>
  <dd>名词1解释2</dd>
</dl>

```

- `<dl></dl>` 里面只能包含 `<dt>` 和 `<dd>` 
- `<dt>` 和 `<dd>` 个数没有限制，经常是一个`<dt>` 对应多个 `<dd>` 

4.列表总结

{{<md>}}
<div align="center">
<img src="https://s2.loli.net/2022/02/01/iQ6q9WAxo37SzVK.jpg" alt="10" >
</div>
{{</md>}}

<br>



### 表单标签

1.为什么需要表单

- 收集用户信息

2.表单的组成

- 在html中，一个完整的表单通常由表单域、表单控件(也称表单元素)和提示信息3个部分构成

  {{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/01/STc47X9hMt2Hi6x.jpg" alt="11" >
  </div>
  {{</md>}}

3.表单域

- 表单域是一个包含表单元素的区域

- `<form>` 标签用于定义表单域，以实现用户信息的收集和传递

- `<form>` 会把规定范围内的表单元素信息提交给服务器

```html

<form action="url地址" method="提交方式" name="表单域名称">
  各种表单元素控件
</form>

```

- 常用属性

  {{<md>}}
  <div align="center">
  <img src="https://s2.loli.net/2022/02/01/gCtuJXWjUpl9bHa.jpg" alt="12" >
  </div>
  {{</md>}}

4.表单控件(表单元素)

- 在表单域中可以定义各种表单元素，这些表单元素就是允许用户在表单中输入或者选择的内容控件

- input输入表单元素

  - `<input>` 标签用于收集用户信息

  - `<input>` 标签中，包含一个type属性，根据不同的type属性值，输入字段拥有很多形式(可以是文本字段、复选框、掩码后的文本控件、单选按钮、按钮等)

    `<input type ="属性值">`

  - `<input>` 为单标签

  - type属性值设置不同的属性值用来指定不同的控件类型

    {{<md>}}
    <div align="center">
    <img src="https://s2.loli.net/2022/02/01/mDOCl1iqPtnZoLE.jpg" alt="13" >
    </div>
    {{</md>}}

  - input常用其他属性

    {{<md>}}
    <div align="center">
    <img src="https://s2.loli.net/2022/02/01/CbVyZ7mrGLjot2h.jpg" alt="14" >
    </div>
    {{</md>}}

    - name是表单元素名字，单选按钮radio中必须要有相同的名字才能实现多选1，复选按钮同理
    - value - 预览填充input框框，只在文本框中能看到效果，主要针对后台人员使用
    - name和value是每个表单元素都有的属性，主要给后台人员使用
    - name表单元素的名字，要求单选按钮和复选框要有相同的name值
    - 单选按钮和复选框可以设置checked属性，当页面打开的时候就可以默认选中按钮
    - maxlength是用户可以在表单元素输入的最大字符数，一般较少使用

- label标签

  - `<label>` 标签为input元素定义标注 (标签)

  - `<label> ` 标签用于绑定一个表单元素，当点击`<label>` 标签内的文本时，浏览器就会自动将焦点(光标)转到或者选择对应的表单元素上，用来增加用户体验

```html

<label for="">内容</label>
<input type="radio" name="" id="">
/*for和id属性的值必须相同*/

```

- select下拉表单元素

  - 在页面中，如果有多个选项让用户选择，并且想要节约页面空间时，我们可以使用`<select>` 标签控件定义下拉标签

```html

<select>
  <option>选项1</option>
  <option>选项2</option>
  <option>选项3</option>
  ...
</select>

```

  - `<select>` 中至少包含一对 `<option>` 

  - 在`<option>` 中定义selected= “selected”时，当前项即为默认选中项

    `<option selected="selected">内容1</option>`

- textarea文本域元素

  - 使用场景：当用户输入内容较多的情况下，我们就不能使用文本框表单了，此时我们可以使用`<textarea>` 标签

  - 在表单元素中，`<textarea>` 标签是用于定义多行文本输入的控件

```html

<textarea rows="3" cols="2">
  文本内容
</textarea>

```

  - 通过`<textarea>` 标签可以轻松地创建多行文本输入框
  - cols= "每行中的字符数"，rows= "显示的行数"，我们在实际开发中不会使用，都是用CSS来改变大小

<br>



### 学会查阅文档

- W3C
- MDN
- ....

<br>

<hr>








