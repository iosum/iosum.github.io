---
layout: post
title: Clustered Index & Non-Clustered Index | sql
author: Casey
date: 2022-09-29
categories: Blogging
tags: sql
---

## INDEX

主要以下的特點：

- Index 加快從 Table 或 View 中拿到資料的速度
- Index 的值可以為一個或是多個值，這一些值會從 Table 或是 View 來的
- Index 會存在一個資料結構叫做 B-tree 中

Index 可以分成 2 種：

- CLUSTERED INDEX (叢集索引)
- NON-CLUSTERED INDEX (非叢集索引)

## CLUSTERED INDEX (叢集索引)

- Clustered Index 可以將 View 或是 Table 中的資料依照 Index 的 Value 排序後儲存
- 因為資料本身只能以一種順序排序，所以每個 Table 只能有一個 Clustered Index
- 只有當 Table 包含 Clustered Index 時，Table 中的資料才會以排序順序儲存
- Table 有 Clustered Index 時，Table 又稱為 Clustered Table (叢集資料表)
- 如果 Table 沒有任何 Clustered Index，它的資料就儲存在未排序的資料結構中，這個資料結構稱為 Heap (堆積)。

## Non-clustered Index (非叢集索引)

- Non-clustered Index 包含 Non-clustered Index Value (非叢集索引鍵值)， Non-clustered Index Value 可以是一個或是多個，為 Table 中的欄位。而每個 Non-clustered Index Value 都有一個 Pointer，指向包含 Non-clustered Index Value 的資料，也就是 Table 裡的欄位資料。
- Non-clustered Index Value 的 Pointer 稱為 Row Locator (資料列定位器)。Row Locator 的資料結構須要看資料儲存是在 Heap 或 Clustered Table 而定。若是 Heap，Row Locator 是指向 Pointer。 若是 Clustered Table，Row Locator 就是 Clustered Index。

## 共通點

- 每當修改 Table 的資料時，就會自動維護資料表或檢視的索引。
- Clustered Index 與 Non-clustered Index 都可以是 Unique 或是不是 Unique，Unique 表示資料值不能重複，不是 Unique 表示資料值可以重複。

## Query Optimizer 如何使用 Index

- 建立好的 Index 可以降低磁碟 I/O 作業並耗用較少的系統資源，因此可改善查詢效能。
- 當執行 SELECT、UPDATE、DELETE 或 MERGE 時， Query Optimizer 會評估每個擷取資料的可用方法。
- 擷取資料的可用方法可以分成 2 種
  - Table Scan
  - 掃描一個或是多個 Index

### Table Scan (資料表掃描)

- 當執行 Table Scan 時，Query Optimizer 可以讀取 Table 中的所有資料，並擷取符合查詢條件的資料列。
- Table Scan 將產生許多磁碟 I/O 作業，而且可能需要大量資源。

### 使用 Index 掃描

- 當 Query Optimizer 使用 Index 掃描時，它會搜尋 Index Value 、尋找查詢所需的資料之儲存位置，並從該位置擷取符合的資料。
- 一般而言，搜尋 Index 會比搜尋 Table 更快。

## 參考資料

[Clustered and Non-clustered indexes described](https://learn.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-Non-clustered-indexes-described?view=sql-server-ver16)
