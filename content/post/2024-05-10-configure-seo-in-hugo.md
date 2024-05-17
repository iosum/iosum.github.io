---
layout: post
title: Hugo SEO 設定
date: 2024-05-10
categories: SEO
tags: SEO
draft: true
canonical: https://www.caseyho.dev/post/2024-05-10-configure-seo-in-hugo/
---

## 設定 meta title

這是為了讓 Google 搜尋時的標題。

![Imgur](https://i.imgur.com/5KYU6Qk.png)

在 Hugo 中，通常都會有 `config.toml` 的檔案可以做設定。

`title = "爆肝工程師 Casey"`

顯示的話，可以由 html 的 `<head>` 底下的 `<title>` 看有沒有設定到。

`<title>{{with.Title}}{{.}} | {{end}}{{.Site.Title}}</title> `

## 使用 meta description

描述這個網站是是做什麼的。英文大約 100 ~ 150 英文字，中文大約是 75 字以內。

![Imgur](https://i.imgur.com/v7WX3uN.png)

在 Hugo 中，可以在 `config.toml` 檔案加入 `description`。

![img](https://i.imgur.com/QOQUvuq.png)

在 `layouts\partials\head\head.html` 可以加入

```html
<meta name="description" content="{{ site.Params.Description }}" />
```

![Img](https://i.imgur.com/hXeNhHQ.png)

## 設定標準 URL (Canonical URL)

設定標準 URL（Canonical URL）就是告訴搜尋引擎：「這個網頁是主要的版本，請優先顯示它。」

```html
<link rel="canonical" href="https://www.example.com/main-page">
```

可以在每一個 Post 加上canonical

```
---
title: "My Article"
date: 2024-05-17
canonical: "https://www.example.com/my-article"
---

```

## 使用 Pagination meta tags

當一個網站的內容被分成多個頁面時，比如一篇很長的文章分成多個頁面，搜尋引擎可能不知道這些頁面之間的關係。這樣會影響搜尋引擎對這些頁面的理解和排名。

使用 pagination meta tags 可以告訴搜尋引擎這些頁面之間的關係，幫助它們更好地理解和索引你的網站。

這些標籤有兩種：

`rel="prev"`：告訴搜尋引擎這個頁面**前面**還有一個頁面。

`rel="next"`：告訴搜尋引擎這個頁面**後面**還有一個頁面。

這樣做的好處包括：

- 更好的索引：搜尋引擎可以更好地理解內容的結構，將這些頁面視為一個整體。
- 提升排名：有助於提升分頁內容在搜尋引擎中的排名，因為搜尋引擎知道這些頁面之間的關係。
- 更好的用戶體驗：讓搜尋引擎知道如何導航這些頁面，可以幫助使用者更容易找到他們需要的內容。



## 參考資料
[Hugo SEO Best Practices](https://cloudcannon.com/tutorials/hugo-seo-best-practices/)