---
layout: post
title: 使用 SSIS 的 RetainSameConnection 屬性 | SSIS
author: Casey
date: 2022-09-27
categories: Blogging
tags: sql ssis
---

![Imgur](https://i.imgur.com/peQjqbW.png)

## RetainSameConnection 的預設值為 False，為什麼?

當`RetainSameConnection=false`，SSIS 的每個工作在開始使用和資料庫連線時才會打開連線，在工作結束時，關閉連線。

因此每個工作都會打開和關閉連線，且每個工作所使用的連線都是不同的。

![Imgur](https://i.imgur.com/dd6cnVp.png)

以上面的圖片，`執行 SQL 工作`和`資料流程工作`的連線就會不是同一條，即便他們都是連到同一個資料庫。

當初的用意應該是如果`執行 SQL 工作`和`資料流程工作`用的是不同的資料庫連線，例如`執行 SQL 工作`連到的是 ORACLE DB，`資料流程工作`連到的是 SQL SERVER，當`執行完執行 SQL 工作`完成時，`資料流程工作`其實用不到 ORACLE 的連線，所以就會在完成`執行 SQL 工作`結束時關閉連線。

這也是合理的，因為有一些工作流程可能是打開檔案，發送信件，那麼打開檔案，發送信件這一些工作就不需要資料庫的連線，因此也不會浪費資源。

## Temp Table

當`RetainSameConnection=true`，表示只要一執行封裝，連線就會打開，直到整個封裝執行結束。以剛剛的圖做舉例，如果我們在`執行 SQL工作`裡面新增一個 Temp Table，那麼`資料流程工作`也可以存取這一個 Temp Table，因為`執行 SQL工作`和`資料流程工作`連線是一樣的，資源還沒有被釋放掉，Temp Table 還會存在 DB 裡面。

但是如果`RetainSameConnection=false`，表示每一個的工作連線都是獨立的，如果在`執行 SQL工作`新增 Temp Table，`資料流程工作`就不會存取到這一個 Temp Table，因為 Temp Table 早就因為`執行 SQL工作`結束跟著一起被連線釋放掉。

## 參考資料

[What is the RetainSameConnection Property of OLEDB Connection in SSIS?](http://www.sqlerudition.com/what-is-the-retainsameconnection-property-of-oledb-connection-in-ssis/)

[使用 Connetion 的屬性 RetainSameConnection](https://blog.csdn.net/p77ll9l53x/article/details/71108120)
