---
title: "建立摄影网站 home 总计"
subtitle: ""
date: 2022-04-03
draft: false
author: ""
authorLink: ""
description: "一些css相关点"
keywords: ""
license: ""
comment: false
weight: 0

tags:
  - css
categories:
  - css

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

## Responsive web design - basic

### Set the viewpoint

- 在 head 必须有 meta viewport tag -> give the browser instructions on how to control the page's dimensions and scaling

- 一般 desktop scree size -> 980px

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    …
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    …
  </head>
  …
</html>
```

- `width=device-width` instructs the page to match the screen's width in device-independent pixels -> This allows the page to reflow content to match different screen sizes, whether rendered on a small mobile phone or a large desktop monitor

- value `initial-scale=1` instructs browsers to establish a 1:1 relationship between CSS pixels and device-independent pixels regardless of device orientation, and allows the page to take advantage of the full landscape width

</br>

### Ensure an accessible viewport

- `minimum-scale`
- `maximum-scale`
- `user-scalable`

--> When set, these can disable the user's ability to zoom the viewport, potentially causing accessibility issues. Therefore we would not recommend using these attributes

</br>

### Size to centent to the viewport

#### imgaes

```css
img {
  max-width: 100%;
  display: block;
}
```

- `max-width` of `100%`
  - cause the image to shrink to fit the space it has
  - because the `max-width`, rather than the `width` is `100%`, the image will not stretch larger than its natural size
    - width:100% : 100%是将所有指定元素的宽度拉伸或收缩到和父元素的宽度一致
    - max-width:100% : 如果 img 宽度大于 div 宽度，img 就显示 div100%宽度，否则就显示 img 自身的宽度
    - 很多适合 width 和 max-width 是配合使用的：比如设置一个标签，`width` 是（父元素的）`80%`但是 `max-width` 不能超过`1200px`，那么这个标签就有了一个最基本的可缩放特性

#### layout

- By using **percentages for the widths**, the columns always remain a certain percentage of the container. This means that the columns become narrower, rather than creating a scrollbar

- Modern CSS layout techniques such as **Flexbox, Grid Layout, and Multicol** make the creation of these flexible grids much easier

</br>

### Use CSS media queries for responsiveness

```
@media print {
/* print styles go here */
}
```

- For responsive web design, we are typically querying the *features* of the device in order to provide a different layout for smaller screens, or when we detect that our visitor is using a touchscreen

#### media queries based on viewport size

- `width` (`min-width`, `max-width`)
- `height` (`min-height`, `max-height`)
- `orientation`
  - 屏幕方向 (orientation) 可用于测试视口 viewport 的横纵方向
  - portrait -> 处于纵向 高度大于宽度
  - landscape -> 处于横向 宽度大于高度
- `aspect-ratio`
  - aspect-ratio css 媒体属性 可以用来测试 viewport 的宽高比
  - 宽高比属性被指定为 ratio 值来代表 viewport 的宽高比
  - 其为一个范围，这意味着你可以使用  **`min-aspect-ratio`**  和  **`max-aspect-ratio`**  分别查询最小和最大的值

#### media queries based on device capability

- `hover`
- `pointer`
- `any-hover`
- `any-pointer`

</br>

### How to choose breakpoints

#### pick major breakpoints by starting small, then working up

- Design the content to fit on a small screen size first, then expand the screen until a breakpoint becomes necessary. This allows you to optimize breakpoints based on content and maintain the least number of breakpoints possible

- 慢慢拉大，查询 breakpoint 点，insert breakpoint 点

```css
@media (max-width: 600px) {
}

@media (min-width: 601px) {
}
```

- Inside the media query for a `max-width` of `600px`, add the CSS which is only for small screens. Inside the media query for a `min-width` of `601px` add CSS for larger screens

#### pick minor breakpoints when necessary

- 由小至大

```css
@media (min-width: 360px) {
  body {
    font-size: 1em;
  }
}

@media (min-width: 500px) {
  .seven-day-fc .temp-low,
  .seven-day-fc .temp-high {
    display: inline-block;
    width: 45%;
  }

  .seven-day-fc .seven-day-temp {
    margin-left: 5%;
  }

  .seven-day-fc .icon {
    width: 64px;
    height: 64px;
  }
}

