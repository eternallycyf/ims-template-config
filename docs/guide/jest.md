---
title: jest
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## jest

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "jest",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/jest/bin/jest.js",
      "console": "integratedTerminal",
      "args": [
        // 不再用 worker 进程并行跑测试用例，而是在当前进程串行跑：
        "-i"
      ]
    }
  ]
}
```

- 只调试某个测试用例

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "jest",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/jest/bin/jest.js",
      "console": "integratedTerminal",
      "args": [
        // 不再用 worker 进程并行跑测试用例，而是在当前进程串行跑：
        "-i",
        "packages/ims-view-pc/tests/index.test.tsx",
        "-t",
        "CommonDemo"
      ]
    }
  ]
}
```

## 调试当前打开的文件

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "jest",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/jest/bin/jest.js",
      "console": "integratedTerminal",
      "args": [
        // 不再用 worker 进程并行跑测试用例，而是在当前进程串行跑：
        "-i",
        "${file}"
      ]
    }
  ]
}
```

- 手动输入名称调试
  - (支持正则 例如输入 `CommonDemo\d`)

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "jest",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/jest/bin/jest.js",
      "console": "integratedTerminal",
      "args": [
        // 不再用 worker 进程并行跑测试用例，而是在当前进程串行跑：
        "-i",
        "${file}",
        "-t",
        "${input:case}"
      ]
    }
  ],
  "inputs": [
    {
      "type": "promptString",
      "id": "case",
      "description": "CommonDemo",
      "default": ""
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/jest-debugger.png)

## FAQ

### 发生异常: Error: Cannot find module 'jest-environment-jest-environment-jsdom/package.json' from 'xxx'

- 关闭异常断点等
