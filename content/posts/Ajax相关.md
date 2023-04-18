---
title: "异步 JavaScript——回调、Promises 和 Async/Await"
subtitle: ""
date: 2023-04-18
draft: false
author: ""
authorLink: ""
description: "似懂非懂吧🤯"
keywords: ""
license: ""
comment: false
weight: 0

tags:
  - Ajax
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

## 概览

### 回调

- **回调是在另一个函数内部传递的函数，然后在该函数中调用以执行任务**

```javascript
console.log("fired first");
console.log("fired second");

setTimeout(() => {
  console.log("fired third");
}, 2000);

console.log("fired last");

// fired first
// fired second
// fired last
// fired third
```

- 你会看到在函数  `setTimeout`  返回结果之前输出了最后一条指令。假设我们使用此方法从数据库中获取数据。当用户在等待数据库调用返回结果时，执行中的流程不会被中断

- 这种方法非常有效，但仅限于一点。有时候，开发人员必须对代码中的不同源代码进行多次调用。为了进行这些调用，回调将被嵌套，直到它们变得非常难以读取或维护。这被称为**回调地狱** - > 引入 Promise / fetch API

### Promise

在我们的语境中，promise 是需要一些时间去做的事情。一个 promise 有两种可能的结果：

- 我们要么运行并解决 promise，要么
- 执行过程中出现了一些错误，promise 被拒绝

promise 的出现是为了解决回调函数的问题。promise 接受两个函数作为参数。即`resolve`和`reject`。请记住，resolve 表示成功时，reject 表示错误发生时。

让我们看一下 promise 的作用：

```javascript
const getData = (dataEndpoint) => {
   return new Promise ((resolve, reject) => {
     //some request to the endpoint;

     if(request is successful){
       //do something;
       resolve();
     }
     else if(there is an error){
       reject();
     }

   });
};
```

- 上面的代码是一个 promise，包含在对某个端点的请求中。就像我前面提到的，这个 promise 包含了`resolve`和`reject`。

- 例如，在调用端点之后，如果请求成功，我们将解决承诺并继续对响应执行任何我们想要的操作。但是如果出现错误，承诺就会被拒绝。

- Promise 是一种巧妙的方法用来解决回调地狱带来的问题, 被称为  **promise 链式调用**。你可以使用这个方法从多个端点顺序地获取数据，但代码更少，方法更简单

### fetch API

- 像回调一样将 promise 链接在一起会变得非常庞大和混乱。这就是产生 Async 和 Await 的原因。执行以下操作定义一个异步函数：

```javascript
const asyncFunc = async () => {};
```

- 请注意，**调用异步函数将始终返回一个 promise** 。看看这个：

```javascript
const test = asyncFunc();
console.log(test);
```

- 在浏览器控制台中运行上面的代码，我们看到  `asyncFunc`  返回了一个 promise。

- 现在让我们真正分解一些代码。思考下面的代码片段：

```javascript
const asyncFunc = async () => {
  const response = await fetch(resource);
  const data = await response.json();
};
```

- `async`  关键字是我上面提到的用来定义 async 函数的。但是  `await`呢？好吧，它阻止 JavaScript 在解决 promise 之前将  `fetch`  赋值给 response 变量。一旦 promise 被解决，现在可以将 fetch 方法的结果分配给 response 变量。

- 第 3 行代码也是相同的行为。`.json`  方法返回一个 promise 对象，我们可以使用  `await`  延迟分配直到 promise 被解决。

- 当我说“暂停”，你一定认为实现 Async 和 Await 以某种方式阻塞代码执行。因为我们的请求花费的时间太长了，对吧？

- 事实上并不是。async 函数内部的代码会阻塞，但不会以任何方式影响程序的执行。**代码的执行仍然是异步的**。正如下面的代码：

```javascript
const asyncFunc = async () => {
  const response = await fetch(resource);
  const data = await response.json();
};

console.log(1);
console.log(2);

asyncFunc().then((data) => console.log(data));

console.log(3);
console.log(4);

//1
//2
//3
//4
//data returned by asyncFunc
```

## 深入 Ajax 基础

### 什么是 AJAX ？

- AJAX 代表异步的 JavaScript 和 XML（**A**synchronous **J**avaScript **A**nd **X**ML）。简单点说，就是使用  `XMLHttpRequest`对象与服务器通信

- 它可以使用 JSON、XML、HTML 和文本文件等格式发送和接收数据。AJAX 最吸引人的就是它的“异步”特性，也就是说它可以在不重新刷新页面的情况下与服务器通信，交换数据，或更新页面。

- 尽管 Ajax 中的 X 代表 XML，但是  JSON 才是首选，因为它更加轻量，而且是用 JavaScript 编写的。在 Ajax 模型中，JSON 和 XML 都被用来包装信息

你可以使用 AJAX 最主要的两个特性做下列事：

- 在不重新加载页面的情况下发送请求给服务器。
- 接收并使用从服务器发来的数据。

### 第一步——发送 HTTP 请求

- 为了使用 JavaScript 向服务器发送一个  HTTP 请求，你需要一个包含必要函数功能的对象实例。这就是为什么会有  `XMLHttpRequest`  的原因。

```js
const httpRequest = new XMLHttpRequest();
```

- 发送一个请求后，你会收到响应。在这一阶段，你要告诉  `XMLHttpRequest`  对象由哪一个 JavaScript 函数处理响应，在设置了对象的  `onreadystatechange`  属性后给它命名，当请求状态改变时调用函数，像这样：

```js
function handler() {
  // 在这里处理服务器响应。
}

httpRequest.onreadystatechange = handler;
```

- 要注意的是，函数名后没有括号和参数，因为这是把一个引用赋值给了函数，而不是真正的调用了它。此外，如果不使用函数名的方式，你还可以用 JavaScript 的匿名函数响应处理的动作，就像下面这样：

```js
httpRequest.onreadystatechange = () => {
  // 在这里处理服务器响应。
};
```

- 接下来，声明当你接到响应后要做什么，你要通过调用 HTTP 请求对象的  `open()`  和  `send()`  方法发送一个实际的请求，像下面这样：

```js
httpRequest.open("GET", "http://www.example.org/some.file", true);
httpRequest.send();
```

- `open()`  的第一个参数是 HTTP 请求方法——GET，POST，HEAD 以及服务器支持的其他方法。根据 HTTP 标准的要求，保证这些方法一定要是大写字母，否则其他一些浏览器（比如 FireFox）可能无法处理这个请求。

- 第二个参数是你要发送请求的 URL。由于安全原因，默认不能调用第三方 URL 域名。确保你在页面中使用的是正确的域名，否则在调用  `open()`  方法时会有 "permission denied" 错误提示。一个容易犯的错误是你企图通过  `domain.tld`  访问网站，而不是使用  `www.domain.tld`。

- 第三个参数是可选的，用于设置请求是否是异步的。如果设为  `true`（默认值），即开启异步，JavaScript 就不会在此语句阻塞，使得用户能在服务器还没有响应的情况下与页面进行交互。这就是 AJAX 中的第一个 A

### 第二步——处理服务器响应

- 在发送请求时，你提供的 JavaScript 函数名负责处理响应：

```js
httpRequest.onreadystatechange = nameOfTheFunction;
```

- 这个函数应该做什么？首先，函数要检查请求的状态。如果状态的值是  `XMLHttpRequest.DONE` （对应的值是 4），意味着服务器响应收到了并且是没问题的，然后就可以继续执行

```js
if (httpRequest.readyState === XMLHttpRequest.DONE) {
  // 很好，服务器已经接收到了响应。
} else {
  // 还没准备好。
}
```

