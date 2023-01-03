---
layout: post
title: 縮小 SSIS DB 檔案大小 | SSIS
author: Casey
date: 2022-11-07
categories: Blogging
tags: ssis
---

# 縮小 SSIS DB 檔案大小

1. 將週期天數從預設的 365 天改到 30 天或其他更小的數字。
![Imgur](https://i.imgur.com/pY2Rf6P.png)

2.  將 delete_batch_size 設定為 1000，預設為 10。

```sql
	Alter procedure SSISDB.[internal].[cleanup_server_retention_window] SET @delete_batch_size  =  1000
```


4. 把以下 4 張 Table 做 Page 壓縮

```sql
USE [SSISDB]
ALTER TABLE  [internal].[event_messages]  REBUILD  PARTITION  =  ALL  WITH (DATA_COMPRESSION  =  PAGE)

ALTER TABLE  [internal].[operation_messages]  REBUILD  PARTITION  =  ALL  WITH (DATA_COMPRESSION  =  PAGE)

ALTER TABLE  [internal].[execution_component_phases]  REBUILD  PARTITION  =  ALL  WITH (DATA_COMPRESSION  =  PAGE)

ALTER TABLE  [internal].[execution_data_statistics]  REBUILD  PARTITION  =  ALL  WITH (DATA_COMPRESSION  =  PAGE)
```

4. Shrink the db

```
USE [SSISDB]

GO

DBCC SHRINKDATABASE(N'SSISDB'  )

GO
```

## 參考資料
[How to Reduce SSISDB Size](https://sqlvikas.blogspot.com/2014/08/how-to-reduce-ssisdb-size-issue-ssisdb.html)