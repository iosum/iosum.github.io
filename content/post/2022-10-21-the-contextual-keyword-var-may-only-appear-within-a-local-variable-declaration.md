---
layout: post
title: The contextual keyword 'var' may only appear within a local variable declaration.  | c#
author: Casey
date: 2022-10-19
categories: Snippets
tags: c#
---

## 錯誤訊息

> The contextual keyword 'var' may only appear within a local variable declaration.

```csharp
using System;
using System.Collections.Generic;
using System.Web;
using System.Text;
using WebMatrix.Data;

/// <summary>
/// Summary description for ClassName
/// </summary>
public class Base
{
    public void CalculateTotalPriceInCart(var PartNumber, var Description, var OrderId, bool IsBoxed)
    {
        var database = Database.Open("OSF");
        var query = "";
        var result = "";
        decimal price = 0.00M;

        if(IsBoxed)
        {
            // Select item.
            query = "SELECT Boxes, BoxPrice FROM Cart WHERE OrderId = '" + OrderId + "' AND PartNumber = '" + PartNumber + "' AND Description = '" + Description + "' AND IsBoxed = 1";
            result = database.Query(query);

            // Recalculate Price.
            foreach(var item in result)
            {
                price = result.Boxes * result.BoxPrice;
            }

            // Update item.
            query = "UPDATE Cart SET BoxPrice = '" + price + "' WHERE OrderId = '" + OrderId + "' AND PartNumber = '" + PartNumber + "' AND Description = '" + Description + "' AND IsBoxed = 1";
            database.Execute(query);
        }
    }
}

```

## 為什麼

`var` 只能在宣告並初始化後才可以在 method 的 scope 使用，不能在 global scope 使用和當作參數使用。

因為編譯器無法知道 `CalculateTotalPriceInCart` 必須要接到的參數的 data type 是什麼。

## 解決方法

將 `CalculateTotalPriceInCart` 所接收到的參數的資料型態變成 strongly data type。

```csharp
using System;
using System.Collections.Generic;
using System.Web;
using System.Text;
using WebMatrix.Data;

/// <summary>
/// Summary description for ClassName
/// </summary>
public class Base
{
		// var 不能當作參數的型態傳入，參數的資料型態必須是強型別的資料型態。
    public void CalculateTotalPriceInCart(IEnumerable<dynamic> Description, string PartNumber, string OrderId,bool IsBoxed)
    {
        var database = Database.Open("OSF");
        var query = "";
        var result = "";
        decimal price = 0.00M;

        if(IsBoxed)
        {
            // Select item.
            query = "SELECT Boxes, BoxPrice FROM Cart WHERE OrderId = '" + OrderId + "' AND PartNumber = '" + PartNumber + "' AND Description = '" + Description + "' AND IsBoxed = 1";
            result = database.Query(query);

            // Recalculate Price.
            foreach(var item in result)
            {
                price = result.Boxes * result.BoxPrice;
            }

            // Update item.
            query = "UPDATE Cart SET BoxPrice = '" + price + "' WHERE OrderId = '" + OrderId + "' AND PartNumber = '" + PartNumber + "' AND Description = '" + Description + "' AND IsBoxed = 1";
            database.Execute(query);
        }
    }
}

```

## 參考資料

[The contextual keyword 'var' may only appear within a local variable declaration issues](https://stackoverflow.com/questions/6628358/the-contextual-keyword-var-may-only-appear-within-a-local-variable-declaration)