- 全部  `readyState`  状态值

  - 0（未初始化）或（**请求还未初始化**）
  - 1（正在加载）或（**已建立服务器链接**）
  - 2（已加载）或（**请求已接收**）
  - 3（交互）或（**正在处理请求**）
  - 4（完成）或（**请求已完成并且响应已准备好**）

- 接下来，检查 HTTP 响应的 响应状态码。在下面的例子中，我们通过检查响应码  `200 OK` 判断 AJAX 调用有没有成功。

```
if (httpRequest.status === 200) {
  // 完美！
} else {
  // 请求有问题。
  // 比如，响应可能是 404 (Not Found)
  // 或 500 (Internal Server Error) 响应码。
}
```

- 在检查完请求状态和 HTTP 响应码后，你就可以用服务器返回的数据做任何你想做的了。你有两个方法去访问这些数据：

- `httpRequest.responseText`：以文本字符串的方式返回服务器响应。
- `httpRequest.responseXML`：以  `XMLDocument`  对象的形式返回服务器响应，你可以使用 JavaScript DOM 函数来遍历它。

注意上面这一步只在你发起异步请求时有效（即  `open()`  的第三个参数未特别指定或设为  `true`）。如果你发起的是**同步**请求则不必使用函数，但是非常不推荐这样做，它的用户体验很糟糕。

### 第三步——简单的示例

- 让我们把所有的知识都集中起来做一个简单的 HTTP 请求。这个 JavaScript 会请求一个 HTML 文档  `test.html`，包含文本内容“I'm a test”。然后我们  `alert()`  响应的内容。注意这个例子我们只是用了原生 JavaScript，没有用 jQuery。而且，HTML、XML 和 PHP 文件都要放在同一个目录下。

```js
<button id="ajaxButton" type="button">发送请求</button>

<script>
  (() => {
    let httpRequest;
    document
      .getElementById("ajaxButton")
      .addEventListener("click", makeRequest);
    function makeRequest() {
      httpRequest = new XMLHttpRequest();
      if (!httpRequest) {
        alert("放弃了 :( 不能创建 XMLHTTP 实例");
        return false;
      }
      httpRequest.onreadystatechange = alertContents;
      httpRequest.open("GET", "test.html");
      httpRequest.send();
    }
    function alertContents() {
      if (httpRequest.readyState === XMLHttpRequest.DONE) {
        if (httpRequest.status === 200) {
          alert(httpRequest.responseText);
        } else {
          alert("请求遇到了问题。");
        }
      }
    }
  })();
</script>
```

在这个例子中：

- 用户点击“发送请求”按钮；
- 事件处理器调用  `makeRequest()`  函数；
- 请求已通过然后（`onreadystatechange`）传给  `alertContents()`  执行。
- `alertContents()`  检查返回的响应是否 OK，然后  `alert()`  文件  `test.html`  的内容。

### 第四步——处理数据

- 在上一个例子中，在收到 HTTP 请求的响应后我们会使用对象的  `responseText`  属性，包含  `test.html`  文件的内容。现在我们试试  `responseXML`  属性。

- 首先，我们创建一个稍后将要请求的有效的 XML 文档。文档（`test.xml`）包含以下内容：

```
<?xml version="1.0" ?>
<root> 我是测试文字。 </root>
```

- 然后，在  `makeRequest()`  函数中，我们需要把  `text.html`  换成我们刚创建的 XML 文件：

```
httpRequest.open("GET", "test.xml");
```

- 然后在  `alertContents()`  里，我们把  `alert(httpRequest.responseText);`  改为：

```
const xmldoc = httpRequest.responseXML;
const root_node = xmldoc.querySelector("root");
alert(root_node.firstChild.data);
```

- 这部分代码采用  `responseXML`  提供的  `XMLDocument`  对象，并使用 DOM 方法访问 XML 文档中包含的一些数据。

### 第五步——处理数据

- 最后，我们发送一个数据给服务器并收到响应。这次我们用 JavaScript 请求动态页面  `test.php`  并返回一个计算后的字符串——“你好，[user data]”，并  `alert()`  出来。

- 首先要添加一个文本到 HTML 中以方便用户输入名字：

```
<label>
  你的名字：
  <input type="text" id="ajaxTextbox" />
</label>
<span id="ajaxButton" style="cursor: pointer; text-decoration: underline">
  发出请求
</span>
```

- 我们还将在事件处理程序中添加一行，从文本框中获取用户的数据，并将其与服务器端脚本的 URL 一起发送给  `makeRequest()`  函数：

```
document.getElementById("ajaxButton").onclick = () => {
  const userName = document.getElementById("ajaxTextbox").value;
  makeRequest("test.php", userName);
};
```

- 我们还要修改  `makeRequest()`  让它接受用户数据并将其发给服务器。把请求方法从  `GET`  改为  `POST`，把数据作为参数让  `httpRequest.send()`  调用。

```
function makeRequest(url, userName) {
  // …

  httpRequest.onreadystatechange = alertContents;
  httpRequest.open("POST", url);
  httpRequest.setRequestHeader(
    "Content-Type",
    "application/x-www-form-urlencoded"
  );
  httpRequest.send(`userName=${encodeURIComponent(userName)}`);
}
```

- `alertContents()`  函数可以使用第三步中的相同函数写，而服务器会返回计算后的内容和原内容。所以，如果用户在输入框中输入“Jane”，那服务器就会返回如下内容：

```
{ "userData": "Jane", "computedString": "Hi, Jane!" }
```

- 为了在  `alertContents()`  中使用这个数据，我们可不能只是 alert `responseText`，我们要解析它并 alert `computedString`，这才是我们想要的属性：

```
function alertContents() {
  if (httpRequest.readyState === XMLHttpRequest.DONE) {
    if (httpRequest.status === 200) {
      const response = JSON.parse(httpRequest.responseText);
      alert(response.computedString);
    } else {
      alert("请求出现了问题。");
    }
  }
}
```

- `test.php`  文件应该包含以下内容：

```
$name = $_POST['userName'] ?? 'no name';
$computedString = "Hi, " . $name . "!";
$array = ['userName' => $name, 'computedString' => $computedString];
echo json_encode($array);
```

## 深入 回调函数

- **函数被作为实参传入另一函数，并在该外部函数内被调用**，用以来完成某些任务的函数，称为回调函数。

例如：

```js
function greeting(name) {
  alert("Hello " + name);
}

function processUserInput(callback) {
  var name = prompt("Please enter your name.");
  callback(name);
}

processUserInput(greeting);
```

- 以上示例为同步回调，它是立即执行的

- 然而需要注意的是，回调函数经常被用于在一个异步操作完成后执行代码，它们被称为异步回调。一个常见的例子是在 promise 末尾添加的 `.then` 内执行回调函数（在 promise 被兑现或拒绝时执行）。这个结构常用于许多现代的 web API, 例如 `fetch()`

## 深入 回调地狱

根据我们在回调函数和异步任务中的内容可以得出一个结论：存在异步任务的代码，不能保证按照顺序执行，那如果非要代码顺序执行呢？ **回调函数中嵌套回调函数的情况就叫做回调地狱**。 回调地狱就是为是实现代码顺序执行而出现的一种操作，它会造成我们的代码可读性非常差，后期不好维护

## 深入 Promise

- **`Promise`** **对象**用于表示一个异步操作的最终完成（或失败）及其结果值

### 描述

- 一个  `Promise`  对象代表一个在这个 promise 被创建出来时不一定已知值的代理。**它让你能够把异步操作最终的成功返回值或者失败原因和相应的处理程序关联起来。这样使得异步方法可以像同步方法那样返回值：异步方法并不会立即返回最终的值，而是会返回一个  *promise*，以便在未来某个时候把值交给使用者**。

