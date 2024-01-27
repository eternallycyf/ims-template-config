---
title: node
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## 新建一个目录

```base
mkdir debug
cd debug
npm init -y
```

- 添加 index.js

```js
// index.js
const os = require('os');
const homedir = os.homedir();
console.log(homedir);
```

### 使用 chrome 调试

- node --inspect-brk index.js
- 在 chrome 浏览器打开 chrome://inspect/#devices

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/chrome-inspect.png.png)

### vscode

- ./vscode/launch.json

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "首行断点",
      "type": "node",
      "request": "launch",
      // 首行断点
      // "stopOnEntry": true,
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}/index.js"
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/node-vscode-debugger.png)
