---
title: ts-node
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## ts-node

- ./vscode/launch.json

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "ts-node",
      "type": "node",
      "request": "launch",
      "runtimeExecutable": "node",
      "runtimeArgs": ["--nolazy", "-r", "ts-node/register/transpile-only"],
      "args": ["scripts/generateBizConfig.ts"],
      "cwd": "${workspaceRoot}",
      "internalConsoleOptions": "openOnSessionStart",
      "skipFiles": ["<node_internals>/**", "node_modules/**"]
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/ts-node.png)
