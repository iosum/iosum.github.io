---
layout: post
title: The DELETE statement conflicted with the REFERENCE constraint "FK_subplan_job_id" | SQL
author: Casey
date: 2022-11-10
categories: Snippets
tags: sql
---


# The DELETE statement conflicted with the REFERENCE constraint "FK_subplan_job_id"

## 錯誤訊息

![Imgur](https://i.imgur.com/5WWuXt9.png)

> "子計劃 缷除失敗"  
delete 陳述式與reference 條件的約束'FK_subplan_job_id'衝突。衝突發生在資料庫  
"msdb",資料表 "dbo.sysmaintplan_subplans",colum "job_id"。

英文版：
> TITLE: Microsoft SQL Server Management Studio ------------------------------ Drop failed for Job 'manual_db_backups.Subplan_1'. (Microsoft.SqlServer.Smo) For help, click: http://go.microsoft.com/fwlink?ProdName=Microsoft+SQL+Server&ProdVer=9.00.3042.00&EvtSrc=Microsoft.SqlServer.Management.Smo.ExceptionTemplates.FailedOperationExceptionText&EvtID=Drop+Job&LinkId=20476 ------------------------------ ADDITIONAL INFORMATION: An exception occurred while executing a Transact-SQL statement or batch. (Microsoft.SqlServer.ConnectionInfo) ------------------------------ The DELETE statement conflicted with the REFERENCE constraint "FK_subplan_job_id". The conflict occurred in database "msdb", table "dbo.sysmaintplan_subplans", column 'job_id'. The statement has been terminated. (Microsoft SQL Server, Error: 547) For help, click: http://go.microsoft.com/fwlink?ProdName=Microsoft+SQL+Server&ProdVer=09.00.3042&EvtSrc=MSSQLServer&EvtID=547&LinkId=20476



## 解決辦法

Step 1：先查詢子計畫和子計畫的 log 

```sql

USE [MSDB]
GO

-- 查詢子計畫
select * from sysmaintplan_subplans

-- 查詢子計畫log
select * from sysmaintplan_log
```

Step 2：刪除子計畫和子計畫的 log 

```sql
USE [MSDB]
go

-- 刪除維護計畫子計畫的 log
DELETE FROM sysmaintplan_log
WHERE subplan_id in 
  ( SELECT Subplan_ID from sysmaintplan_subplans
    -- change Subplan name where neccessary 
  WHERE subplan_name = 'sub plan name' ) 

-- 刪除維護計畫子計畫
DELETE FROM sysmaintplan_subplans
WHERE subplan_name = 'sub plan name'

```

Step 3：到 SQL Agent Server 刪除該計畫即可

## 發生原因

因為先刪除主計畫之後，再刪除子計畫時，就會找不到主計畫在哪裡，因此無法刪除。


## 參考資料

[The DELETE statement conflicted with the REFERENCE constraint "FK_subplan_job_id"](https://dbamohsin.wordpress.com/2011/12/13/the-delete-statement-conflicted-with-the-reference-constraint-fk_subplan_job_id/)

[MS SQL SERVER 刪除 工作排程(JOBS)時出現錯誤](https://twchuck.blogspot.com/2010/10/ms-sql-server-jobs.html)


---

# 備份資料庫

## 方法
- SSMS
- TSQL


### SSMS

1. 資料庫按右鍵 > 工作 > 備份

![Imgur](https://i.imgur.com/xYl9Jbv.png)

![](https://learn.microsoft.com/zh-tw/sql/relational-databases/backup-restore/media/quickstart-backup-restore-database/backup-db-ssms.png?view=sql-server-ver16)


2. 按加入，選擇要把備份檔放哪裡，之後按確定即可備份。

![Imgur](https://i.imgur.com/aC3aNGU.png) 

### TSQL


```sql
USE [master];
GO
-- 要備份的資料庫名稱
BACKUP DATABASE [SQLTestDB]
TO DISK = N'Z:\SQLServerBackups\AdvWorksData.bak' 
WITH NOFORMAT, NOINIT,
NAME = N'SQLTestDB-Full Database Backup', SKIP, NOREWIND, NOUNLOAD, STATS = 10;
GO
```