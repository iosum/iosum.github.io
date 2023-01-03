---
layout: post
title: 如何讓 flex item 等高? | css
author: Casey
date: 2022-10-03
categories: Blogging
tags: css flexbox
---

[CodePen 完成圖](https://codepen.io/iosum/pen/eYrbJJy?editors=1100)

## 步驟

### Step 1

先畫出理想的 HTML Mark up，簡單來講分成 3 層，最外層紅色的 `.container`，橘色的 `.card`，和螢光綠的 `.card__header`，`.card__body` 和 `.card__footer`。

![Imgur](https://i.imgur.com/xmFgXbu.png)

```html
<div class="container">
  <div class="card">
    <div class="card__header">
      <img
        src="https://source.unsplash.com/600x400/?computer"
        alt="card__image"
        class="card__image"
        width="600"
      />
    </div>
    <div class="card__body">
      <span class="tag tag-blue">Technology</span>
      <h4>What's new in 2022 Techhhhhhhhhhhhhhh</h4>
      <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Saepe
        laudantium eos molestiae porro cum, doloribus, nostrum nisi error fugit
        optio rerum velit, eius sunt placeat vitae! Ipsam a mollitia cupiditate
        error sequi pariatur porro, in cum doloribus commodi voluptates. Nulla
        blanditiis ea dolore voluptas quaerat veniam aut asperiores sed quis.
      </p>
    </div>
    <div class="card__footer">
      <div class="user">
        <img
          src="https://i.pravatar.cc/40?img=1"
          alt="user__image"
          class="user__image"
        />
        <div class="user__info">
          <h5>Jane Doe</h5>
          <small>2h ago</small>
        </div>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card__header">
      <img
        src="https://source.unsplash.com/600x400/?food"
        alt="card__image"
        class="card__image"
        width="600"
      />
    </div>
    <div class="card__body">
      <span class="tag tag-brown">Food</span>
      <h4>Delicious Food</h4>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Sequi
        perferendis molestiae non nemo doloribus. Doloremque, nihil! At ea atque
        quidem!
      </p>
    </div>
    <div class="card__footer">
      <div class="user">
        <img
          src="https://i.pravatar.cc/40?img=2"
          alt="user__image"
          class="user__image"
        />
        <div class="user__info">
          <h5>Jony Doe</h5>
          <small>Yesterday</small>
        </div>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card__header">
      <img
        src="https://source.unsplash.com/600x400/?car,automobile"
        alt="card__image"
        class="card__image"
        width="600"
      />
    </div>
    <div class="card__body">
      <span class="tag tag-red">Automobile</span>
      <h4>Race to your heart content</h4>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Sequi
        perferendis molestiae non nemo doloribus. Doloremque, nihil! At ea atque
        quidem!
      </p>
    </div>
    <div class="card__footer">
      <div class="user">
        <img
          src="https://i.pravatar.cc/40?img=3"
          alt="user__image"
          class="user__image"
        />
        <div class="user__info">
          <h5>John Doe</h5>
          <small>2d ago</small>
        </div>
      </div>
    </div>
  </div>
</div>
```

### Step 2

在 `.container ` 設定 flex container，可以使 `.card`變成 flex item，
加入`flex-wrap: wrap;` 是希望寬度不夠時，flex item 在 ltr 的方向，最右邊的 flex item 可以自己換到下一行。

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
```

![Imgur](https://i.imgur.com/ay9bL1o.png)

### Step 3

希望將 `.card` 裡面的 `.card__header`，`.card__body`，和 `.card__footer` 垂直排列，因此我們需要將 `.card` 變成 flex container，並將 `flex-direction: column`。

在桌機或是筆電的大螢幕下，我們希望 item 可以在一個 row 可以一次顯示 3 個，因此一個 item 的 width 大約是 30%，並隨著螢幕的縮小，每一個 row 所放的 item 愈來愈少，直到一個 row 只有一個 item。

```css
.card {
  display: flex;
  flex-direction: column;
  width: 30%;
  padding: 1rem;
}
```

```css
@media all and (max-width: 768px) {
  .card {
    width: 100%;
  }
}
```

![Imgur](https://i.imgur.com/2RzOoZJ.png)

> 上圖還未加 media query

![Imgur](https://i.imgur.com/TltEhsO.gif)

> 已加入 media query

### Step 4

將照片依照等比例縮小。

```css
.card .card__header .card__image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
```

![Imgur](https://i.imgur.com/ASdrpAa.png)

### Step 5

```css
.card .card__body {
  flex: 1 0 auto;
  margin-top: 0.5rem;
}
```

最重要的步驟，我們需要將 `.card__body` 的高度維持最大化，也就是頭像永遠都會在底部，圖片都會占一定的高度，其他的部分都是 `.card__body`。

---

先來分析 `flex: 1 0 auto;`

```css
flex-grow: 1;
flex-shrink: 0;
flex-basis: auto;
```

`flex-grow: 1;`，預設值爲 0。依照 flex item 的設定比例分配剩餘空間，因為 `flex-grow` 預設值為 0，所以如果只有一個 flex item 設定 `flex-grow: 1`，表示如果有剩餘的空間，會將這空間都分配給設定 `flex-grow: 1` 的 flex item，以這一個例子就是 `.card__body`。

`flex-shrink: 0;`，預設值爲 1，表示空間如果不夠分，flex item 會等比例縮小。如果將 `flex-shrink: 0;`，表示我們要讓 flex item 不隨著 flex container 的大小跟著改變，flex item 該是多大就是多大。以這一個例子，將 `.card__body` 設定為 `flex-shrink: 0;`，並不會壓縮到 `.card__body` 的空間，而是壓到其他 `.card__header` 和 `.card__footer` 的空間。

`flex-basis: auto`，設定 flex item 在 main axis 上的預設大小，如果 main axis 為水平線，表示 flex container 的 `flex-direction: row`，flex-basis 將設定 flex item 的高度。如果 main axis 為垂直線，表示 flex container 的 `flex-direction: column`，flex-basis 將設定 flex item 的寬度。

![Imgur](https://i.imgur.com/uw4iatV.png)

### Step 6

剩下其他的 styling，使用 comment 的方式快速帶過。

```css
/* style h4 標題 */
.card .card__body h4 {
  letter-spacing: 1px;
  font-size: 1.5rem;
  text-transform: capitalize;
  margin-top: 0.5rem;
  /* h4 標題如果超過 2 行，則用 ... 表示 */
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
/* p如果超過 4 行，則用 ... 表示 */
.card .card__body p {
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* 頭像和 username，日期並排 */
.card .card__footer .user {
  display: flex;
  margin-top: 0.5rem;
}

/* 頭像呈現圓形狀 */
.card .card__footer .user .user__image {
  border-radius: 50%;
  margin-right: 0.5rem;
}
```

如果希望 `.card`的 border 有 glassmorphism 的效果，可以在 `.card` 加入以下的 css code。

```css
.card {
  /* 原本有的 */
  display: flex;
  flex-direction: column;
  border: 1px solid red;
  width: 30%;
  padding: 1rem;
  margin-top: 0.5rem;

  /* glassmorphism styling */
  background: rgba(255, 255, 255, 0.2);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
}
```

## 結果圖

![Imgur](https://i.imgur.com/mjLOqX2.gif)

## 參考資料

[An equal height grid using Flexbox](https://clearleft.com/thinking/an-equal-height-grid-using-flexbox)
