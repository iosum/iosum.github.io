---
layout: post
title: 保留原本 C# 的 Exception message，並加上客製化 Exception Message  | c#
author: Casey
date: 2022-10-19
categories: Snippets
tags: c#
---

假設現在程式拋出了一個 Exception，那麼我們看到的訊息應該會是 C# 預設寫好的錯誤訊息，但同時我們希望使用者需要知道這一個錯誤訊息，開發者應該可以將預設寫好的錯誤訊息變成使用者看得懂的東西。此時可以使用 Exception 的 [Data 屬性](https://learn.microsoft.com/en-us/dotnet/api/system.exception.data?redirectedfrom=MSDN&view=net-6.0#System_Exception_Data)。

Data 屬於 key/value pair，可以傳入自己想要的 key 和 value，可以使用以下 `Exception.Data[key]` 取到 Value。

## 範例

```c#
catch (Exception ex)
{
    ex.Data.Add("UserMessage", "An error occurred while trying to load the XSLT file.");
    throw;
}
```

```csharp
catch (Exception ex)
{
    if (ex.Data.Contains("UserMessage"))
    {
        MessageBox.Show(ex.Data["UserMessage"].ToString());
    }
    else
    {
        MessageBox.Show(ex.Message);
    }
}
```

## 參考資料

[How can I add a message to an exception without losing any information in C#?](https://stackoverflow.com/questions/14409988/how-can-i-add-a-message-to-an-exception-without-losing-any-information-in-c)
