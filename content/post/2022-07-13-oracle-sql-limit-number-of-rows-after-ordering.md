---
layout: post
title: 排序後再 SELECT TOP N 筆資料
author: Casey
date: 2022-07-13
categories: Snippets
tags: oracle-sql
---

寫法一：

```sql
SELECT *
FROM (
    SELECT *
    FROM TABLE_A
    ORDER BY TABLE_A.COLUMN_A DESC
)
WHERE ROWNUM <= 5;
```

寫法二：

```sql
SELECT *
FROM TABLE_A
ORDER BY TABLE_A.COLUMN_A DESC
OFFSET 0 ROWS FETCH NEXT 5 ROWS ONLY;
```

寫法三： (Ask Tom) [速度最快](https://stackoverflow.com/questions/470542/how-do-i-limit-the-number-of-rows-returned-by-an-oracle-query-after-ordering?rq=1)

```sql
SELECT * FROM (
    SELECT a.*, ROWNUM rnum FROM (
        SELECT *
        FROM TABLE_A
        ORDER BY TABLE_A.COLUMN_A DESC
  ) a WHERE ROWNUM <= MAX_ROW
) WHERE rnum >= MIN_ROW
```

寫法四：

```sql
SELECT *
FROM (
    SELECT *
    FROM TABLE_A
    ORDER BY TABLE_A.COLUMN_A DESC
) WHERE ROWNUM BETWEEN MIN_ROW AND MAX_ROW

```
