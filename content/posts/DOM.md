---
title: " DOM 基础"
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
  - DOM
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

## 0.Pre

- `DOM（Document Object Model）`： 文档对象模型
- 其实就是操作 `html` 中的标签的一些能力
- 我们可以操作哪些内容

  - 获取一个元素
  - 移除一个元素
  - 创建一个元素
  - 向页面里面添加一个元素
  - 给元素绑定一些事件
  - 获取元素的属性
  - 给元素添加一些 `css` 样式
  - ...

- `DOM` 的核心对象就是 `docuemnt` 对象
- `document` 对象是浏览器内置的一个对象，里面存储着专门用来操作元素的各种方法
- `DOM`： 页面中的标签，我们通过 `js` 获取到以后，就把这个对象叫做 **DOM 对象**

</br>

## 1. 获取一个元素

### getElementById

- `getElementById` 是通过标签的 `id` 名称来获取标签的
- 因为在一个页面中 `id` 是唯一的，所以获取到的就是一个元素

```html
<body>
  <div id="box"></div>
  <script>
    var box = document.getElementById("box");
    console.log(box); // <div></div>
  </script>
</body>
```

- 获取到的就是页面中的那个 **id 为 box 的 div 标签**

### getElementsByClassName

- `getElementsByClassName` 是用过标签的 `class` 名称来获取标签的
- 因为页面中可能有多个元素的 `class` 名称一样，所以获取到的是一组元素
- 哪怕你获取的 `class` 只有一个，那也是获取一组元素，**只不过这一组中只有一个 DOM 元素而已**

```javascript
<body>
  <div calss="box"></div>
  <script>
    var box = document.getElementsByClassName('box') console.log(box) // [<div></div>

    ] console.log(box[0]) // <div></div>
  </script>
</body>
```

- 获取到的是一组元素，是一个长得和数组一样的数据结构，但是不是数组，是 **伪数组**
- 这个一组数据也是按照索引排列的，所以我们想要准确的拿到这个 `div`，需要用索引来获取

### getElementsByTagName

- `getElementsByTagName` 是用过标签的 标签 名称来获取标签的
- 因为页面中可能有多个元素的 标签 名称一样，所以获取到的是一组元素
- 哪怕真的只有一个这个标签名，那么也是获取一组元素，只不过这一组中只有一个 DOM 元素而已

```html
<body>
  <div></div>
  <script>
    var box = document.getElementsByTagName("div");
    console.log(box); // [<div></div>]
    console.log(box[0]); // <div></div>
  </script>
</body>
```

- 和 `getElementsByClassName` 一样，获取到的是一个长得很像数组的元素
- 必须要用索引才能得到准确的 `DOM` 元素

### querySelector

- `querySelector` 是按照选择器的方式来获取元素
- 也就是说，按照我们写 `css` 的时候的选择器来获取
- 这个方法只能获取到一个元素，并且是页面中第一个满足条件的元素

```javascript
console.log(document.querySelector("div")); // 获取页面中的第一个 div 元素
console.log(docuemnt.querySelector(".box")); // 获取页面中第一个有 box 类名的元素
console.log(document.querySelector("#box")); // 获取页面中第一个 id 名为 box 的元素
```

### querySelectorAll

- `querySelectorAll` 是按照选择器的方式来获取元素
- 这个方法能获取到所有满足条件的元素，以一个伪数组的形式返回

```javascript
console.log(document.querySelectorAll("div")); // 获取页面中的所有的 div 元素
console.log(docuemnt.querySelectorAll(".box")); // 获取页面中所有有 box 类名的元素
```

- 获取到的是一组数据，也是需要用索引来获取到准确的每一个 `DOM` 元素

</br>

## 2. 操作属性

- 通过我们各种获取元素的方式获取到页面中的标签以后
- 我们可以直接操作 `DOM` 元素的属性，就能直接把效果展示在页面上

### innerHTML

- 获取元素内部的 `HTML` 结构

```html
<body>
  <div>
    <p>
      <span>hello</span>
    </p>
  </div>

  <script>
    var div = document.querySelector("div");
    console.log(div.innerHTML);
    /*

          <p>
            <span>hello</span>
          </p>

	  */
  </script>
</body>
```

- 设置元素的内容

```html
<body>
  <div></div>

  <script>
    var div = document.querySelector("div");
    div.innerHTML = "<p>hello</p>";
  </script>
</body>
```

- 设置完以后，页面中的 `div` 元素里面就会嵌套一个 `p` 元素

### innerText

- 获取元素内部的文本（只能获取到文本内容，获取不到 `html` 标签）

```html
<body>
  <div>
    <p>
      <span>hello</span>
    </p>
  </div>

  <script>
    var div = document.querySelector("div");
    console.log(div.innerText); // hello
  </script>
</body>
```

- 可以设置元素内部的文本

