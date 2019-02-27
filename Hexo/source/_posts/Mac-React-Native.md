---
title: Mac React-Native
date: 2018-06-02 19:34:35
categories: "React-Native" #哪个分类下
tags: [iOS,Android]
description:  #描述
---



# React-native 安装基础篇 <br>
> RN官方文档 (0.55):
- http://facebook.github.io

> RN `中文翻译` 文档 (0.51):
- https://reactnative.cn

> 推荐博客 `ES6` 语法学习(阮一峰)
- http://es6.ruanyifeng.com

<!--more-->

<br>

## 以下基于MacOS <br>
## 一、安装工具 <br>

1、[ 安装 homebre ](https://brew.sh)
```sh
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2、然后 安装 ` node.js `
```sh
    brew install node
```

3、  配置` node `国内镜像
```sh
# (1)修改 下载仓库为淘宝镜像
npm config set registry https://registry.npm.taobao.org --global

#如果要发布自己的镜像需要修改回来
#npm config set registry https://registry.npmjs.org/

# (2)　
npm config set disturl https://nodejs.org/dist/ --global

#是否配置成功,请使用下面命令
npm config get registry
npm config get disturl

#查看npm全部配置
npm config get
```


4、Yarn、React Native的命令行工具（react-native-cli）
```sh
# Yarn是Facebook提供的替代npm的工具，可以加速node模块的下载。
# React Native的命令行工具用于执行创建、初始化、更新项目、运行打包服务（packager）等任务。

npm install -g yarn react-native-cli

# 配置` Yarn `国内镜像
yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global
```

## 二、安装、配置 RN <br>
1、下载 RN
```sh
# 第1️⃣种 -> 第一次新项目空文件安装
react-native init <项目名>

# ------------------------------------
# 第2️⃣种 -> 在原生项目基础上安装
#    (2-1)新建 `RN工程文件夹` 后 `终端`定位到该文件夹(cd ...)，copy 项目 到建立 `/ios` 文件夹
        # https://reactnative.cn/docs/0.51/integration-with-existing-apps.html#content

#    (2-2)在项目根目录下创建一个名为package.json的空文本文件
      touch  package.json  # 或者copy 一个也行，但要看配置

#    (2-3) `package.json`为空，需要填写将要安装的`react-native`配置信息
       vim package.json
       # 或者  Sublime / Atom / Notepad++ .... 进行填写配置,如下:

       {
            "name": "项目名",
            "version": "0.0.1", //# 字段没有太大意义（除非你要把你的项目发布到npm仓库）
            "private": true,
            "scripts": {
                //# 启动packager服务的命令
                "start": "node node_modules/react-native/local-cli/cli.js start",
                "test": "jest",
                "flow": "flow; test $? -eq 0 -o $? -eq 2"
            },
            "dependencies": {
                //# react和react-native的版本取决于你的具体需求,一般来说我们推荐使用最新版本
                "react": "16.3.1",
                "react-native": "^0.55.4",

                //# 用于reeact-native内部ES6参数类型检查
                "prop-types": "^15.6.1",

                //# 热更新(第三方)
                "code-push-server": "^0.2.20",
                "react-native-code-push": "^5.3.4",

                //# 滚动图(第三方)
                "react-native-swiper": "^1.5.13",

                //# 导航栏(第三方)
                "react-navigation": "^2.0.1"

             //# 你可以使用npm info react和npm info react-native来查看当前的最新版本
             //# 这两个必须是匹配，官方也没能列出匹配的列表，只能通过命令  先尝试执行npm install，然后根据提示 ...
               "eslint": "^3.17.0", //#是一个JavaScript代码静态检查工具，可以检查JavaScript的语法错误，提示潜在的bug https://segmentfault.com/a/1190000009914940
                            //# 安装官网的Rule,配置代码的规范  http://eslint.org/docs/rules/
              "eslint-plugin-react-native": "^3.2.1",
            },
            "devDependencies": {
                "babel-cli": "^6.26.0",
                "babel-jest": "23.0.0",
                "babel-preset-flow": "^6.23.0",
                "babel-preset-react-native": "4.0.0",

                //# 静态的检查类型检查
                "flow-bin": "^0.67.1",

                "jest": "23.0.0",
                "react-test-renderer": "16.3.1"
            },
            "jest": {
                "preset": "react-native"
            }
        }

```

<br>

2、根据`package.json`安装相应的 `react-native` + `React` 以及第三方
```sh
npm init #（这个工作跟cocoapods的podfile文件初始化有点像）-> 根据package.json配置内容，进行安装。
```

<br>

3、添加 yarn (react-native依赖管理工具)
```sh
yarn add react-native

# facebook.github.io/react-native/docs/image.html 看官网最新是哪个版本
yarn add react@16.3.1
```

<br>

4、工程根目录 使用命令(这个会很慢很慢，取决你的网络)
```sh
npm install
```

<br>

5、进入项目目录(我的是 ./ios/) ,如果你已经安装Cocoapods 了
```sh
# Podfile 设置
        platform :ios, '8.0'

        target '项目名' do

          # 你的项目需要库

          #-------以下是RN库--------

          	pod 'React', :path => '../node_modules/react-native', :subspecs => [
            	'Core',
            	'CxxBridge', # 如果RN版本 >= 0.45则加入此行
            	'DevSupport', # 如果RN版本 >= 0.43，则需要加入此行才能开启开发者菜单
                'RCTText',
                'RCTImage',
                'RCTNetwork',
                'RCTSettings',
                'RCTVibration',
                'RCTAnimation',
                'RCTActionSheet',
                'RCTGeolocation',
            	'RCTWebSocket', # 这个模块是用于调试功能的
            	# 在这里继续添加你所需要的RN模块
          	]

          	# 如果你的RN版本 >= 0.42.0，则加入下面这行
            pod "yoga", :path => "../node_modules/react-native/ReactCommon/yoga"

          	 # 如果RN版本 >= 0.45则加入下面三个第三方编译依赖
           	pod 'DoubleConversion', :podspec => '../node_modules/react-native/third-party-podspecs/DoubleConversion.podspec'
           	pod 'GLog', :podspec => '../node_modules/react-native/third-party-podspecs/GLog.podspec'
          	pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'
           
           #如果用 npm/yarn 添加库，自动会在此处添加



        	post_install do |installer|
        	    installer.pods_project.build_configurations.each do |config|
        	      config.build_settings['SYMROOT'] = '${SRCROOT}/../build'
        	    end
          	end
        end

# ------------------------------------------------------------------

# 安装 CocoaPod
pod install
```
<br>

6、react-native (启动 本地Node服务，方便实时用nodo.js去解析ES6的代码->`main.bundle.js`)

# 在React Native项目根目录下运行
```sh
npm start   /   react-native start
```
<br>

7、`index.ios.js` 生产可执行的文件(可被RN-server 找到) （作为测试用，真正开发需要 `react-native bundle.........`）
```sh
curl http://localhost:8081/index.ios.bundle -o main.jsbundle
```

<br>

8、重新 启动RN服务问题 <br>
凡是遇到 终端命令错误等的问题，记得先 彻底关闭 ` 终端 `，在去执行，可能就好了。 <br>

或者 <br>

```sh
# 查看`Node.js服务运行进程`命令
lsof -i:8081

# 查询结果(node的PID)
# COMMAND  PID    USER   FD   TYPE             DEVICE   SIZE/OFF   NODE           NAME
# node    9753 srxboys   32u  IPv6 0xd47...     0t0      TCP       *:sproxyadmin  (LISTEN)

# 关掉进程(PID)
kill -9 9753

```
---

<br><br>


#### 编译项目 之前，一定要自测
1、先 运行`React Native `(上面的第6步)  <br>

2、看看`index.js + ...js`是否有问题 (上面的 第7步) <br>

3、你的 `jsCodeLocation ` 是以何种方式 写的, 是否执行你的js <br>
> - (1)是 NSBundle 走Xcode的`Copy Bundle resources`里面找文件 xx.jsbundle <br>
> - (2) [NSURL filexxx]   ，就是改 app 目录下里面找文件  xx.jsbundle <br>
> - (3) [NSURL urlWithxx]  很遗憾，这个不支持，可能RN觉得不安全 <br>
> > - 这个我们可以先下载xx.jsbundle,  然后执行 (2) 步【注意 安全保护处理】 <br>


4、针对错误 或者 想要调试的(针对变量等) 可以采用 `debugger模式` --> * `React-Native`+`iphone/Android` + `Google Chrome` *
> - 模拟器
> - -  *`菜单`*  iPhone-> `Command` + `D`、Android->  百度上有很多教程 以及安卓`夜神模拟器`
> - - iPhone-> `Command` + `R` 、Android->`R+R` 

> -  真机
> - - 摇晃

---



## 三、 运行项目错误
1、如果有用的文件，一定确保文件在 `app` 的目录里  <br>
2、确保js 文件正确(上面)  <br>
3、确保js 调用的RN库，你的项目RN都保函这些库(包括自带、第三方)  <br>
4、RN 以及 支持的第三方，Xcode编译通过  <br>




> WARN eslint-plugin-react-native@3.2.1 requires a peer of eslint@^3.17.0 || ^4.0.0 but none is insta ...  
- package.json 文件追加 最后2行代码

```sh
    ...
      "dependencies": {
        "react": "16.3.1",
        "react-native": "0.55.4",
        # 后面两行，看好上面`WARN`提示的版本号
        "eslint": "^3.17.0",
        "eslint-plugin-react-native": "^3.2.1"
        ...
      },
    ...
```


---

### React-Native特性
> 一、RN 提供了四种点击事件
- 1、TouchableHighlight       : 可编写点击的 背景色、透明度,只支持一个子节点
- 2、TouchableNativeFeedback  : 仅限Android平台
- 3、TouchableWithoutFeedback : 点击没有任何颜色变化,只支持一个链单节点
- 4、TouchableOpacity         : 此组件与TouchableHighlight的区别在于并没有额外的颜色变化，继承了所有TouchableWithoutFeedback的属性,并支持多个子节点

> 二、React认为一个组件应该具有如下特征：
- 可组合（Composeable）：一个组件易于和其它组件一起使用，或者嵌套在另一个组件内部。如果一个组件内部创建了另一个组件，那么说父组件拥有它创建的子组件，通过这个特性，一个复杂的UI可以拆分成多个简单的UI组件；
- 可重用（Reusable）：每个组件都是具有独立功能的，它可以被使用在多个UI场景；
- 可维护（Maintainable）：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护；


> 三、在React Native（React.js）里，组件所持有的数据分为两种：
- 属性（props）：组件的props是不可变的，它只能从其他的组件（例如父组件）传递过来。
- 状态（state）：组件的state是可变的，它负责处理与用户的交互。在通过用户点击事件等操作以后，如果使得当前组件的某个state发生了改变，那么当前组件就会触发render()方法刷新自己。


> 四、组件也有生命周期，大致分为三大阶段：
- Mounting：已插入真实 DOM
- Updating：正在被重新渲染
- Unmounting：已移出真实 DOM

> 五、React 中组件的几种通信方式，分别是：
- 父组件向子组件通信：使用 props
- 子组件向父组件通信：使用 props 回调
- 跨级组件间通信：使用 context 对象
- 非嵌套组件间通信：使用事件订阅
