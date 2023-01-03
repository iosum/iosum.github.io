---
layout: post
title: SSIS ValidateExternalMetaData | SSIS
author: Casey
date: 2022-09-30
categories: Blogging
tags: ssis
---

## 說明

從打開封裝，拉 component，到執行封裝，這一段的過程都要驗證資料是否正確。

![Imgur](https://i.imgur.com/F3XI5P7.png)

> 此圖為官方版說明。

如果 `ValidateExternalMetadata = True`，在設計封裝的時候， SSIS 就會連到外面的資料庫來比對資料正不正確，所以就會有紅色的 X。

![Imgur](https://i.imgur.com/43ySl7K.png)

設定 `ValidateExternalMetadata = False`，在設計封裝的時候， SSIS 就不會比對外部的資料正不正確，直到執行這一個 OLEDB 的時候才會驗證資料。

![Imgur](https://i.imgur.com/cUXgypX.png)
