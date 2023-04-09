---
title: "package.json 是什么"
subtitle: ""
date: 2023-04-09
draft: false
author: ""
authorLink: ""
description: "开发forkify相关"
keywords: ""
license: ""
comment: false
weight: 0

tags:
  - npm
categories:
  - front-end

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

## 了解 package.json

1. 如果你以前用过 Node.js，则可能会遇到 _package.json_ 文件。它是一个 JSON 文件，位于项目的根目录中。你的 _package.json_ 包含关于项目的重要信息。它包含关于项目的使人类可读元数据（如项目名称和说明）以及功能元数据（如程序包版本号和程序所需的依赖项列表）

</br>

## package.json  中的用途是什么

1. 项目的 _package.json_ 是配置和描述如何与程序交互和运行的中心。 npm CLI（和 yarn）用它来识别你的项目并了解如何处理项目的依赖关系。_package.json_ 文件使 npm 可以启动你的项目、运行脚本、安装依赖项、发布到 NPM 注册表以及许多其他有用的任务。 npm CLI 也是管理 package.json 的最佳方法，因为它有助于在项目的整个生命周期内生成和更新 _package.json_ 文件。

2. _package.json_ 会在项目的生命周期中扮演多个角色，其中某些角色仅适用于发布到 NPM 的软件包。即使你没有把项目发布到 NPM 注册表中，或者没有将其公开发布给其他人，那么 _package.json_ 对于开发流程仍然至关重要。

3. 你的项目还必须包含 _package.json_，然后才能从 NPM 安装软件包。这可能是你在项目中需要它的主要原因之一

</br>

## package.json  中的常见字段

1. 让我们看一下  *package.json*  中包含的一些最常见和重要的字段，以更好地了解如何使用和管理这个基本文件。有些用来发布到 NPM，而其他一些则可以帮助 npm CLI 运行应用程序或安装依赖项

2. [相关文档](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.npmjs.com%2Ffiles%2Fpackage.json "https://docs.npmjs.com/files/package.json")

### name

```json
"name": "my-project"
```

1. `name` 字段定义包的名称。发布到 NPM 注册表时，这是软件包将在其中显示的名称。它不能超过 214 个字符，只能是小写字母，并且必须是 URL 安全的（允许连字符和下划线，但 URL 中不允许使用空格或其他字符）。

2. 如果将软件包发布到 NPM，则 `name` 属性是必需的，并且必须是唯一的。如果尝试用 NPM 注册表上当前已经使用的名称发布程序包，则会收到错误消息。如果你的软件包并不是要发布到 NPM 上，则 `name` 不必是唯一的。

### version

```json
"version": "1.5.0",
```

1. `version`  字段对于任何已发布的软件包都非常重要，并且在发布之前是必填的。这是  *package.json*  描述的软件的当前版本。

2. 你不需要使用 SemVer，但它是 Node.js 生态系统中使用的标准，强烈建议使用。对于未发布的程序包，此属性不是严格要求的。通常在将新版本发布到 NPM 之前，根据 SemVer，版本号会增加。当不依赖程序包作为依赖项或未将程序包发布到 NPM 时，通常不使用这个工作流程。但是如果将软件包用作依赖项，那么确保 `version` 字段保持最新非常重要，这样可以确保其他人所使用的软件包的正确版本。

### license

1. 这是非常重要但经常被忽略的属性。`license` 字段使我们可以定义适用于 _package.json_ 所描述代码的许可证。同样，在将项目发布到 NPM 注册表时，这非常重要，因为许可证可能会限制某些开发人员或组织对软件的使用。拥有清晰的许可证有助于明确定义该软件可以使用的术语。

2. `license` 字段的值通常是许可证的标识符代码——例如 `MIT` 或 `ISC` 之类的字符串，它们代表 MIT 许可证和 ISC 许可证。如果你不想提供许可证，或者明确不想授予使用私有或未发布的软件包的权限，则可以将 `UNLICENSED` 作为许可证。

### author 和 contributors

```perl
"author": "Jon Church jon@example.com https://www.osioslabs.com/#team",
"contributors": [{
	"name": "Amber Matz",
	"email": "example@example.com",
	"url": "https://www.osiolabs.com/#team"
}],
```

1. `author` 和 `contributors` 字段的功能类似。它们都是 `people` 字段，可以是`"Name"` 格式的字符串，也可以是具有 `name，email，url` 字段的对象。email 和 url 都是可选的。

2. `author` 只供一个人使用，`contributors` 则可以由多个人组成。

3. 这些字段是列出公共项目的联系人以及与贡献者共享信用的有用方法。

### description

1. NPM 注册表将`description` 字段用于发布的软件包，以在搜索结果中和 npmjs.com 网站上描述该软件包。

2. 当用户搜索 NPM 注册表时，该字符串用于帮助了解软件包。这应该是软件包的简短摘要。

3. 即使你没有将其发布到 NPM 注册表中，它也可以用作项目的简单文档。

### main

```json
"main": "src/index.js",
```

1. `main` 字段是 _package.json_ 的功能属性。它定义了项目的入口点，通常是用于启动项目的文件。

2. 如果你的包（例如其名称为 `foo-lib`）是由用户安装的，则当用户执行 `require('foo-lib')` 时，这是 require 返回的 `main` 字段中所列出的文件的 `module.exports` 属性。

