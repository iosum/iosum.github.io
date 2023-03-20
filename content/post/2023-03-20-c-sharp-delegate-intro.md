---
layout: post
title: C# Delegate 簡介
author: Casey
date: 2023-03-20
categories: Blogging
tags: c#
---

## 定義

代表 Function 的 pointer。當一個方法被 assign 給 delegate 時，就可以通過這個 delegate 來用 function。

## 範例

-   創建 delegate

```csharp
delegate int Calculate(int x, int y);
```

-   Assign delegate

```csharp
Calculate calc = Add;
```

-   使用 delegate

```csharp
int result = calc(5, 10);
```

---

## 為什麼不直接呼叫 function 而是使用 delegate 的方式?

使用 delegate 可以幫助提高 code 的靈活性和 reusability。

### 範例 - 使用 delegate

當 User click 一個 button 時，會顯示 feedback message，這個範例就可以使用 delegate 完成。

這裡使用了 EventHandler delegate，它是一個系統提供的 delegate，可以表示具有兩個參數的方法，第一個參數是從哪邊觸發，第二個參數是 EventArgs 類型的事件參數。

然後，定義 `OnClick` function，它將在 User click button 被調用：

`EventHandler` 定義

```csharp
public delegate void EventHandler(object sender, EventArgs e);
```

```csharp
button1.Click += new EventHandler(OnClick);
```

`OnClick` function 定義

```csharp
private void OnClick(object sender, EventArgs e)
{
    Console.WriteLine("Button clicked");
}
```

現在，如果需要更改按鈕 Click，只需要創建一個新的 function，並將它 assign 給 `OnClick`。這樣一來，不需要修改原有的代碼，就可以實現按鈕 Click 的不同 implementation。

### 範例 - 不使用 delegate

可以看到如果我想要修改 `OnClick()`，那麼 `button1_Click()` 和 `OnClick()` 都必須要修改，這樣就需要修改 2 個地方，
且如果想回到之前的版本，將會無法實現。

```csharp
private void button1_Click(object sender, EventArgs e)
{
    OnClick();
}
```

```csharp
public void OnClick()
{
    Console.WriteLine("Button clicked");
}
```
