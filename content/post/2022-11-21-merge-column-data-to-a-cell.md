---
layout: post
title: 將多筆資料合併為一筆顯示 - FOR XML PATH | SQL
author: Casey
date: 2022-11-21
categories: Blogging
tags: sql
---

## 前情提要

本篇使用 AdventureWorks2016 資料庫，將每一個產品的利用 FOR XML PATH 將評論人顯示多筆資料。

## 步驟

1. 先找出要使用合併的資料 (通常在 detail page)，先鎖定 `ProductID = 937`，較容易寫出完整 query

```sql
SELECT ','  + [Production].[ProductReview].ReviewerName 
FROM [Production].[ProductReview]
WHERE ProductID = 937
FOR XML PATH('')
```

可以看到評論 ProductId = 937 的人有 David 和 Jill

![Imgur](https://i.imgur.com/tG8hCz0.png)

2.  在每一個產品中，顯示各個產品的評論的人並使用 FOR XML PATH 顯示

- 將 `WHERE ProductID = 937` 拿掉
- 加入 `[Production].[ProductReview].ProductID = [Product].ProductID` 和 `FROM [Production].[Product]`

```sql
	SELECT ProductID, 
	(
		SELECT ',' + [Production].[ProductReview].ReviewerName 
		FROM [Production].[ProductReview]
		WHERE [Production].[ProductReview].ProductID = [Product].ProductID
		FOR XML PATH('')
	) AS Reviewer
	FROM [Production].[Product]
```

![Imgur](https://i.imgur.com/n7t1JXJ.png)

---
因為這一個例子的評論人並不多，所以先拿掉沒有評論的產品

```SQL
SELECT *
FROM (
	SELECT ProductID, 
	(
		SELECT ',' + [Production].[ProductReview].ReviewerName 
		FROM [Production].[ProductReview]
		WHERE [Production].[ProductReview].ProductID = [Product].ProductID
		FOR XML PATH('')
	) AS Reviewer
	FROM [Production].[Product]
)A
WHERE Reviewer IS NOT NULL
```

這樣就很清楚的看到哪一個產品有被誰寫評價


![Imgur](https://i.imgur.com/ioxRg73.png)

---

3. 使用 `STUFF()`，拿掉最左邊的逗號

- STUFF(原字串, 起始位置, 移除長度, 替換字串)

```SQL
SELECT *
FROM (
	SELECT ProductID, 
	STUFF((
		SELECT ',' + [Production].[ProductReview].ReviewerName 
		FROM [Production].[ProductReview]
		WHERE [Production].[ProductReview].ProductID = [Product].ProductID
		FOR XML PATH('')
	), 1, 1, '') AS Reviewer
	FROM [Production].[Product]
)A
WHERE Reviewer IS NOT NULL
```

![Imgur](https://i.imgur.com/IW05Tp0.png)


## 參考資料

[[SQL]將多筆資料合併為一筆顯示(FOR XML PATH)](https://dotblogs.com.tw/kevinya/2012/06/01/72553)

[[食譜好菜] SQL Server 使用「FOR XML」語法做欄位合併](https://dotblogs.com.tw/supershowwei/2016/01/26/145353)