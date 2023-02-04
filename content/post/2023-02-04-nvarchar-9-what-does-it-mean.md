---
layout: post
title: NVARCHAR(9) v.s. VARCHAR(9) IN MSSQL
author: Casey
date: 2023-02-04
categories: Blogging
tags: SQL
draft: true
---

## NVARCHAR(9)

在 SQL SERVER 中， NVARCHAR(9) 的 9 代表的是在這一個 COLUMN 中，可以最多放 9 個字元，若未滿 9 個字元，則會補到 9 個字元，長度是固定的。

其中每一個字元都以 2 個 bytes 做計算，NVARCHAR(9) 表示儲存空間為 18 bytes。

以英文和中文，可以是 `abcdefghi`，或是 `aaaaccccd`，`一二三日禮拜拜日日`...等最多擺放 9 個字元，

```sql
DROP TABLE IF EXISTS TEST
CREATE TABLE TEST (
	TEST1 NVARCHAR(9),
	TEST2 VARCHAR(9)
)

INSERT INTO TEST VALUES(N'一二三日禮拜拜日日', '')
INSERT INTO TEST VALUES(N'123456789', '')

```

![Imgur](https://i.imgur.com/OjMQrV0.png)

## VARCHAR(9)

但以中文來說，需要先判斷中文的編碼原則，再去判斷長度，

編碼原則常見的是 UTF-8 和 BIG5，

以 UTF-8 來說，每一個中文字代表 3 個 bytes，

但是 BIG5，每一個中文代表 2 bytes，

不同的編碼，中文的長度會不同，

在 UTF-8 編碼中，`一二` 需要 3+3 bytes = 6 bytes

在 BIG5 編碼中，`一二` 需要 2+2 bytes = 4 bytes

所以在 SQL Server 上設定 NVARCHAR(9)，表示最大可以存 18 bytes，如果中文是以 UTF-8 方式放入 DB，可以最多放 18/3 = 6 個字

如果中文是以 BIG5 方式放入 DB，可以最多放 18/2 = 9 個字

## 參考資料

[請問"李襎"這個字是算幾個 BYTE ??](https://ithelp.ithome.com.tw/questions/10021627)
