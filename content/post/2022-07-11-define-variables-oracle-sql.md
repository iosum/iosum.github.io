---
layout: post
title: 定義變數
author: Casey
date: 2022-07-11
categories: Snippets
tags: oracle-sql
---

## 目的

Oracle SQL 定義變數跟 SQL Server 的用法十分不一樣(踩到非常多坑啊 😭)，所以這一篇主要紀錄 Oracle SQL 定義變數 的 `VARIABLE` 和 `DEFINE`。

### `DEFINE` 的 `VARIABLE` 的差別

-   `DEFINE` 的目的是**替代**變數，在 client 端執行解析，需要加入`&`在變數名稱前面，且必須要有變數名稱和預設值。不可以指定 data type，唯一的 data type 為 `char`。

    語法：

    > DEFINE variable_name = value

-   `VARIABLE` 的目的是**綁定**變數，在 server 端執行解析，需要加入`:`在變數名稱前面，可以綁定多種 data type。

    語法：

    > VARIABLE variable_name data_type

```sql
-- 先定義 VARIABLE variable_name data_type
VARIABLE po_header_ids VARCHAR2(1000);

-- 如果需要賦予預設值，必須在 variable_name 前面加入 :，也就是 :variable_name
-- := 在 ORACLE SQL 表示 ASSIGN
BEGIN
  :po_header_ids := '1,2,3';
END;
/

SELECT PHA.SEGMENT1
FROM   PO.PO_HEADERS_ALL PHA
WHERE  :po_header_ids = '0'
OR     :po_header_ids IS NULL
OR     PHA.PO_HEADER_ID IN (
         SELECT TO_NUMBER(regexp_substr(:po_header_ids,'[^,]+',1,level))
         FROM   dual
         CONNECT BY
                regexp_substr(:po_header_ids ,'[^,]+',1,level) IS NOT NULL
       );
```

## 參考資料

[Declare bind variable in the Oracle SQL Developer](https://stackoverflow.com/questions/72853678/declare-bind-variable-in-the-oracle-sql-developer)

[Oracle 變數定義的三種方式(define,variable,declare)](https://iter01.com/397633.html)
