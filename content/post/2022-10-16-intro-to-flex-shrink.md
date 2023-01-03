---
layout: post
title: flex-shrink 屬性介紹 | css
author: Casey
date: 2022-10-16
categories: Blogging
tags: css flexbox
---

## 介紹

flex-shrink 只適用於 flex item 上。

當使用 `flex-shrink` 時，如果 flex container 的長寬太小，設定 flex shrink 可以允許 flex item 縮小。
當 flex container 的寬度小於其中所有 flex item 的相加起來的寬度時，flex item 就會縮小。

flex-shrink 的屬性值為數字。數字越大，flex item 會縮小得越多。

例如有一個 flex item 的 `flex-shrink: 1`，而另一個 flex item 的 `flex-shrnk: 3`，則 `flex-shrink: 3`的 flex item 將縮小原本自己寬度四分之三， `flex-shrink: 1` 的 flex item 將縮小原本自己寬度四分之三。

`flex-shrink` 定義空間不夠時各個元素如何收縮。`flex-shrink: 1` 為預設值。

## 範例

[CodePen](https://codepen.io/iosum/pen/KKRqopm?editors=1100)

```css
html {
  box-sizing: border-box;
}
.flex-container {
  width: 1000px;
  height: 500px;
  display: flex;
  background-color: violet;
}

.flex-container > div {
  padding: 20px;
  background-color: aqua;
  margin: 10px;
  width: 200px;
  height: 30px;
  flex-shrink: 1;
}
```

![Imgur](https://i.imgur.com/xM71yI1.png)

可以看到每一個 flex item 的 width = `width: 200px` + `padding: 20px` x 2 (左右 2 邊) + `margin: 10px` x 2 =` 260px`。

5 個 flex item 表示總共的 width 為 260px x 5 = 1300px

但是 flex container 的 width 也才 1000px，多出來 1300px - 1000px = 300px，這時候我們想要讓 flex item 依照我們想要的比例縮小時該怎麼做?

具體的計算方式為：
每個元素收縮的權重為 flex item 的 flex-shrink 乘上自己的寬度。

> 打到這邊我自己也看好久，看範例會比較容易理解。

以這一個範例，總權重(每一個 flex item 的寬度乘上 flex shrink 的值)為 1 x 260 + 2 x 260 + 1 x 260 + 1 x 260 + 1 x 260 = 1560

我們剛剛有算出了已經超過 300px，那這 300px 將由 5 個 flex item 依比例分攤，現在看到 css code，第 2 個 flex item 的 `flex-shrink: 2`。

第一個 flex item 計算方式：
300(總共超過多少) x 1 (第一個 flex item 的 flex-shrink，因為無設定，所以為預設值 1) x 260 (第一個 flex item 的 width) / 1560(總權重) = -50px

原本 260px - 50px = 210px = 第一個 flex item shrink 完的總寬度。
可以對照以下的圖片，第一個 flex item shrink 完的 width 是 210px。

![Imgur](https://i.imgur.com/XZo5DiJ.png)

那我們來計算第 2 個 flex item 真實的 width 為多少。

第 2 個 flex item 計算方式：
300(總共超過多少) x 2(第 2 個 flex item 的 flex-shrink: 2) x 260 (第 2 個 flex item 的 width) / 1560 (總權重) = -100px

原本 260px - 100px = 160px = 第 2 個 flex item shrink 完的總寬度。
可以對照以下的圖片，第 2 個 flex item shrink 完的 width 為 160px。

![Imgur](https://i.imgur.com/Ms9ND66.png)

那麼 flex item 3 ~ flex item 5 都和 flex item 1 的計算方式一樣，這裡就不多贅述。
