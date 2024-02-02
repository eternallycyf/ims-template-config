---
title: patch-package
apiHeader: false
tocDepth: 4
group:
  title: script
  order: 0
nav:
  title: 脚本
  order: 0
---

## patch-package

- 有时候我们需要修改 node_modules 下的一些代码
- 但是 node_modules 不会提交到 git 仓库，改动保存不下来
- 这时候我们可以使用 patch-package 来解决这个问题

```shell
修改xxx文件夹下面的源码
npx patch-package xxx
# ./patches/xxx+1.0.0.patch 文件会被创建 记录着对这个包的改动。

# 这个 patches 目录是可以提交到 git 仓库的，然后再次把项目拉下来的时候，执行下 npx patch-package 就会应用这次改动

# 可以把它配到 postintsll 里，每次安装完依赖自动跑。

# package.json
{
  "scripts": {
    "postinstall": "npx patch-package"
  }
}
```

## FAQ

### pnpm 不支持 patch-package

- pnpm 内置 [patch](https://pnpm.io/cli/patch)、patch-commit 命令
