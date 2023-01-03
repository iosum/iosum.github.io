---
layout: post
title: MSSQL Update Query | SQL
author: Casey
date: 2022-09-27
categories: Snippets
tags: sql
---

不知道為什麼，每一次只要有 FROM 或是 INNER JOIN 在 UPDATE 裡面都會忘記怎麼寫，大概是寫的不夠多吧，特別筆記一下。

```sql

UPDATE A
SET A.X = B.X
FROM A
INNER JOIN B
ON A.ID = B.ID

```