- 一个  `Promise`  必然处于以下几种状态之一：

  - _待定（pending）_：初始状态，既没有被兑现，也没有被拒绝。
  - _已兑现（fulfilled）_：意味着操作成功完成。
  - _已拒绝（rejected）_：意味着操作失败。

- 待定状态的 Promise 对象要么会通过一个值被兑现，要么会通过一个原因（错误）_被拒绝_。当这些情况之一发生时，我们用 promise 的  `then`  方法排列起来的相关处理程序就会被调用。如果 promise 在一个相应的处理程序被绑定时就已经被兑现或被拒绝了，那么这个处理程序也同样会被调用，因此在完成异步操作和绑定处理方法之间不存在竞态条件。

![Screenshot 2023-04-17 at 5.23.45 PM.png](https://s2.loli.net/2023/04/17/VRT35L9afQAPtFW.png)

- 本质上 Promise 是一个函数返回的对象，我们可以在它上面绑定回调函数，这样我们就不需要在一开始把回调函数作为参数传入这个函数了

- 假设现在有一个名为  `createAudioFileAsync()`  的函数，它接收一些配置和两个回调函数，然后异步地生成音频文件。一个回调函数在文件成功创建时被调用，另一个则在出现异常时被调用。

以下为使用  `createAudioFileAsync()`  的示例：

```js
// 成功的回调函数
function successCallback(result) {
  console.log("音频文件创建成功：" + result);
}

// 失败的回调函数
function failureCallback(error) {
  console.log("音频文件创建失败：" + error);
}

createAudioFileAsync(audioSettings, successCallback, failureCallback);
```

- 更现代的函数会返回一个 Promise 对象，使得你可以将你的回调函数绑定在该 Promise 上。

- 如果函数  `createAudioFileAsync()`  被重写为返回 Promise 的形式，那么我们可以像下面这样简单地调用它：

```js
const promise = createAudioFileAsync(audioSettings);
promise.then(successCallback, failureCallback);
```

或者简写为：

```js
createAudioFileAsync(audioSettings).then(successCallback, failureCallback);
```

我们把这个称为  **_异步函数调用_**，这种形式有若干优点，下面我们将会逐一讨论

### 约定

不同于“老式”的传入回调，在使用 Promise 时，会有以下约定：

- 在本轮  **事件循环** 运行完成之前，回调函数是不会被调用的。
- 即使异步操作已经完成（成功或失败），在这之后通过  `then()` 添加的回调函数也会被调用。
- 通过多次调用  `then()` 可以添加多个回调函数，它们会按照插入顺序进行执行。

Promise 很棒的一点就是**链式调用**（**chaining**）

### 链式调用

**连续执行两个或者多个异步操作是一个常见的需求，在上一个操作执行成功之后，开始下一个的操作，并带着上一步操作所返回的结果**。我们可以通过创造一个  **Promise 链**来实现这种需求。

见证奇迹的时刻：`then()`  函数会返回一个和原来不同的**新的 Promise**：

```js
const promise = doSomething();
const promise2 = promise.then(successCallback, failureCallback);
```

或者

```js
const promise2 = doSomething().then(successCallback, failureCallback);
```

`promise2`  不仅表示  `doSomething()`  函数的完成，也代表了你传入的  `successCallback`  或者  `failureCallback`  的完成，这两个函数也可以返回一个 Promise 对象，从而形成另一个异步操作，这样的话，在  `promise2`  上新增的回调函数会排在这个 Promise 对象的后面。

基本上，每一个 Promise 都代表了链中另一个异步过程的完成。

在过去，要想做多重的异步操作，会导致经典的回调地狱：

```js
doSomething(function (result) {
  doSomethingElse(
    result,
    function (newResult) {
      doThirdThing(
        newResult,
        function (finalResult) {
          console.log("Got the final result: " + finalResult);
        },
        failureCallback
      );
    },
    failureCallback
  );
}, failureCallback);
```

现在，我们可以把回调绑定到返回的 Promise 上，形成一个 Promise 链：

```js
doSomething()
  .then(function (result) {
    return doSomethingElse(result);
  })
  .then(function (newResult) {
    return doThirdThing(newResult);
  })
  .then(function (finalResult) {
    console.log("Got the final result: " + finalResult);
  })
  .catch(failureCallback);
```

then 里的参数是可选的，`catch(failureCallback)`  是  `then(null, failureCallback)`  的缩略形式。如下所示，我们也可以用 **箭头函数** 来表示：

```js
doSomething()
  .then((result) => doSomethingElse(result))
  .then((newResult) => doThirdThing(newResult))
  .then((finalResult) => {
    console.log(`Got the final result: ${finalResult}`);
  })
  .catch(failureCallback);
```

**注意：一定要有返回值，否则，callback 将无法获取上一个 Promise 的结果。(如果使用箭头函数，`() => x`  比  `() => { return x; }`  更简洁一些，但后一种保留  `return`  的写法才支持使用多个语句。**

#### Catch 的后续链式操作

有可能会在一个回调失败之后继续使用链式操作，即，使用一个  `catch`，这对于在链式操作中抛出一个失败之后，再次进行新的操作会很有用。请阅读下面的例子：

```js
new Promise((resolve, reject) => {
  console.log("初始化");

  resolve();
})
  .then(() => {
    throw new Error("有哪里不对了");

    console.log("执行「这个」”");
  })
  .catch(() => {
    console.log("执行「那个」");
  })
  .then(() => {
    console.log("执行「这个」，无论前面发生了什么");
  });

/*输出结果如下：
  初始化
  执行“那个”
  执行“这个”，无论前面发生了什么*/
```

注意：**因为抛出了错误** 有哪里不对了，所以前一个  **执行「这个」**  没有被输出。

### 错误传递

- 在之前的回调地狱示例中，你可能记得有 3 次  `failureCallback`  的调用，而在 Promise 链中只有尾部的一次调用。

```js
doSomething()
  .then((result) => doSomethingElse(result))
  .then((newResult) => doThirdThing(newResult))
  .then((finalResult) => console.log(`Got the final result: ${finalResult}`))
  .catch(failureCallback);
```

通常，一遇到异常抛出，浏览器就会顺着 Promise 链寻找下一个  `onRejected`  失败回调函数或者由  `.catch()`  指定的回调函数。这和以下同步代码的工作原理（执行过程）非常相似。

```js
try {
  let result = syncDoSomething();
  let newResult = syncDoSomethingElse(result);
  let finalResult = syncDoThirdThing(newResult);
  console.log(`Got the final result: ${finalResult}`);
} catch (error) {
  failureCallback(error);
}
```

在 ECMAScript 2017 标准的  `async/await` 语法糖中，这种异步代码的对称性得到了极致的体现：

```js
async function foo() {
  try {
    const result = await doSomething();
    const newResult = await doSomethingElse(result);
    const finalResult = await doThirdThing(newResult);
    console.log(`Got the final result: ${finalResult}`);
  } catch (error) {
    failureCallback(error);
  }
}
```

- 这个例子是在 Promise 的基础上构建的，例如，`doSomething()`  与之前的函数是相同的。通过捕获所有的错误，甚至抛出异常和程序错误，Promise 解决了回调地狱的基本缺陷。这对于构建异步操作的基础功能而言是很有必要的。

### Promise 拒绝事件

当 Promise 被拒绝时，会有下文所述的两个事件之一被派发到全局作用域（通常而言，就是`window`；如果是在 web worker 中使用的话，就是  `Worker` 或者其他 worker-based 接口）。这两个事件如下所示：

`rejectionhandled`

当 Promise 被拒绝、并且在  `reject`  函数处理该 rejection 之后会派发此事件。

`unhandledrejection`

当 Promise 被拒绝，但没有提供  `reject`  函数来处理该 rejection 时，会派发此事件。

以上两种情况中，`PromiseRejectionEvent` 事件都有两个属性，一个是  `promise` 属性，该属性指向被驳回的 Promise，另一个是  `reason` (en-US)  属性，该属性用来说明 Promise 被驳回的原因。

因此，我们可以通过以上事件为 Promise 失败时提供补偿处理，也有利于调试 Promise 相关的问题。在每一个上下文中，该处理都是全局的，因此不管源码如何，所有的错误都会在同一个处理函数中被捕捉并处理。

一个特别有用的例子：当你使用  Node.js 时，有些依赖模块可能会有未被处理的 rejected promises，这些都会在运行时打印到控制台。你可以在自己的代码中捕捉这些信息，然后添加与  `unhandledrejection` 相应的处理函数来做分析和处理，或只是为了让你的输出更整洁。举例如下：

```js
window.addEventListener(
  "unhandledrejection",
  (event) => {
    /* 你可以在这里添加一些代码，以便检查
     event.promise 中的 promise 和
     event.reason 中的 rejection 原因 */

    event.preventDefault();
  },
  false
);
```

调用 event 的  `preventDefault()` 方法是为了告诉 JavaScript 引擎当 Promise 被拒绝时不要执行默认操作，默认操作一般会包含把错误打印到控制台，Node 就是如此的。

理想情况下，在忽略这些事件之前，我们应该检查所有被拒绝的 Promise，来确认这不是代码中的 bug。

### 在旧式回调 API 中创建 Promise

可以通过 Promise 的构造器从零开始创建  `Promise` 。这种方式（通过构造器的方式）应当只在封装旧 API 的时候用到

理想状态下，所有的异步函数都已经返回 Promise 了。但有一些 API 仍然使用旧方式来传入的成功（或者失败）的回调。典型的例子就是  `setTimeout()` (en-US) 函数：

```js
setTimeout(() => saySomething("10 seconds passed"), 10000);
```

混用旧式回调和 Promise 可能会造成运行时序问题。如果  `saySomething`  函数失败了，或者包含了编程错误，那就没有办法捕获它了。这得怪  `setTimeout`。

幸运地是，我们可以用 Promise 来封装它。最好的做法是，将这些有问题的函数封装起来，留在底层，并且永远不要再直接调用它们：

```
const wait = ms => new Promise(resolve => setTimeout(resolve, ms));

wait(10000).then(() => saySomething("10 seconds")).catch(failureCallback);
```

通常，Promise 的构造器接收一个执行函数 (executor)，我们可以在这个执行函数里手动地 resolve 和 reject 一个 Promise。既然  `setTimeout`  并不会真的执行失败，那么我们可以在这种情况下忽略 reject

### 组合

`Promise.resolve()` 和  `Promise.reject()` 是手动创建一个已经 resolve 或者 reject 的 Promise 快捷方法。它们有时很有用。

`Promise.all()`和  `Promise.race()`是并行运行异步操作的两个组合式工具。

我们可以发起并行操作，然后等多个操作全部结束后进行下一步操作，如下：

```js
Promise.all([func1(), func2(), func3()]).then(([result1, result2, result3]) => {
  /* use result1, result2 and result3 */
});
```

可以使用一些聪明的 JavaScript 写法实现时序组合：

```js
[func1, func2, func3]
  .reduce((p, f) => p.then(f), Promise.resolve())
  .then((result3) => {
    /* use result3 */
  });
```

通常，我们递归调用一个由异步函数组成的数组时，相当于一个 Promise 链：

Promise.resolve().then(func1).then(func2).then(func3);

我们也可以写成可复用的函数形式，这在函数式编程中极为普遍：

```js
const applyAsync = (acc, val) => acc.then(val);
const composeAsync =
  (...funcs) =>
  (x) =>
    funcs.reduce(applyAsync, Promise.resolve(x));
```

`composeAsync()`  函数将会接受任意数量的函数作为其参数，并返回一个新的函数，该函数接受一个通过 composition pipeline 传入的初始值。这对我们来说非常有益，因为任一函数可以是异步或同步的，它们能被保证按顺序执行：

```js
const transformData = composeAsync(func1, func2, func3);
const result3 = transformData(data);
```

在 ECMAScript 2017 标准中，时序组合可以通过使用  `async/await`  而变得更简单：

```
let result;
for (const f of [func1, func2, func3]) {
  result = await f(result);
}
/* use last result (i.e. result3) */
```

### 时序

为了避免意外，即使是一个已经变成 resolve 状态的 Promise，传递给  `then()`  的函数也总是会被异步调用：

```js
Promise.resolve().then(() => console.log(2));
console.log(1); // 1, 2
```

传递到  `then()`  中的函数被置入到一个微任务队列中，而不是立即执行，这意味着它是在 JavaScript 事件队列的所有运行时结束了，且事件队列被清空之后，才开始执行：

```js
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

wait().then(() => console.log(4));
Promise.resolve()
  .then(() => console.log(2))
  .then(() => console.log(3));
console.log(1); // 1, 2, 3, 4
```

### 嵌套

简便的 Promise 链式编程最好保持扁平化，不要嵌套 Promise，因为嵌套经常会是粗心导致的。可查阅下一节的 常见错误 中的例子。

嵌套 Promise 是一种可以限制  `catch`  语句的作用域的控制结构写法。明确来说，嵌套的  `catch`  仅捕捉在其之前同时还必须是其作用域的 failureres，而捕捉不到在其链式以外或者其嵌套域以外的 error。如果使用正确，那么可以实现高精度的错误修复。

```js
doSomethingCritical()
  .then((result) =>
    doSomethingOptional()
      .then((optionalResult) => doSomethingExtraNice(optionalResult))
      .catch((e) => {
        console.log(e.message);
      })
  ) // 即使有异常也会忽略，继续运行;(最后会输出)
  .then(() => moreCriticalStuff())
  .catch((e) => console.log("Critical failure: " + e.message)); // 没有输出
```

注意，有些代码步骤是嵌套的，而不是一个简单的纯链式，这些语句前与后都被括号  `()`  包裹着。

这个内部的  `catch`  语句仅能捕获到  `doSomethingOptional()`  和  `doSomethingExtraNice()`  的失败，`之后就恢复到 moreCriticalStuff()`  的运行。重要提醒：如果  `doSomethingCritical()`  失败，这个错误仅会被最后的（外部）`catch`  语句捕获到。

### 常见错误

在编写 Promise 链时，需要注意以下示例中展示的几个错误：

```js
// 错误示例，包含 3 个问题！

doSomething()
  .then(function (result) {
    doSomethingElse(result) // 没有返回 Promise 以及没有必要的嵌套 Promise
      .then((newResult) => doThirdThing(newResult));
  })
  .then(() => doFourthThing());
// 最后，是没有使用 catch 终止 Promise 调用链，可能导致没有捕获的异常
```

第一个错误是没有正确地将事物相连接。当我们创建新 Promise 但忘记返回它时，会发生这种情况。因此，链条被打破，或者更确切地说，我们有两个独立的链条竞争（同时在执行两个异步而非一个一个的执行）。这意味着  `doFourthThing()`  不会等待  `doSomethingElse()`  或  `doThirdThing()`  完成，并且将与它们并行运行，可能是无意的。单独的链也有单独的错误处理，导致未捕获的错误。

第二个错误是不必要地嵌套，实现第一个错误。嵌套还限制了内部错误处理程序的范围，如果是非预期的，可能会导致未捕获的错误。其中一个变体是  Promise 构造函数 反模式，它结合了 Promise 构造函数的多余使用和嵌套。

第三个错误是忘记用  `catch`  终止链。这导致在大多数浏览器中不能终止的 Promise 链里的 rejection。

一个好的经验法则是总是返回或终止 Promise 链，并且一旦你得到一个新的 Promise，返回它。下面是修改后的平面化的代码：

```js
doSomething()
  .then(function (result) {
    return doSomethingElse(result);
  })
  .then((newResult) => doThirdThing(newResult))
  .then(() => doFourthThing())
  .catch((error) => console.log(error));
```

注意：`() => x`  是  `() => { return x; }`  的简写。

上述代码的写法就是具有适当错误处理的简单明确的链式写法。

## 深入 Fetch API

### 基本概念

- Fetch 是一个现代的概念，等同于 XMLHttpRequest，它提供了许多与 XMLHttpRequest 相同的功能，但被设计成更具可扩展性和高效性。本文介绍了 Fetch API 的一些基本概念

- Fetch 的核心在于对 HTTP 接口的抽象，包括  `Request`，`Response`，`Headers` ，`Body`，以及用于初始化异步请求的  `global fetch` 。得益于 JavaScript 实现的这些抽象好的 HTTP 模块，其他接口能够很方便的使用这些功能

- 除此之外，Fetch 还利用到了请求的异步特性——它是基于  `Promise`  的

### 使用 Fetch

#### 基本使用

Fetch API 提供了一个 JavaScript 接口，用于访问和操纵 HTTP 管道的一些具体部分，例如请求和响应。它还提供了一个全局  `fetch()` 方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源

这种功能以前是使用  `XMLHttpRequest`实现的。Fetch 提供了一个更理想的替代方案，可以很容易地被其他技术使用，例如  `Service Workers`。Fetch 还提供了专门的逻辑空间来定义其他与 HTTP 相关的概念，例如  CORS 和 HTTP 的扩展。

请注意，`fetch`  规范与  `jQuery.ajax()`  主要有以下的不同：

- 当接收到一个代表错误的 HTTP 状态码时，从  `fetch()`  返回的 Promise **不会被标记为 reject**，即使响应的 HTTP 状态码是 404 或 500。相反，它会将 Promise 状态标记为 resolve（如果响应的 HTTP 状态码不在 200 - 299 的范围内，则设置 resolve 返回值的  `ok` 属性为 false），仅当网络故障时或请求被阻止时，才会标记为 reject。
- `fetch` **不会发送跨域 cookie**，除非你使用了  *credentials*  的 初始化选项 。（自  2018 年 8 月 以后，默认的 credentials 政策变更为  `same-origin`。Firefox 也在 61.0b13 版本中进行了修改）

一个基本的 fetch 请求设置起来很简单。看看下面的代码：

```js
fetch("http://example.com/movies.json")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

这里我们通过网络获取一个 JSON 文件并将其打印到控制台。最简单的用法是只提供一个参数用来指明想  `fetch()`  到的资源路径，然后返回一个包含响应结果的 promise（一个   `Response` 对象）。

当然它只是一个 HTTP 响应，而不是真的 JSON。为了获取 JSON 的内容，我们需要使用  `json()`  方法（该方法返回一个将响应 body 解析成 JSON 的 promise）

##### 支持的请求参数

`fetch()`  接受第二个可选参数，一个可以控制不同配置的  `init`  对象：

参考  `fetch()`，查看所有可选的配置和更多描述。

```js
// Example POST method implementation:
async function postData(url = "", data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
    cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
    credentials: "same-origin", // include, *same-origin, omit
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: "follow", // manual, *follow, error
    referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify(data), // body data type must match "Content-Type" header
  });
  return response.json(); // parses JSON response into native JavaScript objects
}

