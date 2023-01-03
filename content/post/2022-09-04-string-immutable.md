---
layout: post
title: String values are immutable | JavaScript
author: Casey
date: 2022-09-04 23:12:00 +08:00
categories: Blogging
tags: javascript
---

在 JS 的世界裡面，`string` 是 immutable，表示 `string` 裡面的內容物是不可以變動的。
這是什麼意思，我們看以下的例子就知道。

## 範例

今天我們想要讓 string 這一個字串從 `Jesse` 變成 `Aesse` 該怎麼做?

以下步驟：

- 先設定一個變數叫做 `student`
- 將 `student` assign 給 `Jesse`
- 再將 `student` 的第 0 號位置變成 A

```js
// 先設定一個變數叫做 student 並且 value 設為 Jesse
let student = "Jesse";
console.log(student);

// 將第 0 號位置重新assign，從 J 變成 A
student[0] = "A";
console.log(student);
```

看到這心想應該是沒什麼問題吧，結果拿到 console 一跑，會發現 `student` 怎麼還是 `Jesse`?

![Imgur](https://i.imgur.com/DiLTKFf.png)

會發生這種事情，是因為 string 有 immutabllity，裡面的任何字元都不可以變動。所以使用 `student[0]` assign 是行不通的。

但我們還是很想讓 `Jesse` 變成 `Aesse` 該怎麼做?

其實只要 reassign student 這一個變數即可。

```js
let student = "Jesse";
console.log(student); // Jesse

// 重新 assign 一整個 student 變數
student = "Aesse";
console.log(student); // Aesse
```

![Imgur](https://i.imgur.com/wDljPnr.png)

---

## 參考資料

[string in javascript are immutable, but when we use let with strings , it becomes changeable,](https://stackoverflow.com/questions/65548251/string-in-javascript-are-immutable-but-when-we-use-let-with-strings-it-become)
