---
layout: post
title: 如果我使用網頁觸發按鈕執行 stored procedure，stored procedure 會執行 SSIS dtsx，如果在 stored procedure 執行時將網頁關閉, stored procedure 還會繼續執行嗎?
author: Casey
date: 2023-03-28
categories: Blogging
tags: sql
---

如果在網頁上觸發按鈕執行的 stored procedure 中，執行了一個包含 SSIS 封裝的 dtsx 檔案，當你關閉網頁時，stored procedure 仍然會繼續執行。

這是因為在 SQL Server 中，stored procedure 通常在執行時是作為一個單獨的執行緒在運行的，而這個執行緒是獨立於網頁的。

換句話說，即使你關閉了網頁，stored procedure 仍然會在 SQL Server 上運行，直到其執行完成或被手動停止。

因此，希望停止 stored procedure 的執行，可以使用 SQL Server Management Studio 或 Transact-SQL 命令來停止其執行，具體方法可以參考前面的回答。

## 找到正在執行的 SP ID

找到 session ID

```SQL
SELECT session_id FROM sys.dm_exec_requests WHERE session_id > 50
```

## 停止 Stored Procedure 的執行

`<SPID>` 是指正在執行 stored procedure 的 session ID

```SQL
KILL <SPID>
```
