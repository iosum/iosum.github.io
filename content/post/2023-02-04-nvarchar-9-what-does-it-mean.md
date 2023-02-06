---
layout: post
title: NVARCHAR(9) v.s. VARCHAR(9) IN MSSQL
author: Casey
date: 2023-02-04
categories: Blogging
tags: SQL
---

## NVARCHAR(9)

在 MSSQL 中， NVARCHAR(9) 的 9 代表的是在這一個 COLUMN 中，可以最多放 9 個字元，若未滿 9 個字元，則會補到 9 個字元，欄位長度是固定的。

以英文和中文，可以是 `abcdefghi`，或是 `aaaaccccd`，`一二三日禮拜拜日日`...等最多擺放 9 個字元。

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

如果輸入大於 9 個字元，會出現以下錯誤訊息

![Imgur](https://i.imgur.com/vPcOHKY.png)

### 儲存空間

nvarchar(n)：(2 \* n + 2) bytes

不管是英文或中文，每一個字元都以 2 個 bytes 做計算，NVARCHAR(9) 表示儲存空間為 18 bytes + 2 byes，其中 2 bytes 為地址位置。

## VARCHAR(9)

### 判斷規則

1. 判斷 Character set 是否可以存中文

   在 MSSQL 中，VARCHAR 是可以儲存中文的，只是 MSSQL 預設的 Character set 是 `Latin1_General_CI_AS`，是無法儲存中文的，

   須將 Character set 變成 `Chinese_Taiwan_Stroke_CI_AS` 或是其他可以相容中文的 Character set

2. 判斷編碼原則，計算最多可以放入幾個中文字

   以中文來說，需要先判斷中文的編碼原則，再去判斷長度，

   編碼原則常見的是 UTF-8 和 BIG5，

   以 UTF-8 來說，每一個中文字代表 3 個 bytes，

   但是 BIG5，每一個中文代表 2 bytes，

   不同的編碼，中文的長度會不同，

   在 UTF-8 編碼中，`一二` 需要 3+3 bytes = 6 bytes

   在 BIG5 編碼中，`一二` 需要 2+2 bytes = 4 bytes

   所以在 MSSQL 上設定 VARCHAR(9)，如果中文是以 UTF-8 方式放入 DB，可以最多放 9/3 = 3 個字

   如果中文是以 BIG5 方式放入 DB，可以最多放 9/2 = 4 個字

```sql
DROP TABLE IF EXISTS TEST
CREATE TABLE TEST (
	TEST1 NVARCHAR(9),
	TEST2 VARCHAR(9)
)

INSERT INTO TEST VALUES(N'一二三日禮拜拜日日', '一二三日')
INSERT INTO TEST VALUES(N'123456789', '123456789')

```

![Imgur](https://i.imgur.com/TQDC0op.png)

### 儲存空間

#### 中文

因為我在 varchar 放入中文，再加上中文一個字為 2 bytes，所以 varchar(9)的儲存空間為 2\*9+2 = 20 bytes，其中 2 是用來記住地址

varchar(n)：(2 \* n + 2) bytes

#### 英文

varchar(n)：(n + 2) bytes

## 參考資料

[請問"李襎"這個字是算幾個 BYTE ??](https://ithelp.ithome.com.tw/questions/10021627)

[[MSSQL] 欄位開立(1) - nvarchar, varchar, nchar, char 的抉擇](https://dotblogs.com.tw/henryli/2014/05/27/145277)

[[iT 鐵人賽 Day6]SQL Server 資料型態 char varchar nchar nvarchar](https://ithelp.ithome.com.tw/articles/10213922)
