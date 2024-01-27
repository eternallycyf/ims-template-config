---
title: 调试工具
apiHeader: false
tocDepth: 4
group:
  title: chrome
  order: 0
nav:
  title: 脚本
  order: 0
---

## chrome

### 元素断点

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/element-debugger.png)

### 过滤控制台信息

```js
  - ._\/node_modules\/._
  - ._\/.umi\/._
  - ^webpack://.\\\\\\\\\\\\*/react refresh\$
  - /umi\.js\$
  - /react_devtools_backend.js\.js\$
  - ^chrome-extension://fmkadmapgofadopljbjfkapdkoienihi\b.\\\\\\\\\*/react_devtools_backend\.js\$
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/console.png)

### 添加 ignore list(这样在 chrome 上断点就不会跳到源码了)

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/ignore1.png)

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/ignore2.png)

### 其他断点

- 条件断点一般用于 循环时，当满足某个条件时，才会触发断点
- 日志断点 一般用于 打印日志，当触发日志断点时，会打印出日志信息
- 不触发断点一般用于 网站防止操作无限循环 debugger 时，设置后，不会触发断点
- xhr 断点 可以用来调试 ajax 请求
- 事件断点 可以用来调试事件

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/other-debugger)

### 代码段

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/snnippets.png)

### 快速定位代码

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/css-find-code.png)

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/xhr-find-code.png)

### xhr 调试

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/search.png)

### Performance 性能分析

- 如页面卡顿找不到原因时 可以用过这个来快速找到源头

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/Performance.png)

### Layers

- 用来测试滚动条 等功能时 测试层级

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/layers.png)

### animations

- 测试动画
- 在生产环境遇到异常动画导致的问题 可以定位到元素然后样式覆盖

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/animations.png)
