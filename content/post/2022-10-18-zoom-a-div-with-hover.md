---
layout: post
title: Hover div 的時候放大圖片 | css
author: Casey
date: 2022-10-17
categories: Blogging
tags: css
---

## 預設結果

此為我們要做的結果圖。

![Imgur](https://i.imgur.com/JyJAMJJ.gif)

## background-position

background-position 用來設定背景圖片位置，如果只指定 x 軸位置，y 軸位置必定為 center。

```css
background-position: x軸位置 y軸位置;
```

```css
/* 靠左靠下對齊 */
background-position:left bottom;　
/* 離左邊 30px，離上方 60px 的位置 */
background-position:30px 60px;　
/* 離左邊 10%，離上方 50% 的位置  */
background-position:10% 50%;　
```

## CodePen 範例

[CodePen](https://codepen.io/iosum/pen/dyeLEEb?editors=1100)

```html
<div class="wrapper">
  <div class="frame"></div>
  <div class="frame"></div>
  <div class="frame"></div>
  <div class="frame"></div>
</div>
```

```css
.wrapper {
  /* 使用 flex 讓 flex item 呈現由左到右的排列 */
  display: flex;
  /* 增加一點空間在 flex item 的周圍 */
  justify-content: space-around;
}

.frame {
  /* 將每一個 div 寬度設定為 100px */
  width: 100px;
  /* 將每一個 div 高度設定為 150px */
  height: 150px;
  /* 設定背景圖片 */
  background-image: url("https://picsum.photos/200/150");
  /* 將背景圖片位置置中 */
  background-position: center;
  /* 設定邊框顏色及寬度 */
  border: 1px solid #ecf1f4;
  /* 設定邊框的圓角 */
  border-radius: 24px;
  /* 在:hover時增加動畫效果 */
  transition: 0.5s;
}

.frame:hover {
  /* 在:hover時寬度變成 200px */
  width: 200px;
}
```

## 參考資料

[how to zoom a div with :hover but not the image inside](https://stackoverflow.com/questions/74105081/how-to-zoom-a-div-with-hover-but-not-the-image-inside)
