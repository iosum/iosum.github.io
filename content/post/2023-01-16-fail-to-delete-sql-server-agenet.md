---
layout: post
title: 在SSMS上刪除SQL Server Agent 失敗
author: Casey
date: 2023-01-16
categories: Snippets
tags: SSMS
---

## 錯誤訊息

> 作業 'TEST.Subplan_1' 的 卸除 失敗。 (Microsoft.SqlServer.Smo)
> DELETE 陳述式與 REFERENCE 條件約束 "FK_subplan_job_id" 衝突。衝突發生在資料庫 "msdb"，資料表 "dbo.sysmaintplan_subplans", column 'job_id'。
> 陳述式已經結束。 (Microsoft SQL Server, 錯誤: 547)

## 解決方法

1. 先找出要被刪除的 id

```sql
SELECT name, id FROM msdb.dbo.sysmaintplan_plans
```

2. 再依序執行以下 SQL

```sql
DELETE FROM msdb.dbo.sysmaintplan_log WHERE plan_id =
DELETE FROM msdb.dbo.sysmaintplan_subplans WHERE plan_id =
DELETE FROM msdb.dbo.sysmaintplan_plans WHERE id =
```

3. 再回到 SSMS 透過 UI 刪除該排程即可成功

## 參考資料

**[SQL Server - cannot drop idle job](https://dba.stackexchange.com/questions/121877/sql-server-cannot-drop-idle-job)**
