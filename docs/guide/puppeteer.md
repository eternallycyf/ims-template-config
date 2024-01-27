---
title: puppeteer
apiHeader: false
tocDepth: 4
group:
  title: 自动化测试
  order: 0
nav:
  title: 脚本
  order: 0
---

## puppeteer UI 自动化测试

- https://github.com/eternallycyf/Antd-CustomComponent

### utils.tsx

```ts
const fs = require('fs');

/**
 * @param {*} path
 */
async function removeDir(path) {
  if (fs.existsSync(path)) {
    const dirs = [];
    const files = fs.readFileSync(path);
    files.forEach(async (file) => {
      const childPath = `${path}/${file}`;
      if (fs.statSync(childPath).isDirectory()) {
        await removeDir(childPath);
        dirs.push(childPath);
      } else {
        fs.unlinkSync(path);
      }
    });
    dirs.forEach((fir) => fs.rmdirSync(fir));
  } else {
    console.log('no such file or directory, failed to remove');
  }
}

async function goto(page, link) {
  return page.evaluate((link) => {
    location.href = link;
  }, link);
}

async function click(page, selector, timeout = 30000) {
  await page.waitForSelector(selector, { visible: true, timeout });
  let error;
  while (timeout > 0) {
    try {
      await page.click(selector);
      return;
    } catch (e) {
      await page.waitFor(100);
      timeout -= 100;
      error = e;
    }
  }
  throw err;
}

module.exports = {
  removeDir,
  goto,
  click,
};
```

### testConfig.js

```ts
module.exports = {
  domain: 'http://localhost:8000',
  username: 'admin',
  password: 'admin',
};
```

### index.js

```ts
const puppeteer = require('puppeteer');
const path = require('path');
const testConfig = require('./testConfig');
const CommentTable = require('./commonTable/class');
const utils = require('./utils');

(async () => {
  const browser = await puppeteer.launch({
    // 有浏览器界面启动
    headless: false,
    // 放慢浏览器执行速度 方便测试观察
    slowMo: 100,
    devtools: true,
    args: ['--window-size=1480,960', '--unlimited-storage'],
    debuggerPort: 9992,
  });

  const startTime = new Date().getTime();
  const page = await browser.newPage();
  await page.setViewport({
    width: 1480,
    height: 960,
  });

  await utils.goto(page, `${testConfig.domain}/login`);
  await page.waitForNavigation();

  const username = await page.$("input[type='text']");
  await username.type(testConfig.username);
  const password = await page.$("input[type='password']");
  await password.type(testConfig.password);
  const submit = await page.$("button[type='submit']");
  await Promise.all([submit.click(), page.waitForNavigation()]);
  const submitBtn = await page.waitForSelector('.ant-tour-close');
  await submitBtn.click();

  page.on('pageerror', (err) => {
    console.error(err);
  });

  // await utils.removeDir(path.join(__dirname, '/screenshot'));

  let testResList = [];
  let isLastTest = false;

  function handleLastTest(flag) {
    isLastTest = flag;
    return statisticsTestResult;
  }

  function statisticsTestResult(testResult) {
    testResList.push(testResult);
    if (isLastTest) {
      let allCount = 0;
      let passCount = 0;
      testResList.forEach((item) => {
        allCount += item.allCount;
        passCount += item.passCount;
      });

      testResList.push({
        moduleName: '总计',
        allCount,
        passCount,
      });

      console.log('测试结果完成, 统计结果如下:');
      console.table(testResList);

      if (allCount === passCount && passCount > 0) {
        console.log('\x1B[32m%s\x1B[39m', '测试通过');
      }

      const spendTime = (new Date().getTime() - startTime) / 1000;
      console.log('\x1B[32m%s\x1B[39m', `done in ${spendTime}s.`);
    }
  }

  // 非最后的测试用例  handleLastTest(false)  最后的测试用例 handleLastTest(true)
  await CommentTable.CommentTableAddTest(page, handleLastTest(true));

  // await page.close();
  // await browser.close();
})();
```

### commonTable/class.js

```ts
const testConfig = require('../testConfig');
const utils = require('../utils');
const { domain } = testConfig;

async function CommentTableAddTest(page, callback) {
  let allCount = 0;
  let passCount = 0;
  const moduleName = '公众组件class';
  const imgId = Date.now();
  try {
    allCount++;
    await utils.goto(page, `${testConfig.domain}/home/class`, {
      timeout: 5 * 1000,
      waitUntil: [
        'domcontentloaded', // 等待 DOMContentLoaded 事件触发
      ],
    });
    // 等待列表接口请求完成
    await page.waitForRequest(`${domain}/getActivityList?page=1&limit=30&aaaaaa=1&my=121213`);
    const EditBtnElement = '.ant-table-tbody .ant-table-row td:last-child >div >button';
    const SubmitBtn = '.ant-modal-content > div.ant-modal-footer > button.ant-btn.ant-btn-primary';
    const SelectElements = '.ant-modal-content .ant-select';

    await utils.click(page, EditBtnElement);

    const otherFormItemInput = await page.waitForSelector('#otherFormItem', {
      timeout: 2000,
    });
    const keywords = '测试';
    await otherFormItemInput.type(keywords, { delay: 100 });

    const typeSelect = await page.$$(SelectElements);
    await typeSelect[0].click();
    await handleDropdownSelect(page, 1);

    await utils.click(page, SubmitBtn);
    page.on('response', (response) => {
      response
        .json()
        .then((data) => {
          const resCode = Number(data.code);
          const apiUrl = response.url();
          const checkApiPass = apiUrl === `${domain}/updateActivityList`;
          if (resCode !== 200) {
            console.error({
              msg: data.msg,
              code: data.code,
              title: '测试不通过',
              module: moduleName,
            });
            page.screenshot({
              path: `./test/screenshot/${moduleName}${imgId}.png`,
            });
          } else if (resCode === 200) {
            if (checkApiPass) passCount++;
          }
          if (checkApiPass) {
            callback({
              allCount,
              passCount,
              moduleName,
            });
          }
        })
        .catch((err) => {
          console.error('err', err);
          callback({
            allCount,
            passCount,
            moduleName,
          });
          page.screenshot({
            path: `./test/screenshot/${moduleName}${imgId}.png`,
          });
        });
    });

    callback({
      allCount,
      passCount,
      moduleName,
    });
    page.screenshot({
      path: `./test/screenshot/${moduleName}${imgId}.png`,
    });
  } catch (error) {
    console.error('error', error);
  }
}

async function handleDropdownSelect(page, selectedIndex) {
  const allDownList = await page.$$('.ant-select-dropdown');
  const optionsList = await allDownList[allDownList.length - 1].$$('.ant-select-item');
  const selectedItem = optionsList[selectedIndex];
  await selectedItem.click();
}

module.exports.CommentTableAddTest = CommentTableAddTest;
```

### package.json

```json
{
  "scripts": {
    "autotest": "node test"
  },
  "dependencies": {
    "puppeteer": "^19.7.3"
  }
}
```
