---
layout: post
title: 使用 Jest 當作前端 Unit Test 的工具
author: Casey
date: 2023-02-16
categories: Blogging
tags: javascript
draft: true
---

## 安裝工具

1. 安裝 `Jest`

```
npm install --save-dev jest
```

2. 安裝 `babel-jest` 和 `@babel/preset-env`

```
npm install --save-dev babel-jest @babel/core @babel/preset-env
```

3. 在 root folder 新增 `babel.config.js`，並將以下 code 貼上

```js
module.exports = {
  presets: [["@babel/preset-env", { targets: { node: "current" } }]],
};
```

## 測試

此 demo 測試 2 數相加 function

1. 新建 `index.html` 檔案，可以看到裡面有 3 個 `<input>`，前面 2 個 input box 相加的結果會顯示在最後一個 input box。

可以看到 `</body>` 的前方有 import 2 個 script，一個是 `index.js`，另外一個是 `functions.js`

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script
      src="https://code.jquery.com/jquery-1.12.4.min.js"
      integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ="
      crossorigin="anonymous"
    ></script>
    <title>Jest Testing Demo</title>
  </head>
  <body>
    <input type="text" id="input-a" />
    <input type="text" id="input-b" />
    <button id="btn-submit">Add</button>
    <input type="text" id="output" />

    <script src="index.js" type="module"></script>
    <script src="functions.js" type="module"></script>
  </body>
</html>

```

1. export 需要測試的 function
2. 在 index.js 中 import 該 function
3. 在 functions.test.js 中，新增 test case

## 參考資料

[Jest - Getting Started](https://jestjs.io/docs/getting-started)