3. 它的值通常是项目根目录中的 _index.js_ 文件，但也可以是你选择作为包的主入口的任何文件。

### scripts

```json
"scripts": {
	"start": "node index.js",
	"dev": "nodemon"
}
```

1. `scripts` 字段是 _package.json_ 中的另一种元数据功能。`scripts` 属性接受一个对象，它的值为可以通过 `npm run` 运行的脚本，其键为实际运行的命令。这些通常是终端命令，我们把它们放入 `scripts` 字段，可以既可以记录它们又可以轻松地重用。

2. `scripts` 是 npm CLI 用来运行项目任务的强大工具。他们可以完成开发过程中的大多数任务。

### repository

```json
"repository": {
	"type": "git",
	"url": "https://github.com/osiolabs/example.git"
}
```

1. 你可以通过提供 `repository` 字段来记录项目代码所在的资源库。该字段是一个对象，用于定义源代码所在的 url 及其使用的版本控制系统的类型。对于开源项目，可能是以 Git 作为版本控制系统的 GitHub 或 Bitbucket 。

2. 需要注意的是 URL 字段的本意是指向可从中访问版本控制的位置，而不仅仅是指向已发布的代码库。

### dependencies

```json
"dependencies": {
	"express": "^4.16.4",
    "compression": "~1.7.4"
}
```

1. 这是 _package.json_ 中最重要的字段之一，它列出了项目使用的所有依赖项（项目所依赖的外部代码）。使用 npm CLI 安装软件包时，它将下载到你的 _node_modules/_ 文件夹中，并将一个条目添加到你的依赖项属性中，注意软件包的名称和已安装的版本。

2. `dependencies` 字段是一个对象，其中的包名做为键，而版本或版本范围为值。从这个列表中，当在目录中运行 `npm install` 时，npm 知道要获取和安装哪些包（以及什么版本）。 _package.json_ 的 `dependencies` 字段位于项目的核心，并定义项目所需的外部包。

3. 在依赖版本中看到的插入符号（`^`）和波浪号（`~`）是 SemVer 中定义的版本范围的表示法。

### devDependencies

```json
"devDependencies": {
	"nodemon": "^1.18.11"
}
```

1. 与 `dependencies` 字段类似，但是这里列出的包仅在开发期间需要，而在生产中不需要。

2. 例如，在开发过程中使用工具重新加载项目，比如 [`nodemon`](https://link.juejin.cn?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fnodemon "https://www.npmjs.com/package/nodemon")，一旦程序部署并投入生产，将不会再使用它。`devDependencies` 属性使我们可以明确地指出生产中不需要哪些依赖项。在生产环境中安装应用程序时，可以用 `npm install --production` 仅安装 _package.json_ 的 `dependency` 字段中列出的内容。

3. _devDependency_ 是记录开发过程中程序需要哪些工具的好方法。要将 npm 的软件包作为 devDependency 安装，可以运行 `npm install --save-dev`。

4. `devDependencies` 属性的另一种用途是在我们的 npm 脚本中使用它们。

</br>

## 管理你的 package.json

1. _package.json_ 文件必须是有效的 JSON。这意味着任何缺少的逗号、丢失的引号或其他格式错误都将阻止 npm 与 _package.json_ 进行交互。如果确实引入了错误，则下次运行 npm 命令时将会看到错误提示。建议尽可能使用 npm CLI 更新和管理 _package.json_，以避免意外将错误引 入*package.json* 中。

2. 使用 `npm init` [创建你的 _package.json_](https://link.juejin.cn?target=https%3A%2F%2Fheynode.com%2Ftutorial%2Fcreate-packagejson-file "https://heynode.com/tutorial/create-packagejson-file") 将有助于确保你生成有效的文件。

3. 最好使用 npm 的命令 `npm install` ，`npm uninstall` 和 `npm update` 来管理依赖项，这样可以使你的 _package.json_ 和 _node_modules/_ 文件夹保持同步。如果手动添加依赖项列表的话，需要你在把依赖项实际安装到项目之前运行 `npm install`。

4. 因为 _package.json_ 仅是我们记录依赖项的位置，而 _node_modules/_ 文件夹是安装依赖项代码的实际位置，所以手动更新 _package.json_ 的依赖项字段不会立即将我们的状态反映到 _node_modules/_ 文件夹。这就是为什么要用 npm 帮助管理依赖项的原因，因为它会同时更新 _package.json_ 和 _node_modules/_ 文件夹。

5. 你当然可以在文本编辑器中手动编辑 _package.json_ 并进行更改，只要你注意不要引入任何 JSON 格式错误，这对大多数字段都适用。但是我建议你尽可能使用 npm CLI 命令。

</br>

## 总结

1. _package.json_ 文件是 Node 项目的核心。它记录了有关发布到 NPM 之前所需要的项目的重要元数据，它还定义了 npm 用于安装依赖项、运行脚本以及标识包的入口点的项目功能属性。

2. 并非 _package.json_ 中所有字段都适用于你，但是我们可以通过其在 _package.json_ 文件中记录有关程序的信息来获得一些强大的好处。了解 _package.json_ 的角色以及它与 npm 的关系是开发 Node.js 应用的重要组成部分，并且正日益成为 JavaScript 生态系统的重要组成部分。

</br>
