---
title: 自动生成路由
apiHeader: false
tocDepth: 4
group:
  title: script
  order: 0
nav:
  title: 脚本
  order: 0
---

## ts-node scripts/generateBizConfig.ts

## biz-stage-config.ts.ejs

```html
//本文件是自动生成，请勿修改 <% plugins.forEach(function(plugin) { %>import <%= plugin.name %> from
'../pages/<%= plugin.name %>/routes'; <% }); %> export default [ <%
plugins.forEach(function(plugin){ %> <%= plugin.name %>, <% }); %>];
```

## generateBizConfig.ts

```ts
const fs = require('fs');
const path = require('path');
const chalk = require('chalk');
const ejs = require('ejs');
type IBusinessList = { name: string; path: string }[];
function getAllBiz(source: string): IBusinessList {
  if (!fs.existsSync(source)) {
    console.log(chalk.yellow(`目录不存在${source}`));
    return [];
  }
  const folders: string[] = fs.readdirSync(source);
  const bizList: IBusinessList = [];
  folders.forEach((item) => {
    const itemPath = path.resolve(__dirname, `../src/pages/${item}/`);
    bizList.push({
      name: item,
      path: itemPath,
    });
  });
  return bizList;
}
const targetFile: string = path.resolve(__dirname, '../src/routes/routes.ts');
const bizPath: string = path.resolve(__dirname, '../src/pages');
const templatePath: string = path.resolve(__dirname, './biz-stage-config.ts.ejs');

console.log(chalk.green(`配置插件...`));

const template: Buffer = fs.readFileSync(templatePath, 'utf8');
const bizList: IBusinessList = getAllBiz(bizPath);
const result = ejs.render(template, { plugins: bizList });

fs.writeFile(targetFile, result, (err: NodeJS.ErrnoException) => {
  if (err) {
    console.error('write file error', err);
  } else {
    console.log(chalk.green(`配置插件完成: ${targetFile}\n`));
  }
});
```
