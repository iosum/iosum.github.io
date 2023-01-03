---
layout: post
title: CSS positioning 介紹 | css
author: Casey
date: 2022-10-17
categories: Blogging
tags: css
---

## 介紹

`position` 屬性用於 HTML 元素的**定位方法**，再搭配使用 `top`、`bottom`、`left` 和 `right` 屬性定位。

但是，除非首先設置了 `position` 屬性，否則 `top`、`bottom`、`left` 和 `right` 屬性將不起作用。

以下為 `position` 屬性值：

- `position: static`
- `position: relative`
- `position: fixed`
- `position: absolute`
- `position: sticky`

## Static Positioning

`position: static` 是 HTML 元素的預設值。

任何套用 `position: static;` 的元素「不會被特別定位」在頁面上特定位置，而是照著瀏覽器預設的設定自動排版在頁面上。

`position: static;` 的元素不受 `top` 、 `right` 、 `bottom` 和 `left` 屬性影響。

### 範例

[CodePen](https://codepen.io/iosum/pen/JjvVXyx)

可以看到加上了 `position: static;`之後，元素依然在相同的位置。

![Imgur](https://i.imgur.com/pRQ92d4.png)

## Relative Positioning

`position: relative;` 的元素和 `position: static`的元素 十分類似，`position: relative;`的元素可以讓開發者修改元素的最終位置。

`position: relative;` 的元素必須加上`top` 、 `right` 、 `bottom` 和 `left` 屬性，才能修改元素的最終位置，使元素相對於**原本元素該出現的位置**進行定位。

而不管這些「相對定位」過的元素如何在頁面上移動位置或增加了多少空間，都不會影響到原本其他元素所在的位置。

### 範例

[CodePen](https://codepen.io/iosum/pen/KKRNgOy?editors=1100)

```css
.relative {
  position: relative;
  top: 20px;
  left: 10px;
}
```

可以看到加了 `.relative` 的 `.box2`，`.box2` 會**相對於原本的位置**向下移動 20px，向右移動 10px，表示離上方 20px，左邊 10px。

也可以看到 `.box2` 已經疊在 `.box3` 上方，表示 `.box3` 並沒有因為 `.box2`有移動跟著移動。

![Imgur](https://i.imgur.com/i3N3QRZ.png)

如果把 `.relative` 拿掉，表示沒有特別定位，`.box2`元素就會回到原本的位置。

![Imgur](https://i.imgur.com/ZTTKirX.png)

## Fixed Positioning

設定為 `position: fixed` 的元素是相對於**視窗**進行定位，即使往下 scroll 或是往上 scroll，元素都同一位置，不會隨著滾動而有所改變。

可以搭配 `top` 、 `right` 、 `bottom` 和 `left` 屬性將此元素定位在瀏覽器的某一個地方。

### 範例

[CodePen](https://codepen.io/iosum/pen/YzLpLWJ?editors=1100)

可以看到範例，即便我是把要固定的元素放在文字裡面，我還是會相對於瀏覽器視窗做定位。

![Imgur](https://i.imgur.com/cVcVIpz.gif)

## Absolute Positioning

需要注意以下 3 件事情：

- 剩下的元素向上移動
- 寬度變化
- 相對於哪一個元素定位

### 注意事項

#### 剩下的元素向上移動

設定為 `position: absolute;` 的元素，會完全跳脫該頁面，會感覺像浮在頁面之上。

所以，設定為 `position: absolute;` 的元素原本所占用的空間將會消失，在 `position: absolute;` 以後的元素將會往上移動。

#### 寬度變化

我們一開始沒有設元素的寬度，所以寬度會完全撐開至父元素的邊界，這是 block 元素的特性。

當設定為 `position: absolute;` 的元素跳脫該頁面後，也意味著，它脫離了父元素的範圍，寬度就以內容為基準。

#### 相對於哪一個元素定位

當元素的 position 設定 `position: absolute `後，
該元素就會往外層的元素找是否有 `position:relative`、`position: absolute` 、`position: fixed` 和 `position: inherit` (若繼承的是前面 3 個之一)的元素，若是都沒有，就會以該網頁頁面(`<body>`)的左上角為定位點。

若沒有設定任何 `top` 、 `right` 、 `bottom` 和 `left` 屬性，設定為 `position: absolute;` 的元素的位置將遵照原本的位置(`position: static`)，但依舊會跳脫原本頁面。

### 範例

[CodePen](https://codepen.io/iosum/pen/NWMdxqQ?editors=1100)

#### 原圖

下圖為原本元素的定位。

```html
<div class="wrapper ">
  <div class="box1 ">
    box 1 Lorem ipsum dolor sit amet consectetur adipisicing elit. Vero totam
    eaque mollitia explicabo cum aut sint ut nam enim deserunt!
  </div>
  <div class="box2">box 2 Lorem ipsum dolor sit amet</div>
  <div class="box3">
    box 3 Lorem ipsum dolor sit amet, consectetur adipisicing elit.
    Voluptatibus, quis. Lorem ipsum dolor sit, amet consectetur adipisicing
    elit. Cum voluptates veniam fuga, cupiditate ipsam laboriosam!
  </div>
</div>
```

```css
.wrapper {
  border: 5px solid #046865;
  height: 200px;
}

.box1 {
  background-color: #e53d00;
}

.box2 {
  background-color: #ffe900;
}

.box3 {
  background-color: #21a0a0;
}
```

![Imgur](https://i.imgur.com/h4EopGQ.png)

---

#### 範例 1 - 在 box 2 加上 `position: absolute;`

```html
<div class="wrapper ">
  <div class="box1 ">
    box 1 Lorem ipsum dolor sit amet consectetur adipisicing elit. Vero totam
    eaque mollitia explicabo cum aut sint ut nam enim deserunt!
  </div>
  <div class="box2 absolute">box 2 Lorem ipsum dolor sit amet</div>
  <div class="box3">
    box 3 Lorem ipsum dolor sit amet, consectetur adipisicing elit.
    Voluptatibus, quis. Lorem ipsum dolor sit, amet consectetur adipisicing
    elit. Cum voluptates veniam fuga, cupiditate ipsam laboriosam!
  </div>
</div>
```

```css
.wrapper {
  border: 5px solid #046865;
  height: 200px;
}

.box1 {
  background-color: #e53d00;
}

.box2 {
  background-color: #ffe900;
  position: absolute;
}

.box3 {
  background-color: #21a0a0;
}
```

可以看到 `.box2` 加上了 `position: absolute` 之後，後面的 `.box3` 會跑上來，因為 `.box2` 已經有自己獨立的一層。

寬度的部分也因為 `.box2` 沒有設定絕對寬度，再加上脫離父元素(`.wrapper`)，所以`.box2`寬度等於該內容寬度。

![Imgur](https://i.imgur.com/g53E5JM.png)

---

#### 範例 2 - 在 box 2 加上 `position: absolute;` 再加上 `top: 0`

如果在 `.absolute` 上面加上 `top: 0`，可以看到因為父元素 `.wrapper` 的 `position: static`，所以 `.box2` 並不會相對於`.wrapper` 的位置進行定位，反而是相對定位於左上角的 `<html>`。

```css
.wrapper {
  border: 5px solid #046865;
  height: 200px;
}

.box1 {
  background-color: #e53d00;
}

.box2 {
  background-color: #ffe900;
  position: absolute;
  top: 0;
}

.box3 {
  background-color: #21a0a0;
}
```

![Imgur](https://i.imgur.com/iFfASvR.png)

---

#### 範例 3 - 在 box 2 加上 `position: absolute;` 再加上 `top: 0`，在父元素`.wrapper` 加上 `position: relative`

如果在 `.wrapper` 上面加上 `position: relative;`，可以看到 `.box2` 會相對於`.wrapper` 的位置進行定位。

```css
.wrapper {
  border: 5px solid #046865;
  height: 200px;
  position: relative;
}

.box1 {
  background-color: #e53d00;
}

.box2 {
  background-color: #ffe900;
  position: absolute;
  top: 0;
}

.box3 {
  background-color: #21a0a0;
}
```

![Imgur](https://i.imgur.com/l7lVWg4.png)

## Sticky Positioning

`position: sticky;`是一個比較新的屬性，如果要支援舊瀏覽器或是 IE，需要使用別的方法。詳細瀏覽器支援可以參考 [Can I Use...](https://caniuse.com/?search=position%3Asticky)。

使用 `position: sticky;` 的元素會根據**使用者的 scroll bar 位置**進行定位。

`position: sticky;` 的元素有點像是 `position: relative` 和 `position: fixed` 之間做切換。
在預設時有 `position: relative`，但 scroll 到某一位置時，該元素會變成 `position: fixed`，一直固定在瀏覽器的某一個位置。

### 範例

[CodePen](https://codepen.io/iosum/pen/GRdrpqM)

可以看到一開始時，紅色底色的 `div` 被定位在某一個位置，但是當我 scroll 到某一個地方的時候，紅色底色的 `div` 就好像使用了`position: fixed`，將 `div` 一直定位在上方。

![Imgur](https://i.imgur.com/8zuS1NO.gif)

## 參考資料

[CSS 布局 - position 属性](https://www.w3school.com.cn/css/css_positioning.asp)

[學習 CSS 版面配置](https://zh-tw.learnlayout.com/)

[CSS 定位詳解](http://www.ruanyifeng.com/blog/2019/11/css-position.html)

[CSS relative? absolute? 傻傻分不清楚](https://ithelp.ithome.com.tw/articles/10212202)