@media (min-width: 700px) {
  .weather-forecast {
    width: 700px;
  }
}
```

</br>

### Optimize text for reading

Classic readability theory suggests that an ideal column should contain 70 to 80 characters per line (about 8 to 10 words in English). Thus, each time the width of a text block grows past about 10 words, consider adding a breakpoint.

![Screenshot 2023-04-05 at 1.47.45 PM.png](https://s2.loli.net/2023/04/05/NOLMbsuUQdKDyX4.png)

- Let's take a deeper look at the above blog post example. On smaller screens, the Roboto font at `1em` works perfectly giving 10 words per line, but larger screens require a breakpoint. In this case, if the browser width is greater than `575px`, the ideal content width is `550px`.

```css
@media (min-width: 575px) {
  article {
    width: 550px;
    margin-left: auto;
    margin-right: auto;
  }
}
```

</br>

## 固定侧边栏

![Screenshot 2023-04-05 at 1.52.04 PM.png](https://s2.loli.net/2023/04/05/oC8WUHTy43phMba.png)

- 整体布局 flex / direction：row (aside-container + content-container)

- aside-container

```
.aside-container {
	display: flex;
	width: 100%;
	flex-direction: column;
	max-height: 100vh;
}
```

- content-container

```
.content-container {
	width: 100%;
	max-height: 100vh;
}
```

- media query

```


@media screen and (min-width: 50.625rem) {
	.flex-container {
		display: flex;
		flex-direction: row;
	}

	.aside-container {
		display: flex;
		width: 20rem;
		flex-direction: column;
		margin-left: 1rem;
	}



	.content-container {
		width: calc(100% - 20rem);
		overflow: auto;
	}
}

@media screen and (min-width: 75rem) {

	.aside-container {
		width: 22rem;
		margin-left: 1rem;
	}


	.content-container {
		width: calc(100% - 20rem);
		overflow: auto;
	}

}
```

</br>

## 匹配 rem 到 px

- vscode plugin 可以自动转换 - px to rem
- chrome 的默认字体 font 为 16px

</br>

## flex 一些写法意思

### flex 项目的动态尺寸

现在让我们回到第一个例子，看看是如何控制 flex 项占用空间的比例的

1. 第一步，将以下规则添加到 CSS 的底部：

```css
article {
  flex: 1;
}
```

- 这是一个无单位的比例值，表示每个 flex 项沿主轴的可用空间大小

- 本例中，我们设置元素的 flex 值为 1，这表示每个元素占用空间都是相等的

- 占用的空间是在设置 padding 和 margin 之后剩余的空间

- 它是一个比例

2. 现在在上一个规则下添加：

```css
article:nth-of-type(3) {
  flex: 2;
}
```

- 现在当你刷新，你会看到第三个元素占用了两倍的可用宽度和剩下的一样——现在总共有四个比例单位可用

- 前两个 flex 项各有一个，因此它们占用每个可用空间的 1/4

- 第三个有两个单位，所以它占用 2/4 或者说是 1/2 的可用空间

3. 你还可以指定 flex 的最小值。尝试修改现有的 article 规则

```css
article {
  flex: 1 200px;
}

article:nth-of-type(3) {
  flex: 2 200px;
}
```

- 这表示“每个 flex 项将**首先给出 200px 的可用空间**，然后，**剩余的可用空间将根据分配的比例共享**”

### flex 三项简写

- flex-grow / flex shrink / flex-basis 简写

1. 默认值为 0 1 auto -> 表示元素尺寸不放大会收缩

2. `flext: 0 0 auto`

- flex:0 0 auto 表示**元素尺寸不会拓展也不会收缩**，再加上 flex-basis:auto 表示固定尺寸由内容决定，由于元素不具有弹性，因此，元素内的内容不会换行，最终尺寸通常表现为最大内容宽度

3. 自己使用 `flex: 0 0 40rem`

- 表示 content-container 尺寸有空余空间不放大不会收缩，并且在分配多余空间之前，项目占据的主轴空间（main size）为 40rem

</br>

## background-img 自适应

```css
/* 元素是div */
.project1 {
  width: 100%;
  height: 25rem;
  background-image: url(https://s2.loli.net/2023/04/02/keuVaJgbymrGj6E.jpg);
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
}
```

</br>
