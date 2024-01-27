---
title: nest
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## 使用 chrome 调试

- pnpm start:debug

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/nest-inspect.png)

## 使用 vscode 调试

### 1.nest start --debug --watch

- npm run start:debug
- ./vscode/launch.json

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "nest start --debug",
      "port": 9229,
      "request": "attach",
      "skipFiles": ["<node_internals>/**"],
      "type": "node",
      "console": "integratedTerminal"
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/nest-start-debug.png)

### 2. npm script

- 不需要自己自动项目了
- ./vscode/launch.json

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "npm script",
      "request": "launch",
      "runtimeArgs": ["start", "dev"],
      // 首行断点
      // "stopOnEntry": true,
      "runtimeExecutable": "npm",
      "skipFiles": ["<node_internals>/**"],
      "type": "node",
      "console": "integratedTerminal"
    }
  ]
}
```

### 3. debugger 前端静态资源

- pnpm start:dev

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
      "name": "static",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceRoot}/src/public"
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/nest-static-html.png)

### 4. 使用 canary 调试前端静态资源

- 可以保留浏览器的配置 拓展程序等等
- 电脑根目录执行

```base
/Applications/Google\ Chrome\ Canary.app/Contents/MacOS/Google\ Chrome\ Canary --remote-debugging-port=9222
```

- pnpm start:dev
- 在 canary 浏览器打开 http://localhost:9222

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

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/nest-canary.png)
