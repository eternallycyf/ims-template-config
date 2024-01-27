---
title: next
apiHeader: false
tocDepth: 4
group:
  title: vscode
  order: 0
nav:
  title: 脚本
  order: 0
---

## next

```shell
pnpm dev

/Applications/Google\ Chrome\ Canary.app/Contents/MacOS/Google\ Chrome\ Canary --remote-debugging-port=9222
```

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "后端",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev"
    },
    {
      "name": "前端",
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
      "skipFiles": ["${workspaceFolder}/node_modules/**/*.js", "<node_internals>/**/*.js"]
    }
  ]
}
```

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/next-terminal.png)

![](https://raw.githubusercontent.com/eternallycyf/ims-template-config/master/public/images/debugger/next-client.png)