postData("https://example.com/answer", { answer: 42 }).then((data) => {
  console.log(data); // JSON data parsed by `data.json()` call
});
```

注意：`mode: "no-cors"`  仅允许使用一组有限的 HTTP 请求头：

- `Accept`
- `Accept-Language`
- `Content-Language`
- `Content-Type`  允许使用的值为：`application/x-www-form-urlencoded`、`multipart/form-data`  或  `text/plain`

##### 发送带凭据的请求

为了让浏览器发送包含凭据的请求（即使是跨域源），要将  `credentials: 'include'`  添加到传递给  `fetch()`  方法的  `init`  对象。

```js
fetch("https://example.com", {
  credentials: "include",
});
```

如果你只想在请求 URL 与调用脚本位于同一起源处时发送凭据，请添加  `credentials: 'same-origin'`。

```js
// The calling script is on the origin 'https://example.com'

fetch("https://example.com", {
  credentials: "same-origin",
});
```

要改为确保浏览器不在请求中包含凭据，请使用  `credentials: 'omit'`。

```js
fetch("https://example.com", {
  credentials: "omit",
});
```

##### 上传 JSON 数据

使用  `fetch()` POST JSON 数据

```js
const data = { username: "example" };

fetch("https://example.com/profile", {
  method: "POST", // or 'PUT'
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

##### 上传文件

可以通过 HTML `<input type="file" />`  元素，`FormData()`  和  `fetch()`上传文件。

```js
const formData = new FormData();
const fileField = document.querySelector('input[type="file"]');

formData.append("username", "abc123");
formData.append("avatar", fileField.files[0]);

fetch("https://example.com/profile/avatar", {
  method: "PUT",
  body: formData,
})
  .then((response) => response.json())
  .then((result) => {
    console.log("Success:", result);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

##### 上传多个文件

可以通过 HTML `<input type="file" multiple />`  元素，`FormData()` 和  `fetch()` 上传文件。

```js
const formData = new FormData();
const photos = document.querySelector('input[type="file"][multiple]');

formData.append("title", "My Vegas Vacation");
for (let i = 0; i < photos.files.length; i++) {
  formData.append(`photos_${i}`, photos.files[i]);
}

fetch("https://example.com/posts", {
  method: "POST",
  body: formData,
})
  .then((response) => response.json())
  .then((result) => {
    console.log("Success:", result);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

##### 逐行处理文本文件

从响应中读取的分块不是按行分割的，并且是  `Uint8Array`  数组类型（不是字符串类型）。如果你想通过  `fetch()`  获取一个文本文件并逐行处理它，那需要自行处理这些复杂情况。以下示例展示了一种创建行迭代器来处理的方法（简单起见，假设文本是 UTF-8 编码的，且不处理  `fetch()`  的错误）。

```js
async function* makeTextFileLineIterator(fileURL) {
  const utf8Decoder = new TextDecoder("utf-8");
  const response = await fetch(fileURL);
  const reader = response.body.getReader();
  let { value: chunk, done: readerDone } = await reader.read();
  chunk = chunk ? utf8Decoder.decode(chunk) : "";

  const re = /\n|\r|\r\n/gm;
  let startIndex = 0;
  let result;

  for (;;) {
    let result = re.exec(chunk);
    if (!result) {
      if (readerDone) {
        break;
      }
      let remainder = chunk.substr(startIndex);
      ({ value: chunk, done: readerDone } = await reader.read());
      chunk = remainder + (chunk ? utf8Decoder.decode(chunk) : "");
      startIndex = re.lastIndex = 0;
      continue;
    }
    yield chunk.substring(startIndex, result.index);
    startIndex = re.lastIndex;
  }
  if (startIndex < chunk.length) {
    // last line didn't end in a newline char
    yield chunk.substr(startIndex);
  }
}

async function run() {
  for await (let line of makeTextFileLineIterator(urlOfFile)) {
    processLine(line);
  }
}

run();
```

##### 检测请求是否成功

如果遇到网络故障或服务端的 CORS 配置错误时，`fetch()` promise 将会 reject，带上一个  `TypeError`对象。虽然这个情况经常是遇到了权限问题或类似问题——比如 404 不是一个网络故障。想要精确的判断  `fetch()`  是否成功，需要包含 promise resolved 的情况，此时再判断  `Response.ok` 是否为 true。类似以下代码：

```js
fetch("flowers.jpg")
  .then((response) => {
    if (!response.ok) {
      throw new Error("Network response was not OK");
    }
    return response.blob();
  })
  .then((myBlob) => {
    myImage.src = URL.createObjectURL(myBlob);
  })
  .catch((error) => {
    console.error("There has been a problem with your fetch operation:", error);
  });
```

##### 自定义请求对象

除了传给  `fetch()`  一个资源的地址，你还可以通过使用  `Request()` 构造函数来创建一个 request 对象，然后再作为参数传给  `fetch()`：

```js
const myHeaders = new Headers();

const myRequest = new Request("flowers.jpg", {
  method: "GET",
  headers: myHeaders,
  mode: "cors",
  cache: "default",
});

fetch(myRequest)
  .then((response) => response.blob())
  .then((myBlob) => {
    myImage.src = URL.createObjectURL(myBlob);
  });
```

`Request()`  和  `fetch()`  接受同样的参数。你甚至可以传入一个已存在的 request 对象来创造一个拷贝：

```
const anotherRequest = new Request(myRequest, myInit);
```

这个很有用，因为 request 和 response bodies 只能被使用一次（译者注：这里的意思是因为设计成了 stream 的方式，所以它们只能被读取一次）。创建一个拷贝就可以再次使用 request/response 了，当然也可以使用不同的  `init`  参数。创建拷贝必须在读取 body 之前进行，而且读取拷贝的 body 也会将原始请求的 body 标记为已读。

#### Headers

使用  `Headers` 的接口，你可以通过  `Headers()` 构造函数来创建一个你自己的 headers 对象。一个 headers 对象是一个简单的多键值对：

```js
const content = "Hello World";
const myHeaders = new Headers();
myHeaders.append("Content-Type", "text/plain");
myHeaders.append("Content-Length", content.length.toString());
myHeaders.append("X-Custom-Header", "ProcessThisImmediately");
```

也可以传入一个多维数组或者对象字面量：

```js
const myHeaders = new Headers({
  "Content-Type": "text/plain",
  "Content-Length": content.length.toString(),
  "X-Custom-Header": "ProcessThisImmediately",
});
```

它的内容可以被获取：

```js
console.log(myHeaders.has("Content-Type")); // true
console.log(myHeaders.has("Set-Cookie")); // false
myHeaders.set("Content-Type", "text/html");
myHeaders.append("X-Custom-Header", "AnotherValue");

console.log(myHeaders.get("Content-Length")); // 11
console.log(myHeaders.get("X-Custom-Header")); // ['ProcessThisImmediately', 'AnotherValue']

myHeaders.delete("X-Custom-Header");
console.log(myHeaders.get("X-Custom-Header")); // null
```

虽然一些操作只能在  `ServiceWorkers` 中使用，但是它提供了更方便的操作 Headers 的 API。

如果使用了一个不合法的 HTTP Header 属性名，那么 Headers 的方法通常都抛出 TypeError 异常。如果不小心写入了一个不可写的属性（见下方），也会抛出一个 TypeError 异常。除此以外的情况，失败了并不抛出异常。例如：

```js
const myResponse = Response.error();
try {
  myResponse.headers.set("Origin", "http://mybank.com");
} catch (e) {
  console.log("Cannot pretend to be a bank!");
}
```

最好在在使用之前检查内容类型  `content-type`  是否正确，比如：

```js
fetch(myRequest)
  .then((response) => {
    const contentType = response.headers.get("content-type");
    if (!contentType || !contentType.includes("application/json")) {
      throw new TypeError("Oops, we haven't got JSON!");
    }
    return response.json();
  })
  .then((data) => {
    /* process your data further */
  })
  .catch((error) => console.error(error));
```

#### Response 对象

如上所述，`Response`   实例是在  `fetch()`  处理完 promise 之后返回的。

你会用到的最常见的 response 属性有：

- `Response.status`— 整数（默认值为 200）为 response 的状态码。
- `Response.statusText` — 字符串（默认值为 ""），该值与 HTTP 状态码消息对应。注意：HTTP/2  不支持 状态消息
- `Response.ok` — 如上所示，该属性是来检查 response 的状态是否在 200 - 299（包括 200 和 299）这个范围内。该属性返回一个布尔值。

它的实例也可用通过 JavaScript 来创建，但只有在  `ServiceWorkers` 中使用  `respondWith()` 方法并提供了一个自定义的 response 来接受 request 时才真正有用：

```js
const myBody = new Blob();

addEventListener("fetch", (event) => {
  // ServiceWorker intercepting a fetch
  event.respondWith(
    new Response(myBody, {
      headers: { "Content-Type": "text/plain" },
    })
  );
});
```

`Response()` 构造方法接受两个可选参数—— response 的 body 和一个初始化对象（与`Request()`   所接受的 init 参数类似）。

## 深入 async / await

### async 函数

- async 函数是**使用`async`关键字声明的函数**。async 函数是  `AsyncFunction`   构造函数的实例，并且其中允许使用  `await`  关键字。`async`  和  `await`  关键字让我们可以用一种更简洁的方式写出基于  `Promise` 的异步行为，而无需刻意地链式调用  `promise`。

- async 函数还可以被 **作为表达式** 来定义

#### 语法

```js
async function name(param0) {
  statements;
}
async function name(param0, param1) {
  statements;
}
async function name(param0, param1, /* … ,*/ paramN) {
  statements;
}
```

`name` - 函数名称

`param`  - (可选) 要传递给函数的参数的名称。

`statements` - (可选) 包含函数主体的表达式。可以使用  `await`  机制。

返回值：一个  `Promise`，这个 promise 要么会通过一个由 async 函数返回的值被解决，要么会通过一个从 async 函数中抛出的（或其中没有被捕获到的）异常被拒绝

#### 描述

async 函数可能包含 0 个或者多个  `await` 表达式。await 表达式会暂停整个 async 函数的执行进程并出让其控制权，只有当其等待的基于 promise 的异步操作被兑现或被拒绝之后才会恢复进程。promise 的解决值会被当作该 await 表达式的返回值。使用  `async`/`await`  关键字就可以在异步代码中使用普通的  `try`/`catch`  代码块。

- `await`关键字只在 async 函数内有效。如果你在 async 函数体之外使用它，就会抛出语法错误  `SyntaxError`

- `async`/`await`的目的为了简化使用基于 promise 的 API 时所需的语法。`async`/`await`  的行为就好像搭配使用了生成器和 promise。

async 函数一定会返回一个 promise 对象。如果一个 async 函数的返回值看起来不是 promise，那么它将会被隐式地包装在一个 promise 中。

例如，如下代码：

```js
async function foo() {
  return 1;
}
```

等价于：

```js
function foo() {
  return Promise.resolve(1);
}
```

async 函数的函数体可以被看作是由 0 个或者多个 await 表达式分割开来的。从第一行代码直到（并包括）第一个 await 表达式（如果有的话）都是同步运行的。这样的话，**一个不含 await 表达式的 async 函数是会同步运行的。然而，如果函数体内有一个 await 表达式，async 函数就一定会异步执行。**

例如：

```js
async function foo() {
  await 1;
}
```

等价于

```js
function foo() {
  return Promise.resolve(1).then(() => undefined);
}
```

在 await 表达式之后的代码可以被认为是存在在链式调用的 then 回调中，多个 await 表达式都将加入链式调用的 then 回调中，返回值将作为最后一个 then 回调的返回值。

在接下来的例子中，我们将使用 await 执行两次 promise，整个  `foo`  函数的执行将会被分为三个阶段。

1.  `foo`  函数的第一行将会同步执行，await 将会等待 promise 的结束。然后暂停通过  `foo`  的进程，并将控制权交还给调用  `foo`  的函数。
2.  一段时间后，当第一个 promise 完结的时候，控制权将重新回到 foo 函数内。示例中将会将`1`（promise 状态为 fulfilled）作为结果返回给 await 表达式的左边即  `result1`。接下来函数会继续进行，到达第二个 await 区域，此时  `foo`  函数的进程将再次被暂停。
3.  一段时间后，同样当第二个 promise 完结的时候，`result2`  将被赋值为  `2`，之后函数将会正常同步执行，将默认返回`undefined` 。

```js
async function foo() {
  const result1 = await new Promise((resolve) =>
    setTimeout(() => resolve("1"))
  );
  const result2 = await new Promise((resolve) =>
    setTimeout(() => resolve("2"))
  );
}
foo();
```

注意：promise 链不是一次就构建好的，相反，promise 链是分阶段构造的，因此在处理异步函数时必须注意对错误函数的处理。

例如，在下面代码中，即使在 promise 链中进一步配置了  `.catch`  方法处理，也会抛出一个未处理的 promise 被拒绝的错误。这是因为  `p2`  直到控制从  `p1`  返回后才会连接到 promise 链。

```js
async function foo() {
  const p1 = new Promise((resolve) => setTimeout(() => resolve("1"), 1000));
  const p2 = new Promise((_, reject) => setTimeout(() => reject("2"), 500));
  const results = [await p1, await p2]; // 不推荐使用这种方式，请使用 Promise.all 或者 Promise.allSettled
}
foo().catch(() => {}); // 捕捉所有的错误...
```

#### 示例

##### 简单例子

```js
function resolveAfter2Seconds() {
  console.log("starting slow promise");
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("slow");
      console.log("slow promise is done");
    }, 2000);
  });
}

function resolveAfter1Second() {
  console.log("starting fast promise");
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("fast");
      console.log("fast promise is done");
    }, 1000);
  });
}

async function sequentialStart() {
  console.log("==SEQUENTIAL START==");

  // 1. Execution gets here almost instantly
  const slow = await resolveAfter2Seconds();
  console.log(slow); // 2. this runs 2 seconds after 1.

  const fast = await resolveAfter1Second();
  console.log(fast); // 3. this runs 3 seconds after 1.
}

async function concurrentStart() {
  console.log("==CONCURRENT START with await==");
  const slow = resolveAfter2Seconds(); // starts timer immediately
  const fast = resolveAfter1Second(); // starts timer immediately

  // 1. Execution gets here almost instantly
  console.log(await slow); // 2. this runs 2 seconds after 1.
  console.log(await fast); // 3. this runs 2 seconds after 1., immediately after 2., since fast is already resolved
}

function concurrentPromise() {
  console.log("==CONCURRENT START with Promise.all==");
  return Promise.all([resolveAfter2Seconds(), resolveAfter1Second()]).then(
    (messages) => {
      console.log(messages[0]); // slow
      console.log(messages[1]); // fast
    }
  );
}

async function parallel() {
  console.log("==PARALLEL with await Promise.all==");

  // Start 2 "jobs" in parallel and wait for both of them to complete
  await Promise.all([
    (async () => console.log(await resolveAfter2Seconds()))(),
    (async () => console.log(await resolveAfter1Second()))(),
  ]);
}

sequentialStart(); // after 2 seconds, logs "slow", then after 1 more second, "fast"

// wait above to finish
setTimeout(concurrentStart, 4000); // after 2 seconds, logs "slow" and then "fast"

// wait again
setTimeout(concurrentPromise, 7000); // same as concurrentStart

// wait again
setTimeout(parallel, 10000); // truly parallel: after 1 second, logs "fast", then after 1 more second, "slow"
```

##### await 和并行

在  `sequentialStart`  中，程序在第一个  `await`  停留了 2 秒，然后又在第二个  `await`  停留了 1 秒。直到第一个计时器结束后，第二个计时器才被创建。程序需要 3 秒执行完毕。

在  `concurrentStart`  中，两个计时器被同时创建，然后执行  `await`。这两个计时器同时运行，这意味着程序完成运行只需要 2 秒，而不是 3 秒，即最慢的计时器的时间。

但是  `await`  仍旧是顺序执行的，第二个  `await`  还是得等待第一个执行完。在这个例子中，这使得先运行结束的输出出现在最慢的输出之后。

如果你希望并行执行两个或更多的任务，你必须像在`parallel`中一样使用`await Promise.all([job1(), job2()])`

##### async/await 和 Promise/then 对比以及错误处理

大多数 async 函数也可以使用 Promises 编写。但是，在错误处理方面，async 函数更容易捕获异常错误

上面例子中的`concurrentStart`函数和`concurrentPromise`函数在功能上都是等效的。在`concurrentStart`函数中，如果任一`await`ed 调用失败，它将自动捕获异常，async 函数执行中断，并通过隐式返回 Promise 将错误传递给调用者。

在 Promise 例子中这种情况同样会发生，该函数必须负责返回一个捕获函数完成的`Promise`。在`concurrentPromise`函数中，这意味着它从`Promise.all([]).then()`返回一个 Promise。事实上，在此示例的先前版本忘记了这样做！

但是，async 函数仍有可能错误地忽略错误。以  `parallel` async 函数为例。如果它没有等待  `await`（或返回）`Promise.all([])`  调用的结果，则不会传播任何错误。虽然  `parallelPromise`  函数示例看起来很简单，但它根本不会处理错误！这样做需要一个类似于  `return Promise.all([])`  处理方式

##### 使用 async 函数重写 promise 链

返回  `Promise` 的 API 将会产生一个 promise 链，它将函数肢解成许多部分。例如下面的代码：

```js
function getProcessedData(url) {
  return downloadData(url) // 返回一个 promise 对象
    .catch((e) => {
      return downloadFallbackData(url); // 返回一个 promise 对象
    })
    .then((v) => {
      return processDataInWorker(v); // 返回一个 promise 对象
    });
}
```

可以重写为单个 async 函数：

```js
async function getProcessedData(url) {
  let v;
  try {
    v = await downloadData(url);
  } catch (e) {
    v = await downloadFallbackData(url);
  }
  return processDataInWorker(v);
}
```

注意，在上述示例中，`return`  语句中没有  `await`  操作符，因为  `async function`  的返回值将被隐式地传递给  `` [`Promise.resolve`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) ``。

返回值`隐式的传递给 Promise.resolve` ，并不意味着`return await promiseValue;和 return promiseValue;`在功能上相同。

看下下面重写的上面代码，在`processDataInWorker`抛出异常时返回了 null：

```
async function getProcessedData(url) {
  let v;
  try {
    v = await downloadData(url);
  } catch(e) {
    v = await downloadFallbackData(url);
  }
  try {
    return await processDataInWorker(v); // 注意 `return await` 和单独 `return` 的比较
  } catch (e) {
    return null;
  }
}
```

简单地写上`return processDataInworker(v);`  将导致在  `processDataInWorker(v)`  出错时 function 返回值为 `Promise` 而不是返回  `null`。`return foo;`  和  `return await foo;`，有一些细微的差异：`return foo;`不管`foo`是 promise 还是 rejects 都将会直接返回`foo`。相反地，如果`foo`是一个`Promise` ，`return await foo;`将等待`foo`执行 (resolve) 或拒绝 (reject)，如果是拒绝，将会在返回前抛出异常。

### await

- `await`  操作符用于等待一个  `Promise` 兑现并获取它兑现之后的值。它只能在 **异步函数** 或者 **模块** 顶层中使用

#### 语法

```js
await expression;
```

参数：expresssion 要等待的  `Promise` 实例，Thenable 对象，或任意类型的值

返回值：返回从  `Promise`  实例或 thenable 对象取得的处理结果。如果等待的值不符合 thenable，则返回表达式本身的值

异常：拒绝（reject）的原因会被作为异常抛出

#### 描述

`await`  通常用于拆开 promise 的包装，使用方法是传递一个  `Promise` 作为  `expression`。使用  `await`  总会暂停当前异步函数的执行，在该  `Promise`  敲定（settled，指兑现或拒绝）后继续执行。函数的执行恢复（resume）时，`await`  表达式的值已经变成了  `Promise`  兑现的值。

若该  `Promise`  被拒绝（rejected），`await`  表达式会把拒绝的原因（reason）抛出。当前函数（`await`  所在的函数）会出现在抛出的错误的 栈追踪 （stack trace），否则当前函数就不会在栈追踪出现。

`await`  总会同步地对表达式求值并处理，处理的行为与  `Promise.resolve()` 一致，不属于原生  `Promise`  的值全都会被隐式地转换为  `Promise`  实例后等待。处理的规则为，若表达式：

- 是一个原生  `Promise`（原生`Promise` 的实例或其派生类的实例，且满足  `expression.constructor === Promise`），会被直接用于等待，等待由原生代码实现，该对象的  `then()`  不会被调用。
- 是 thenable 对象（包括非原生的  `Promise`  实例、polyfill、Proxy、派生类等），会构造一个新  `Promise`  用于等待，构造时会调用该对象的  `then()`  方法。
- 不是 thenable 对象，会被包装进一个已兑现的  `Promise`  用于等待，其结果就是表达式的值。

#### 示例

##### 等待 Promise 的兑现

当一个  `Promise`  被传递给  `await`  操作符，`await`  将等待该  `Promise`  兑现，并在兑现后返回该  `Promise`  兑现的值。

```js
function resolveAfter2Seconds(x) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}

async function f1() {
  let x = await resolveAfter2Seconds(10);
  console.log(x); // 10
}

f1();
```

##### 转换为 promise

若表达式的值不是  `Promise`，`await`  会把该值转换为已兑现的  `Promise`，然后返回其结果

```js
async function f3() {
  const y = await 20;
  console.log(y); // 20

  const obj = {};
  console.log((await obj) === obj); // true
}

f3();
```

##### promise 被拒绝

如果  `Promise`  被拒绝，则抛出拒绝的原因

```js
async function f4() {
  try {
    const z = await Promise.reject(30);
  } catch (e) {
    console.error(e); // 30
  }
}

f4();
```

##### 处理被拒绝的 promise

你可以链式调用  `catch()`（而不是使用  `try`）以在等待 promise 兑现之前处理被拒绝的 promise。

```js
const response = await promisedFunction().catch((err) => {
  console.error(err);
  return "default response";
});
// response will be "default response" if the promise is rejected
```

##### 在顶层使用 await

在 模块 的顶层，你可以单独使用关键字  `await`（异步函数的外面）。也就是说一个模块如果包含用了  `await`  的子模块，该模块就会等待该子模块，这一过程并不会阻塞其他子模块。

下面是一个在  `export` 表达式中使用了  Fetch API 的例子。任何文件只要导入这个模块，后面的代码就会等待，直到 fetch 完成。

```js
// fetch request
const colors = fetch("../data/colors.json").then((response) => response.json());

export default await colors;
```

##### await 对执行过程的影响

当函数执行到  `await`  时，被等待的表达式会立即执行，所有依赖该表达式的值的代码会被暂停，并推送进 微任务队列（microtask queue）。然后主线程被释放出来，用于事件循环中的下一个任务。即使等待的值是已经敲定的 promise 或不是 promise，也会发生这种情况。例如，考虑以下代码：

```js
async function foo(name) {
  console.log(name, "start");
  console.log(name, "middle");
  console.log(name, "end");
}

foo("First");
foo("Second");

// First start
// First middle
// First end
// Second start
// Second middle
// Second end
```

对应到  `Promise`  的写法是：

```js
function foo(name) {
  return new Promise((resolve) => {
    console.log(name, "start");
    console.log(name, "middle");
    console.log(name, "end");
    resolve();
  });
}
```

执行到  `await`  时，后面的代码就会整体被安排进一个新的微任务，此后的函数体变为异步执行。

```js
async function foo(name) {
  console.log(name, "start");
  await console.log(name, "middle");
  console.log(name, "end");
}

foo("First");
foo("Second");

// First start
// First middle
// Second start
// Second middle
// First end
// Second end
```

对应的  `Promise`  写法是：

```js
function foo(name) {
  return new Promise((resolve) => {
    console.log(name, "start");
    resolve(console.log(name, "middle"));
  }).then(() => {
    console.log(name, "end");
  });
}
```

虽然这里的  `then()`  看起来很多余，其中的代码完全可以被合并到构造器的回调里，但不管该  `Promise`  的状态如何，`then()`  的回调**总会被异步执行**，`await`  的行为也一样。因此，只要情况不是必须或可能需要等待  `Promise`  的结果，就应该避免使用  `await`。

其他微任务能在函数执行恢复之前执行：

```js
let i = 0;

queueMicrotask(function test() {
  i++;
  console.log("microtask", i);
  if (i < 3) {
    queueMicrotask(test);
  }
});

(async () => {
  console.log("async function start");
  for (let i = 1; i < 3; i++) {
    await null;
    console.log("async function resume", i);
  }
  await null;
  console.log("async function end");
})();

queueMicrotask(() => {
  console.log("queueMicrotask() after calling async function");
});

console.log("script sync part end");

// Logs:
// async function start
// script sync part end
// microtask 1
// async function resume 1
// queueMicrotask() after calling async function
// microtask 2
// async function resume 2
// microtask 3
// async function end
```

此案例中，`test()`  总会在异步函数恢复执行前被调用，呈现轮流的调度。微任务被执行的顺序通常就是入队的先后顺序，而  `console.log("queueMicrotask() after calling async function");`  比  `await`  晚入队，因此  `"queueMicrotask() after calling async function"`  在异步函数第一次恢复之后才输出。

##### 改善栈追踪

有时，当异步函数直接返回一个  `Promise`  时我们会省略  `await`。

```js
async function noAwait() {
  // Some actions...

  return /* await */ lastAsyncTask();
}
```

但是假如这个  `Promise`  的由来是调用了异步函数，且该异步函数的异步部分抛出了错误：

```js
async function lastAsyncTask() {
  await null;
  throw new Error("failed");
}

async function noAwait() {
  return lastAsyncTask();
}

noAwait();

// Error: failed
//    at lastAsyncTask
```

栈追踪中只出现了  `lastAsyncTask`，这是因为抛出错误时  `noAwait`  已经返回——某种意义上该  `Promise`  已经与  `noAwait`  无关。若要改善栈追踪，你可以用  `await`  提前等待，错误就会在函数体结束前抛出，接着该错误会被包装进一个新的  `Promise`，因错误被  `await`  在主调函数的函数体抛出，主调函数将会出现在栈追踪。

```js
async function lastAsyncTask() {
  await null;
  throw new Error("failed");
}

async function withAwait() {
  return await lastAsyncTask();
}

withAwait();

// Error: failed
//    at lastAsyncTask
//    at async withAwait
```

但是，这样会有一点性能牺牲，毕竟  `Promise`  会被拆装了又再次包装

## 参考

- [异步 JavaScript——回调、Promises 和 Async/Await](https://www.freecodecamp.org/chinese/news/asynchronous-javascript-explained/)
- [Ajax](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX)
- [使用 Ajax](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)
- [回调函数](https://developer.mozilla.org/zh-CN/docs/Glossary/Callback_function)
- [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E6%8F%8F%E8%BF%B0)
- [使用 Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_promises#%E7%BA%A6%E5%AE%9A)
- [Fetch 基本概念](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Basic_concepts)
- [使用 Fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)
- [async 函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)
- [await](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await)
