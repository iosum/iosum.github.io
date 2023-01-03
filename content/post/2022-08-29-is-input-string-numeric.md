---
layout: post
title: 確認 input string 是否為數字 | JavaScript
author: Casey
date: 2022-08-29 23:11:00 +08:00
categories: Snippets
tags: javascript
---

從 `string` data type 轉成 `int` 中間出的變化會非常多，有可能 input string 是空字串， input string 也有可能是 backctick...等，一堆很奇怪的符號，這邊我使用我自己在專案中有使用的，並不保證大家都能夠判斷正確。

- `parseFloat`(input string)

- 檢查是否為 `NaN`

  - 如果是，則不是 Numeric Value

  - 反之，則是 Numeric Value

```js
function isNumeric(str) {
  if (typeof str != "string") return false; // we only process strings!
  return (
    !isNaN(str) && // use type coercion to parse the _entirety_ of the string (`parseFloat` alone does not do this)...
    !isNaN(parseFloat(str))
  ); // ...and ensure strings of whitespace fail
}
```

---

參考資料: [How can I check if a string is a valid number?](https://stackoverflow.com/questions/175739/how-can-i-check-if-a-string-is-a-valid-number)
