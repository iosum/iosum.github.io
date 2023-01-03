---
layout: post
title: web.config 無法存檔，跳出另存新檔視窗 | c#
author: Casey
date: 2022-09-22 23:00:00 +08:00
categories: Debugging
tags: c#
---

![Imgur](https://i.imgur.com/EQjo1Cn.png)

問題：

當 `web.config` 需要存檔時，會跳出另存新檔的視窗，且再存檔時，會跳出「由於另一個處理序正在使用檔案」。

解決方案：

![Imgur](https://i.imgur.com/85ei6GI.png)

開啟工作管理員， 將 Microsoft.VisualStudio.Web.Host.exe 結束工作即可。
