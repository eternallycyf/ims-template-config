---
title: debugger
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

# 1.浏览器调试

## node

```shell
npm init -y

// index.ts
const os = require('os');
const homedir = os.homedir();
console.log(homedir);

node --inspect-brk index.js
```

```ts
chrome://inspect/
## 添加一个
Discover network targets => Configure
localhost:3000
```

## nest

```ts
"start:debug": "nest start --debug --watch",
pnpm start:debug
在 chrome://inspect/ 打开对应的
代码添加 debugger; 会自动断住
```

# vscode

## node

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "启动程序",
      "skipFiles": ["<node_internals>/**"],
      "stopOnEntry": true,
      "program": "${workspaceFolder}/index.js"
    }
  ]
}
```

## nest

### nest start --debug

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Attach",
      "port": 9229,
      "request": "attach",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "type": "node"
    },
    {
      "type": "node",
      "request": "launch",
      "name": "启动程序",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "program": "${workspaceFolder}/src/person/person.controller.ts",
      "preLaunchTask": "tsc: build - tsconfig.json",
      "outFiles": [
        "${workspaceFolder}/dist/**/*.js"
      ]
    }
  ]
}

## debugger 运行脚本: start:debug
代码添加 debugger; 或断点
```

### npm scripts

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Launch via NPM",
      "request": "launch",
      "runtimeArgs": ["start", "dev"],
      "runtimeExecutable": "npm",
      "skipFiles": ["<node_internals>/**"],
      "type": "node"
    }
  ]
}
```

### 静态资源前端

#### 1.直接调试

```json
  {
      "type": "chrome",
      "request": "launch",
      "name": "static",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceRoot}/src/public"
  },
```

#### 2. canary

```shell
/Applications/Google\ Chrome\ Canary.app/Contents/MacOS/Google\ Chrome\ Canary --remote-debugging-port=9222
```

```json
{
  "name": "canary-前端",
  "type": "chrome",
  "request": "attach",
  "port": 9222,
  "userDataDir": false,
  "runtimeExecutable": "canary",
  "sourceMaps": true,
  "sourceMapPathOverrides": {
    "meteor://💻app/*": "${workspaceFolder}/*",
    "webpack:///./~/*": "${workspaceFolder}/node_modules/*",
    "webpack://?:*/*": "${workspaceFolder}/*"
  },
  "runtimeArgs": [
    // 无痕模式
    // "--incognito",
    // 自动打开开发者工具
    "--auto-open-devtools-for-tabs",
    "--user-data-dir=${workspaceFolder}/.vscode/chrome"
  ],
  "skipFiles": ["${workspaceFolder}/node_modules/**/*.js", "<node_internals>/**/*.js"],
  "webRoot": "${workspaceRoot}/src/public"
}
```

## lauch.json 汇总

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "npm",
      "request": "launch",
      "runtimeArgs": ["start", "dev"],
      "runtimeExecutable": "npm",
      "skipFiles": ["<node_internals>/**"],
      "type": "node",
      "console": "integratedTerminal"
    },
    {
      "type": "chrome",
      "request": "launch",
      "name": "static",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceRoot}/src/public"
    },
    {
      "name": "canary-前端",
      "type": "chrome",
      "request": "attach",
      "port": 9222,
      "userDataDir": false,
      "runtimeExecutable": "canary",
      "sourceMaps": true,
      "sourceMapPathOverrides": {
        "meteor://💻app/*": "${workspaceFolder}/*",
        "webpack:///./~/*": "${workspaceFolder}/node_modules/*",
        "webpack://?:*/*": "${workspaceFolder}/*"
      },
      "runtimeArgs": [
        // 无痕模式
        // "--incognito",
        // 自动打开开发者工具
        "--auto-open-devtools-for-tabs",
        "--user-data-dir=${workspaceFolder}/.vscode/chrome"
      ],
      "skipFiles": ["${workspaceFolder}/node_modules/**/*.js", "<node_internals>/**/*.js"],
      "webRoot": "${workspaceRoot}/src/public"
    }
  ]
}
```

## 图片

<img width="1460" alt="截屏2024-01-20 22 07 03" src="https://github.com/eternallycyf/ims/assets/63464198/9bd95b6e-2ecf-4518-a669-fd62350d57e5" />

<img width="1661" alt="截屏2024-01-20 22 12 17" src="https://github.com/eternallycyf/ims/assets/63464198/de61f980-bb5e-4cc3-86fa-da168579104a" />

<img width="1213" alt="截屏2024-01-20 22 12 48" src="https://github.com/eternallycyf/ims/assets/63464198/f027cf61-c9a8-4c51-89fc-9edb9155a839" />

## ts-node 脚本

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Example",
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
