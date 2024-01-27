---
title: canary
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## canary

- 前端调试使用 canary 浏览器 可以保留浏览器的配置 拓展程序等
- 以 umi 为例

```shell
/Applications/Google\ Chrome\ Canary.app/Contents/MacOS/Google\ Chrome\ Canary --remote-debugging-port=9222
```

- pnpm run start 启动项目
- ./vscode/launch.json

````json
    {
      "name": "针对 localhost 启动 Chrome",
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
      "skipFiles": [
    "${workspaceFolder}/node_modules/**/*.js",
    "<node_internals>/**/*.js"
  ]
    }
    ```
````

- 用 canary 打开 http://localhost:8000

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/canary-umi.png)
