---
layout: post
title: dynamic type 介紹  | c#
author: Casey
date: 2022-10-24
categories: Snippets
tags: c#
---

# Dynamic Type in C#

在 C# 4.0，有一個新的 Type 叫做 Dynamic Type。

Dynamic Type 不會在 compile time 做 checking，而是在 runtime 的時候編譯器才會知道該變數的 type ，並在 runtime 做 checking。

## 須注意事項

- 在大多數的時候，可以把 dynamic type 視為 object。
- 如果想要知道該變數在 runtime 的 type，可以使用 `GetType()`。

```csharp
using System;

public class Program
{

	public static void Main()
	{
		dynamic a = "this is a string";
		dynamic b = 123234;

		Console.WriteLine("Get the actual type of value1: {0}",
                                  a.GetType().ToString());

    Console.WriteLine("Get the actual type of value2: {0}",
                                  b.GetType().ToString());

	}
}
```

結果：

```
Get the actual type of value1: System.String
Get the actual type of value2: System.Int32
```

![Imgur](https://i.imgur.com/GdwesQY.png)

- 當 assign 一個 class object 的 type 使用 dynamic 的時候，compiler 並不會偵測這一個 dynamic object 有沒有正確的使用 method 或是 property。

```c#
using System;

public class Program
{

	public static void Main()
	{
		dynamic s1 = new Student();

		// runtime error
		Console.WriteLine(s1.DisplayStudentInfo());

	}

}
public class Student
{
    public void DisplayStudentInfo(int id)
    {
    }
}
```

```
Run-time exception (line 10): No overload for method 'DisplayStudentInfo' takes '0' arguments

Stack Trace:

[Microsoft.CSharp.RuntimeBinder.RuntimeBinderException: No overload for method 'DisplayStudentInfo' takes '0' arguments]
at CallSite.Target(Closure , CallSite , Object )
at System.Dynamic.UpdateDelegates.UpdateAndExecute1[T0,TRet](CallSite site, T0 arg0)
at Program.Main() :line 10
```

![Imgur](https://i.imgur.com/myCsp1I.png)

- 可以將 dynamic object 當成參數傳入 method。

```c#
	// 2數相加
    public static void Add(dynamic s1, dynamic s2)
    {
        Console.WriteLine(s1 + s2);
    }
```

- 如果 method 或是 property 不相容，compiler 會在 runtime 有錯誤訊息。
- 在 Visual Studio 中不支持 Intellisense。
- 如果沒有額外做 dynamic type 的 checking，compiler 就不會丟錯誤。

```csharp
using System;

public class Program
{

	public static void Main()
	{
		// compiler 不會有錯誤
		Add(false, true);
	}

	// 2數相加
    public static void Add(dynamic s1, dynamic s2)
    {
        Console.WriteLine(s1 + s2);
    }
}
```

但在執行的時候會有錯誤。

```
Run-time exception (line 14): Operator '+' cannot be applied to operands of type 'bool' and 'bool'

Stack Trace:

[Microsoft.CSharp.RuntimeBinder.RuntimeBinderException: Operator '+' cannot be applied to operands of type 'bool' and 'bool']
at CallSite.Target(Closure , CallSite , Object , Object )
at System.Dynamic.UpdateDelegates.UpdateAndExecute2[T0,T1,TRet](CallSite site, T0 arg0, T1 arg1)
at Program.addstr(Object s1, Object s2) :line 14
at Program.Main() :line 8
```

![Imgur](https://i.imgur.com/LH0rNbV.png)

## 參考資料

[Dynamic Type in C#](https://www.geeksforgeeks.org/dynamic-type-in-c-sharp/)

[C# - Dynamic Types](https://www.tutorialsteacher.com/csharp/csharp-dynamic-type)
