---
layout: post
title: 如何壓縮 Transaction Log 檔案 | SQL
author: Casey
date: 2022-11-11
categories: Snippets
tags: sql
---


## 方法

有 2 種方法
- 使用 SSMS 
- 使用 TSQL 


### TSQL 

在資料庫按右鍵 > 屬性 > 復原模式

![Imgur](https://i.imgur.com/njsUp1j.png)

如果 DB 的復原模式使用「簡單」，直接使用 `DBCC SHRINK` 指令即可。

```sql
-- 找出 log 檔案名稱
SELECT name FROM sys.master_files WHERE type_desc = 'LOG'
-- AdventureWorks2012_log為壓縮的檔名
-- 1 為 AdventureWorks2012_log 壓縮到剩 1 MB
DBCC SHRINKFILE (AdventureWorks2012_log, 1)
```

如果 DB 的復原模式使用「完整」，可以將復原模式從完整變成「簡單」後再壓縮檔案，壓縮檔案結束後再將復原模式調回完整。

```SQL
-- 將復原模式變成「簡單」
ALTER DATABASE AdventureWorks2012
SET RECOVERY SIMPLE
GO
-- 壓縮檔案
DBCC SHRINKFILE (AdventureWorks2012_log, 1)
GO
-- 將復原模式變成「完整」
ALTER DATABASE AdventureWorks2012
SET RECOVERY FULL
```

### SSMS

1. 資料庫按右鍵 > 工作(Tasks) > 壓縮(Shrink) > 檔案(Files)

![Imgur](https://i.imgur.com/WcpMB8y.png)

2. 檔案類型選擇紀錄檔 (log)，並選擇要壓縮的 log 檔的位置，壓縮動作可以自行選擇。

![Imgur](https://i.imgur.com/2N1kHVu.png)

3. 按下確定即可壓縮 log 檔


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


## 參考資料

[How to shrink the transaction log](https://www.mssqltips.com/sqlservertutorial/3311/how-to-shrink-the-transaction-log/)

[阿湯哥@IT三兩事](https://itorz324.blogspot.com/)