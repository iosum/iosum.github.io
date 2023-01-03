---
layout: post
title: var vs let - Part 1 | JavaScript
author: Casey
date: 2022-09-01 16:20:00 +08:00
categories: Blogging
tags: javascript
---

自從 JS 在 2015 年推出大改版後，相信大家都看過非常多 `var`，`let`，`const` 的文章，雖然現已 2022，但有許多 legacy project 還是使用 var 來定義變數，就讓我們再了解一次 `var` 和 `let` 有何不同吧。

結論：
用 `var` 定義的變數可以輕易的被重新賦值，但是 `let` 不行。

```js
var student = "Jesse";
var student = "Tracy";
console.log(student);
```

這一段程式碼，表示一開始 student 這一個變數是 assign 給 Jesse，但是下一行又將 student 變數 assign Tracy，console.log 出來的結果並沒有 error，是 log Tracy。

![Imgur](https://i.imgur.com/3acP2kJ.png)

雖然這樣 assign 很方便，但是也增加 debug 的困難度，因為如果是大型專案，在寫得時候如果沒有注意到前面有使用，就容易將 variable 重新 assign。

所以 ES6 推出 `let` + `const` 希望能取代 `var`，增加 debug 的效率。

我們來看看如果使用 `let` 在 console 上，會發生什麼事?

```js
let student = "Jesse";
let student = "Tracy";
console.log(student);
```

> Uncaught SyntaxError: Identifier 'student' has already been declared

答案是會有 error，因為 `student` 已經被定義過一遍了，不能再使用 `student` 再定義一次。
如果需要 override `student` 直接 assign 即可。

```js
let student = "Jesse";
student = "Tracy";
console.log(student);
```

![Imgur](https://i.imgur.com/T8l0NQh.png)

---

參考資料：

[Explore Differences Between the var and let Keywords](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/explore-differences-between-the-var-and-let-keywords)

[How the let, const, and var Keywords Work in JavaScript](https://www.freecodecamp.org/news/understanding-let-const-and-var-keywords/)
