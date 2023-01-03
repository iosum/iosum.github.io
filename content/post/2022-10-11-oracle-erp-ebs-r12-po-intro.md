---
layout: post
title: PO - 採購單 | ORACLE ERP R12
author: Casey
date: 2022-10-11
categories: Blogging
tags: R12
---

# 採購訂單

[ORACLE 官方文件](https://docs.oracle.com/en/cloud/saas/procurement/22b/oedmp/poheadersall-3719.html#poheadersall-3719)

## PO_HEADERS_ALL

### 說明

採購訂單單頭 ，記錄向哪個供應商買東西。

### 主要資料

| Columns          | 中文          |
| ---------------- | ------------- |
| AGENT_ID         | 採購員        |
| SEGMENT1         | 採購單編號    |
| PO_HEADER_ID     | 採購單 ID     |
| VENDOR_ID        | 供應商 ID     |
| VENDOR_SITE_ID   | 供應商地點 ID |
| TERMS_ID         | 付款條件      |
| TYPE_LOOKUP_CODE | 採購單類型    |

### 主要相關 TABLE

| TABLE                           | Data              |
| ------------------------------- | ----------------- |
| PO_AGENTS / PO_AGENTS_V         | 採購員            |
| PO_VENDORS/ PO_VENDOR_SITES_ALL | 供應商/供應商地點 |
| AP_TERMS_TL                     | 付款條件          |

## PO_LINES_ALL

### 說明

採購訂單明細表 ，記錄向這個供應商買哪些東西，例如 item1，item2。

### FOREIGN KEY

- `PO_LINES_ALL.PO_HEADER_ID = PO_HEADERS_ALL.PO_HEADER_ID `

## PO_LINE_LOCATIONS_ALL

### 說明

- 同一採購訂單行的品項可能會送去不同的地點，此表記錄物料送貨情況：

  1.  送貨到自己公司的兩個不同的收貨地點，如分別在台北和新竹收貨。

  2.  或者是同一收貨地點，但是兩個不同的送貨時間，如在新竹收貨，一批在 7 月收貨，一批在 8 月收貨。

- 表中還會記錄到收料、退料、開發票的數量情況。

### FOREIGN KEY

- `PO_LINE_LOCATIONS_ALL.PO_LINE_ID = PO_LINES_ALL.PO_LINE_ID`

## PO_DISTRIBUTIONS_ALL

### 說明

- 分配的不同使得需要對應到不同的費用會計科目，或者費用需由不同的部門來承擔，則可在分配行中操作。

### FOREIGN KEY

- `PO_DISTRIBUTIONS_ALL.LINE_LOCATION_ID = PO_LINE_LOCATIONS_ALL.LINE_LOCATION_ID`

## PO_RELEASES_ALL

### 說明

當客戶或供應商已同意在某個特定時期內以特定價格購買或提供一定數量的某個項目時，就會形成一份**總括合約**。
