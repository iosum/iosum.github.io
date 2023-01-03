---
layout: post
title: 如何讓 image 塞進一個 div 裡面並維持解析度? | css
author: Casey
date: 2022-10-03
categories: Blogging
tags: css
---

![Imgur](https://i.imgur.com/l2ctqUP.png)

## 範例

[CodePen 範例](https://codepen.io/iosum/pen/poVVYOG?editors=1100)

```html
<div class="img-wrap">
  <img
    src="https://images.unsplash.com/photo-1615147342761-9238e15d8b96?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1001&q=80"
    alt=""
  />
</div>
```

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
}

.img-wrap {
  border: 1px solid green;
  width: 50%;
  height: 50%;
}

.img-wrap img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}
```

## 解說

1. 先設定圖片的容器的 `width` 和 `height`

   > 使用絕對單位或是相對單位都可以

2. 將 img 設定 `width: 100%;` `height: 100%;`
   可以將 img 吃到父元素的高度 100%，寬度 100%

3. 使用 `object-fit` 可以決定圖片填滿方式的屬性
   `object-fit: contain;` 可以保持圖片原有寬高比例進行縮放，使圖片顯示完整。
   > 更多 `object-fit` 的屬性介紹可以參考[這裡](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)

## 參考資料

[How do I fit an image (img) inside a div and keep the aspect ratio?](https://stackoverflow.com/questions/4394309/how-do-i-fit-an-image-img-inside-a-div-and-keep-the-aspect-ratio)

[mdn web docs - object-fit](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)