```html
<body>
  <div></div>

  <script>
    var div = document.querySelector("div");
    div.innerText = "<p>hello</p>";
  </script>
</body>
```

- 设置完毕以后，会把 `<p>hello</p>` 当作一个文本出现在 `div` 元素里面，而不会把 `p` 解析成标签

### getAttribute

- 获取元素的某个属性（包括自定义属性）

```html
<body>
  <div a="100" class="box"></div>

  <script>
    var div = document.querySelector("div");
    console.log(div.getAttribute("a")); // 100
    console.log(div.getAttribute("class")); // box
  </script>
</body>
```

### setAttribute

- 给元素设置一个属性（包括自定义属性）

```html
<body>
  <div></div>

  <script>
    var div = document.querySelector("div");
    div.setAttribute("a", 100);
    div.setAttribute("class", "box");
    console.log(div); // <div a="100" class="box"></div>
  </script>
</body>
```

### removeAttribute

- 直接移除元素的某个属性

```html
<body>
  <div a="100" class="box"></div>

  <script>
    var div = document.querySelector("div");
    div.removeAttribute("class");
    console.log(div); // <div a="100"></div>
  </script>
</body>
```

### style

- 专门用来给元素添加 `css` 样式的
- 添加的都是行内样式

```html
<body>
  <div></div>

  <script>
    var div = document.querySelector("div");
    div.style.width = "100px";
    div.style.height = "100px";
    div.style.backgroundColor = "pink";
    console.log(div);
    // <div style="width: 100px; height: 100px; background-color: pink;"></div>
  </script>
</body>
```

- 页面中的 `div` 就会变成一个宽高都是 `100`，背景颜色是粉色

### 获取元素的非行间样式

- 我们在操作 `DOM` 的时候，很重要的一点就是要操作元素的 `css` 样式
- 那么在操作 `css` 样式的时候，我们避免不了就要获取元素的样式
- 之前我们说过可以用 `元素.style.xxx` 来获取
- 但是这个方法只能获取到元素 **行间样式**，也就是写在行内的样式

```html
<style>
  div {
    width: 100px;
  }
</style>

<body>
  <div style="height: 100px;">
    <p>我是一个 p 标签</p>
  </div>

  <script>
    var oDiv = document.querySelector("div");
    console.log(oDiv.style.height); // 100px
    console.log(oDIv.style.width); // ''
  </script>
</body>
```

- 不管是外链式还是内嵌式，我们都获取不到该元素的样式
- 这里我们就要使用方法来获取了 **`getComputedStyle`** 和 **`currentStyle`**
- 这两个方法的作用是一样的，只不过一个在 **非 IE** 浏览器，一个在 **IE** 浏览器

#### getComputedStyle（非 IE 使用）

- 语法：`window.getComputedStyle(元素, null).要获取的属性`

```html
<style>
  div {
    width: 100px;
  }
</style>

<body>
  <div style="height: 100px;">
    <p>我是一个 p 标签</p>
  </div>

  <script>
    var oDiv = document.querySelector("div");
    console.log(window.getComputedStyle(oDiv).width); // 100px
    console.log(window.getComputedStyle(oDiv).height); // 100px
  </script>
</body>
```

- 这个方法获取行间样式和非行间样式都可以

#### currentStyle（IE 使用）

- 语法： `元素.currentStyle.要获取的属性`

```html
<style>
  div {
    width: 100px;
  }
</style>

<body>
  <div style="height: 100px;">
    <p>我是一个 p 标签</p>
  </div>

  <script>
    var oDiv = document.querySelector("div");
    console.log(oDiv.currentStyle.width); // 100px
    console.log(oDiv.currentStyle.height); // 100px
  </script>
</body>
```

### className

- 专门用来操作元素的 **类名的**

```html
<body>
  <div class="box"></div>

  <script>
    var div = document.querySelector("div");
    console.log(div.className); // box
  </script>
</body>
```

- 也可以设置元素的类名，不过是全覆盖式的操作

```html
<body>
  <div class="box"></div>

  <script>
    var div = document.querySelector("div");
    div.className = "test";
    console.log(div); // <div class="test"></div>
  </script>
</body>
```

- 在设置的时候，不管之前有没有类名，都会全部被设置的值覆盖

</br>

## 3. DOM 节点

</br>

## 4. 节点属性

</br>

## 5. 操作 DOM 节点

</br>

## 6. 获取元素的偏移量

</br>

## 7. 获取元素尺寸

</br>

## 8. 获取元素窗口尺寸

</br>

## 9. 事件

</br>

## 10. 事件的绑定方式

</br>

## 11. 常见的事件

</br>

## 12. 事件对象

</br>

## 13. 事件的传播

</br>

## 14. 事件委托

</br>

## 15. 默认行为

</br>

## 16. this 关键字

</br>

## 17. call 和 apply 和 bind

</br>
