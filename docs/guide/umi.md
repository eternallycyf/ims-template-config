---
title: umi
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## umi

- 以 umi4 为例
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
      "name": "Launch Chrome against localhost",
      "url": "http://localhost:8000",
      "webRoot": "${workspaceFolder}",
      "skipFiles": [
        "${workspaceFolder}/<node_internals>/**",
        "${workspaceFolder}/node_modules/**",
        "${workspaceFolder}/webpack/**",
        "${workspaceFolder}/.umi/**",
        "${workspaceFolder}/umi\\.js$",
        "${workspaceFolder}/@@/devScripts.js$",
        "${workspaceFolder}/^webpack://.*/react refresh$",
        "${workspaceFolder}/react_devtools_backend.js\\.js$"
      ],
      "smartStep": true,
      "sourceMaps": true
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/umi.png)

## FAQ

### debugger 行数不对

```js
  chainWebpack: function(config) {
    config.devtool('source-map');
  }
```
