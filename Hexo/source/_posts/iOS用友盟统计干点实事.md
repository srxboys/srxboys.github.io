---
title: iOS用友盟统计干点实事
date: 2017-08-24 19:43:14
categories: "Objective-C" #哪个分类下
tags: [iOS]
---


## ` 友盟统计 ` 分析下 iOS、android 崩溃率


### iOS
- 8 - 24  错误总数  `621`次   活跃数`11685`   概率  `621/11685` = `0.017`      `百分之2`
- 8 - 23   `百分之2`
- ...

<!--more-->

#### 用户数：`461290`
- 8-24 用户活跃数 `15610`
- 8- 23 用户活跃数 `14736`
- ...
-
- `2/百` 概率 比较高，留存用户也在逐渐下降
-
-目标为 `n/千`

---

### android
- 8 - 24  错误总数  `517`次  `百分之1.7`
- 8 - 23   `百分之1.8`
- ...

#### 用户数：`861412`
- 8-24 用户活跃数 `13242`
- 8- 23 用户活跃数 `13015`
-
- `2/百` 概率 比较高，留存用户也在逐渐下降
-
-目标为 `n/千`

---

## iOS 解决方案：
### 采用热更新   (NSObject + method swizzling + JS/Lua/... )
具有针对性的 部分用户进行更新 ，并统计 得出效果。效果好，就全面推广。用户是感觉不到的。

### 那么问题来了:
- 1、代码的编写。在哪里比较合适？
- 2、是不是所有代码都可以改。包括第三方SDK更新吗？？？？
- 3、区分部分热更新统计、在全部热更新。版本号没有变。那么全部热更新后 之前的没有热更新的统计，又怎么区分。
- 4、热更新安全把控
- 5、顺利通过`苹果审核`
- 6、总是热修复，也不是正确的解决方案，是不是我们代码在编写的`健壮`、`review`、`测试` 等,哪里做的不够、不细。

> 如果以上，你都不能把控。那你只能用先用用第三方，看看源码。吃透了 你又有新的技术点。

---

### [* 我搜集的热更新方案 *](https://srxboys.github.io/2018/06/03/热更新方案)

---

###上面说过的
> 用Lua脚本热修复的库
- https://github.com/probablycorey/wax/
- https://github.com/alibaba/wax
- https://github.com/mmin18/WaxPatch

> 用JS脚本热修复的库
- weex ->  https://github.com/apache/incubator-weex
- react-native https://github.com/facebook/react-native
- JSPatch -> https://github.com/bang590/JSPatch
- <del> DynamicCocoa -> https://github.com/DynamicCocoa/DynamicCocoa <del>
