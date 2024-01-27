---
title: vue
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## vue2

- 使用 vue cli 创建的项目
- yarn serve
- ./vscode/launch.json

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "针对 localhost 启动 Chrome",
      "url": "http://localhost:8080",
      "runtimeArgs": [
        "--auto-open-devtools-for-tabs" // 自动打开开发者工具
      ],
      "webRoot": "${workspaceFolder}",
      "sourceMapPathOverrides": {
        "webpack://项目名字/src/*": "${workspaceFolder}/src/*"
      }
    }
  ]
}
```

- vue.config.js

```js
const { defineConfig } = require('@vue/cli-service');
module.exports = defineConfig({
  transpileDependencies: true,
  configureWebpack(config) {
    config.devtool = 'source-map';
  },
});
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/vue2.png)

## vue3

- pnpm create vue@latest
- yarn serve
- ./vscode/launch.json

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "针对 localhost 启动 Chrome",
      "runtimeArgs": ["--auto-open-devtools-for-tabs"],
      "url": "http://localhost:5173",
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/vue3.png)
