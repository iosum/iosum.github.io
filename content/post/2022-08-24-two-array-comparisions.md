---
layout: post
title: 2 陣列中找出至少有一個相同之元素 | JavaScript
author: Casey
date: 2022-08-24 14:14:00 +08:00
categories: Snippets
tags: javascript
---

使用 `Array.prototype.some()` 和 `Array.prototype.filter()`，找出 2 個 array 至少有一個相同的元素。

- `some()` 接收到的參數是一組公式，如果 `array` 的某一個元素有符合此公式，立即回傳 `true`，如遍歷整個 `array` 都找不到則回傳 `false`。

- `filter()` 接收到的參數也是一組公式，不過跟 `some()` 不一樣的地方是 `filter()` 經過公式的運算後，會回傳一個新的陣列。

範例：

```js
var result1 = [
  { id: 1, name: "Sandra", type: "user", username: "sandra" },
  { id: 2, name: "John", type: "admin", username: "johnny2" },
  { id: 3, name: "Peter", type: "user", username: "pete" },
  { id: 4, name: "Bobby", type: "user", username: "be_bob" },
];

var result2 = [
  { id: 2, name: "John", email: "johnny@example.com" },
  { id: 4, name: "Bobby", email: "bobby@example.com" },
];

// 找出 result1 和 result2 相同的 id 之後
// 回傳一個新 array
result1.filter((o1) => result2.some((o2) => o1.id === o2.id));

// 找出 result1 和 result2 不同的 id 之後
// 回傳一個新 array
result1.filter((o1) => !result2.some((o2) => o1.id === o2.id));
```

結果圖：
![Imgur](https://i.imgur.com/eJbzYgV.png)

![Imgur](https://i.imgur.com/yNIjuzY.png)

---

## 參考資料：

[mdn web docs - Array.prototype.some()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

[mdn web docs - Array.prototype.filter()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/filter#%E5%98%97%E8%A9%A6%E4%B8%80%E4%B8%8B)
