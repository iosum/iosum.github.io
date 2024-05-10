---
layout: post
title: Hugo SEO 設定
date: 2024-05-10
categories: SEO
tags: SEO
draft: true
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



## 參考資料
[Hugo SEO Best Practices](https://cloudcannon.com/tutorials/hugo-seo-best-practices/)