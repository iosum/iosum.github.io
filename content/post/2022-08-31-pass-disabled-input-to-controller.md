---
layout: post
title: Disabled Input 傳至 Controller | JavaScript
author: Casey
date: 2022-08-31 11:00:00 +08:00
categories: Snippets
tags: javascript
---

disabled input 是無法將 value 傳至 controller，但是我們仍需要用到 value，此時需要怎麼做?

解決辦法：

1.  將 disabled input 塞進一個 id 或是 class。

2.  在 submit form 的時候，使用 jQuery 的 [removeAttr](https://api.jquery.com/removeattr/) method，將 disabed 這一個屬性拿掉，這樣就可以在 controller 拿到 value 囉。

以下為 pseudo code，請參考。

```c#
@Html.CheckBoxFor(m => m.isUsed, new { @disabled="disabled", @class="disabledCheckbox"} )
```

```js
$("#TestForm").submit(function () {
  $("#CheckBoxId").removeAttr("disabled");
});
```

---

參考資料：
[How do I submit disabled input in ASP.NET MVC?](https://stackoverflow.com/questions/2700696/how-do-i-submit-disabled-input-in-asp-net-mvc/2724483)
