---
layout: post
title: No valid Oracle clients found. You need at least one 64-bit client properly configured. | Toad for Oracle
author: Casey
date: 2022-11-22
categories: Debugging
tags: toad
---

# No valid Oracle clients found. You need at least one 64-bit client properly configured. | Toad for Oracle


## 錯誤原因

因為我安裝的 Toad 為 64 bit，但是 Oracle Instant Client 為 32 bit，所以需要另外再下載  64 bit 的 Oracle Instant Client。

![Imgur](https://i.imgur.com/y1zyw6j.png)
> 可以從 Help > About 查看 Toad 目前使用 x86 還是 x64

![Imgur](https://i.imgur.com/ZDtrtsm.png)

![Imgur](https://i.imgur.com/EjzuQ47.png)

> 如果之前有安裝過，可以執行 sqlplus.exe 並打開工作管理員之後查看 Oracle Instant Client 的版本

![Imgur](https://i.imgur.com/hkpGsjz.png)

## 解決步驟

1.  到 Oracle 官網下載 [Oracle Instant Client Downloads](https://www.oracle.com/database/technologies/instant-client/downloads.html)，需要注意位元，如果 Toad 安裝 32 bit的版本 ，Oracle Instant Client 也需要安裝 32 bit，如果 Toad 安裝 64 bit的版本 ，Oracle Instant Client 也需要安裝 64 bit。

![Imgur](https://i.imgur.com/WsstnTy.png)

> 這一步很重要，因為容易踩雷!!

2. 因為我的電腦是 Windows 10，再加上我要安裝的 Toad 是64bit 的版本，所以下載 Oracle Instant Client 64 bit的版本。

![Imgur](https://i.imgur.com/qHHb5BA.png)

3.  解壓縮之後長的是這樣

![Imgur](https://i.imgur.com/o1F1zYV.png)

4. 搜尋控制台 

![Imgur](https://i.imgur.com/7FWHaul.png)

5. 搜尋環境 > 點擊編輯系統環境變數

![Imgur](https://i.imgur.com/DVpJrJ8.png)

6. 點「環境變數」

![Imgur](https://i.imgur.com/a96p7m8.png)

7. 點擊 Path > 點擊編輯


![Imgur](https://i.imgur.com/wyFTVcg.png)

8. 點擊新增 > 將剛剛解壓縮的資料夾的檔案路徑貼上> 上移移到第一個 > 按下確定

![Imgur](https://i.imgur.com/3Stsfso.png)

9. 在 Toad 上就可以看到 Connect Using 已經指向我們剛剛安裝的 Oracle Instant Client，這時候在打上伺服器 IP 即可連線成功。  

![](https://blog.toadworld.com/hs-fs/hubfs/instant11.jpg?width=477&name=instant11.jpg) 

## 參考資料

[How to install an Oracle Instant Client for Toad® for Oracle](https://blog.toadworld.com/how-to-install-an-oracle-instant-client-for-toad-for-oracle)