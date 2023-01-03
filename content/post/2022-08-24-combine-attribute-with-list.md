---
layout: post
title: List<自定義的 class> 轉成以逗號分隔字串 | c#
author: Casey
date: 2022-08-24 16:14:00 +08:00
categories: Snippets
tags: c# LINQ
---

搭配 LINQ 和 `string.Join()`，將 List\<自定義的 class\> 轉成以逗號分隔字串。

```c#
void Main()
{
  // 新增一個 User List 叫做 result
	List<User> result = new List<User>();

  // 加入 3 個 object 到 result，分別為 Sharon，John 和 Bobby
	result.Add(new User(1, "Sharon", "User", "sharon"));
	result.Add(new User(2, "John", "User", "john"));
	result.Add(new User(3, "Bobby", "Admin", "bobby"));

  // 使用 string.Join()，將 result 的 name attribute 用 ", " 串起來
	Console.WriteLine(string.Join(", ", result.Select(x => x.name).ToList()));
}

// Define other methods and classes here

public class User
{
	public int id {get; set;}
	public string name {get; set;}
	public string type {get; set;}
	public string username {get; set;}

	public User(int id, string name, string type, string username)
	{
		this.id = id;
		this.name = name;
		this.type = type;
		this.username = username;
	}
}
```

結果：
![Imgur](https://i.imgur.com/w15Srgk.png)

---

## 參考資料：

[C# List\<string\> to string with delimiter](https://stackoverflow.com/questions/3575029/c-sharp-liststring-to-string-with-delimiter)
