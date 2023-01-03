---
layout: post
title: 點擊 Enter 之後，執行某一支 Function | Vue.js
author: Casey
date: 2022-08-31 11:00:00 +08:00
categories: Snippets
tags: vue.js
---

[JSFiddle 範例](https://jsfiddle.net/iosum/tsc069m1/3/)

使用 `v-on:keyup.enter`=`'function name'` 綁定 input 或是 form。

起初寫的時候，以為 `v-on:keyup.enter` 要綁在 button 上，但是實際上其實是 form (或是其他的 input)， 以 form 為主體， trigger Enter 鍵之後，呼叫 login function，即可執行成功。

```html
<div id="app">
  <form v-on:keyup.enter="login">
    <input type="text" />
    <input type="text" />
    <button type="button" @click="login">Login</button>
  </form>
</div>
```

```js
new Vue({
  el: "#app",
  methods: {
    login() {
      alert("CLICKED!");
    },
  },
});
```

參考資料: [On key press of Enter, click a button in vuejs](https://stackoverflow.com/questions/46639549/on-key-press-of-enter-click-a-button-in-vuejs)
