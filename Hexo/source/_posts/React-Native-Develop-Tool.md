---
title: React Native Develop Tool
date: 2018-06-03 00:53:58
categories: "React-Native" #哪个分类下
tags: [iOS,Android]
description:  #描述
---

## React Native Develop Tool

### 开发工具提供 `自动补全`、`语法检查`, 方便我们开发。

1、[* VS Code（Visual Studio Code）*](https://code.visualstudio.com) &nbsp;[ open/free ]
```xml
GitHub 项目地址：https://github.com/Microsoft/vscode
# 插件
  React Native Tools：微软官方出的ReactNative插件,非常好用
  Reactjs code snippets：react的代码提示，如componentWillMount方法可以通过cwm直接获得
  Auto Close Tag：自动闭合标签
  Auto Rename Tag：自动重命名标签，配合上面的插件使用，基本上能赶上IntelliJ IDEA系的功能了
  Path Intellisense：文件路径提示补全
  TabSpacer：代码格式化
```

2、[* Atom *](https://www.atom.io) + [* Nuclide *](https://github.com/facebook/nuclide) + [* watchman *](http://github.com/facebook/watchman)   &nbsp; [ open/free ]
```sh
(1)Atom 是github专门为程序员推出的一个跨平台文本编辑器。
      具有简洁和直观的图形用户界面，并有很多有趣的特点：
            支持CSS，HTML，JavaScript等网页编程语言。
      它支持宏，自动完成分屏功能，集成了文件管理器。

(2)`watchman`+ `flow` + `eslint` + `Yarn`
(3)Facebook 12月12日宣布，由于开发团队精力有限，后续将停止维护 `Nuclide`、`Atom-IDE` 和其他相关开源库。
  项目现有源码将继续保留在 Facebook 开源存档仓库中。 目前这些项目的 GitHub 仓库已被官方归档，处于只读状态。
  `Nuclide` 和 `Atom IDE` 的官网也相继挂出了“退休”公告。
```

<!--more-->

3、[* WebStorm *](http://www.jetbrains.com/webstorm) &nbsp;[ private ]
```sh
  是 `jetbrains公司`(http://www.jetbrains.com)旗下一款JavaScript 开发工具。
  目前已经被广大中国JS开发者誉为“Web前端开发神器”、“最强大的HTML5编辑器”、“最智能的JavaScript IDE”等。
  与 `IntelliJ IDEA`(https://www.jetbrains.com/idea/ )同源，继承了IntelliJ IDEA强大的JS部分的功能。
```

4、[* Sublime Text *](https://www.sublimetext.com)  需要安装插件，才可进行预编译 &nbsp; [ private]
```xml
# sublime插件
  ReactJS：支持React开发，代码提示，高亮显示
  Emmet：前端开发必备
  Terminal：在sublime中打开终端并定位到当前目录
  react-native-snippets：react native 的代码片段
  JsFormat：格式化js代码
```

5、[* Vim 编辑器 *](https://www.vim.org) &nbsp;[ open/free ]
```xml
# 需要翻墙

  为 React-JSX 设置 Vim：https://jaxbot.me/articles/setting-up-vim-for-react-js-jsx-02-03-2015
  License：开源
  支持平台：Mac、Linux

# Vim 插件
  vim-jsx - 提供 JSX 的语法高亮和缩进。
  vim-react-snippets - 一组为 Vim 打造的可与Facebook 的 React 库一起使用的片段。
  vim-babel - 一组为 Vim 打造的可与Facebook 的 React 库一起使用的片段
```

6、[* GNU Emacs 编辑器 *](https://www.gnu.org/software/emacs) &nbsp; [ open/free ]
```xml
  官网：https://www.gnu.org/software/emacs/
  官方文档：https://www.gnu.org/software/emacs/documentation.html
  针对 Ract Native 的初始设置：http://www.cyrusinnovation.com/initial-emacs-setup-for-reactreactnative/
  GitHub 项目地址：https://github.com/emacs-mirror/emacs

# 具有用于下载和安装扩展的包系统。
  GNU EMACS 是一个可扩展、可定制、免费、自由的文本编辑器。
  web-mode.el - 它是一个自主的 emacs 主模块，用于编辑 Web模板。它与许多语言兼容，包括 JSX（React）
```

7、[* Spacemacs 编辑器 *](http://spacemacs.org) &nbsp;[ open/free ]
```xml
Spacemacs 是一个社区驱动的 Emacs 发行版 - 最好的编辑器既不是 Emacs 也不是Vim，它是 Emacs 和 Vim 相结合！
  React layer - 适用于 React 的 ES6 和 JSX 配置层。
  它将自动识别 .jsx 和 .react.js 文件。一个用于 React集成的包层。

官网：http://spacemacs.org/
Github 项目地址：syl20bnr/spacemacs(https://github.com/syl20bnr/spacemacs)
官方文档：http://spacemacs.org/doc/DOCUMENTATION.html
```
8、 [* Deco IDE *](https://www.decosoftware.com/) &nbsp;[ open/free ]
```xml
Deco 是专为 React Native 打造的 IDE。它是一个用于编写 React Native 应用程序的一体化解决方案，
  无需任何环境设置即可下载和使用。Deco 专注于组件重用，并支持用户对 UI 的实时编辑，
  从而改进了React Native 开发工作流程。

优点：
  (1)可以直接在编辑器里启动模拟器。
  (2)当然最吸引人的是直接拖拽一些组件到界面。
  (3)可以自动创建新项目、搜索开源组件并插入到项目中。
  (4)还可以实时地可视化地调整用的界面。

官网：https://www.decosoftware.com/
GitHub 项目地址：decosoftware/deco-ide(https://github.com/decosoftware/deco-ide)
官方文档：https://www.decosoftware.com/docs
支持平台：Mac（仅适用于iOS）
```

9、 [* TextMate 编辑器 *](http://macromates.com) &nbsp;[ private ]
```xml
官网：https://macromates.com/
官方文档：http://manual.macromates.com/en/
GitHub 项目地址：https://github.com/textmate/textmate
License：收费
支持平台：Mac

# 插件
  javascript-jsx.tmbundle - 用于JSX（React）的 Textmate Bundle。目前支持语法高亮。
```

10、[* RubyMine *](https://www.jetbrains.com/ruby/) &nbsp;[ private ]
```sh
[* jetbrains公司 *](http://www.jetbrains.com)
  是一个为Ruby 和Rails开发者准备的 IDE，其带有所有开发者必须的功能，
  并将之紧密集成于便捷的开发环境中，号称最智能的Ruby和Rails的IDE，
  能够大大增加Ruby和Rails开发者的开发效率
```


---

### 我用的是 [ ‘VS Code’ ](https://code.visualstudio.com)
很多人选择 1、vim &nbsp; 2、sublime &nbsp; 3、VS Code &nbsp; (我听到的心声是这样顺序)

---

### 框架
1、[* Exponent *](https://docs.expo.io) 只支持全部RN-js代码开发的框架
```sh
是一套开发环境，还带有一个已上架的空应用容器。
  这样你可以在没有原生开发平台（Xcode或是Android Studio）的情况下
  直接编写React Native应用（当然这样你只能写js部分代码而没法写原生代码）。
```



2、[* ReactXP *](https://microsoft.github.io/reactxp/)
```sh
是微软Skype团队维护的一个`框架`。
  ReactXP 的意思是 React Cross Platform。
  那如何跨端的呢？在 React 和 React Native 封装一个抽象层，也是一个子集，提供跨平台的 API。
  底层 iOS/Android 就是跑RN，Web 就是 React，Windows 10 及以上采用自家的 UWP，
  https://wapbaike.baidu.com/item/uwp/4236943
  适配 React Native，Windows 10 以下其他平台就用 Electron 把 Web 包起来……跨端了。
```
