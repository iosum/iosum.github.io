---
layout: post
title: 值違反資料行的完整性條件約束
author: Casey
date: 2022-07-19
categories: Debugging
tags: ssis
---

錯誤訊息：

> DataFlow:錯誤: 寫入 Table_A.輸入[OLE DB 目的地輸入] 上的 寫入 Table_A 輸入[OLE DB 目的地輸入].資料行[Column_A] 發生錯誤。傳回的資料行狀態是: "值違反資料行的完整性條件約束。"。

解決方法：

`Table_A`.`Column_A` 不接受 NULL，但是傳入的資料是 NULL
