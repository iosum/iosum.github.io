---
layout: post
title: 找不到 bin\roslyn\csc.exe 檔案
author: Casey
date: 2023-02-04
categories: Snippets
tags: ASP.NET
---

## 錯誤訊息

找不到路徑 'D:\xxx\bin\roslyn\csc.exe' 的一部分。

![Imgur](https://i.imgur.com/lOxQsXK.png)

## 解決方法

找到 `packages\Microsoft.CodeDom.Providers.DotNetCompilerPlatform.2.0.0`

![Imgur](https://i.imgur.com/cXkYN3u.png)

進入 `tools`

![Imgur](https://i.imgur.com/ujEHZ3X.png)

進入 `Roslyn45`

![Imgur](https://i.imgur.com/wkHGnrW.png)

貼到專案的 `Bin` folder，並重新命名為 `roslyn`

![Imgur](https://i.imgur.com/U9q8uZU.png)

再重啟專案，即可成功

## 參考資料

[神祕的 ASP.NET bin\roslyn 目錄](https://blog.darkthread.net/blog/aspnet-bin-roslyn-folder/)

[[沒有蠢問題] 找不到路徑 bin\roslyn\csc.exe](https://dotblogs.com.tw/initials/2021/02/11/144248)
