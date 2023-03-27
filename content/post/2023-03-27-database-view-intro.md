---
layout: post
title: View 簡介
author: Casey
date: 2023-03-27
categories: Blogging
tags: sql
---

## 什麼是 View ?

View 是 Select 完多個 Table 所組合而成的資料表，是一種 Virtual Structure，並且可以在資料表上進行 SELECT、INSERT、UPDATE、DELETE 的操作。

## 優點

SQL Server Database View 具有以下優點：

1. 提供了一個簡單的方式來查詢多個 Table
2. View 可以簡化複雜的查詢，並且讓使用者只查看他們需要的資訊，而不用顧慮底層的資料表結構
3. View 可以提高資料安全性，因為可以限制使用者只能查詢特定欄位

## 缺點

SQL Server Database View 也有一些缺點：

1. View 的效能可能會比直接查詢 Table 差，因為需要額外的資源和時間來處理 View
2. View 可能會讓資料庫設計更複雜，因為需要考慮許多 Table 之間的關係
3. View 可能會增加資料庫的存儲空間，因為 View 通常需要儲存 Table 的複本

## 為什麼要使用

1. 查詢多個 Table：如果需要查詢多個 Table 來取得所需資訊，使用 View 可以簡化這個過程，讓查詢更加簡單。
2. 保持資料庫的一致性：透過 View，可以將 Table 的結構和應用程式分離，讓資料庫的設計更具有彈性，並且保持資料庫的一致性。
3. 提高資料安全性：可以使用 View 來限制使用者只能查詢特定欄位，提高資料安全性。

## 常用的場景

通常會用到 View 的地方都是 Data Access 的時候，需要 LEFT JOIN 或是 INNER JOIN View

## 範例

以下是一個簡單的範例，該 View 可以從兩個 Table（Customers 和 Orders）中 Select 出顧客的訂單資訊：

```sql
CREATE VIEW CustomerOrders
AS
SELECT Customers.CustomerID, Customers.CustomerName, Orders.OrderID, Orders.OrderDate
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
```

## 翻譯

SSMS 翻譯叫做檢視

![Imgur](https://i.imgur.com/okutHK1.png)
