---
layout: post
title: Automapper 簡介
author: Casey
date: 2023-03-20
categories: Blogging
tags: .NET
---

# AutoMapper 是什麼

AutoMapper 是一個在 .NET 平台上使用的工具，它可以幫助開發人員更快速、更方便地處理不同物件之間的 Mapping。

什麼是物件之間的 Mapping，是指把一個物件的某些屬性自動地複製到另一個物件對應的屬性。

這樣描述似乎有一點複雜，可以參考以下範例和步驟。

# 使用步驟

1. 透過 [Nuget](https://www.nuget.org/packages/automapper/) 安裝 AutoMapper 套件。

2. 建立 DTO 和 Entity 類別，[Click here](#第二步)

3. 建立 Profile 類別，設定 Attribute Mapping 的關係，[Click here](#第三步)

4. Setup AutoMapper，指定使用哪些 Profile 類別，[Click here](#第四步)

5. 在需要使用 AutoMapper 的地方，透過 Dependency Injection 或手動建立 IMapper 物件，使用 Map 方法進行類型轉換，[Click here](#第五步)

# 範例

## 第二步

建立 DTO 和 Entity 類別，假設我們有一個 `User` class 和一個 `UserInfo` class，它們分別如下所示：

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}

public class UserInfo
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

我們希望將 `User` 物件的值 mapping 到 `UserInfo` 物件上，只保留 Id 和 Name 屬性的值，這樣可以得到一個新的 UserInfo 物件。

## 第三步

建立 Profile 類別，設定 Attribute Mapping 的關係

```csharp
public class UserProfile : Profile
{
    public UserProfile()
    {
        // dest => dest.Name 為目標 class 的 attribute，在這邊指的是 UserInfo.Name
        // opt 是表示目標 class 的 attribute 的 mapping 的參數名稱
        // src 則是表示來源 class 的 attribute。在這邊指的是 User.Name
        // opt.MapFrom(src => src.Name) 的意思是，把 User.Name mapping 到 UserInfo.Name
        CreateMap<User, UserInfo>()
            .ForMember(dest => dest.Name, opt => opt.MapFrom(src => src.Name));
    }
}
```

## 第四步

Setup AutoMapper，指定使用哪些 Profile 類別

```csharp
// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    // 註冊 AutoMapper
    services.AddAutoMapper(typeof(Startup));

    // 注冊其他服務
    // ...
}
```

## 第五步

在需要使用 AutoMapper 的地方，透過 Dependency Injection 或手動建立 IMapper 物件，使用 Map 方法進行類型轉換

```csharp
public class ControllerBase
{
    private readonly IMapper _mapper;

		public ControllerBase(IMapper mapper)
		{
	     _mapper = mapper;
		}
}
```

```csharp
[ApiController]
[Route("[controller]")]
public class UserController : ControllerBase
{
    private readonly IUserService _userService;

    // base(mapper) 是在呼叫 base class ControllerBase 的 constructor 並傳入 mapper 參數，
    // 在 UserController 的實例化過程中，先初始化 base controller (ControllerBase) 的部分，
    // 確保base controller (ControllerBase)所需的資源、設定或狀態等已經被正確初始化。
    // 因為 UserController 是繼承自 ControllerBase，而 ControllerBase 的建構子需要一個 IMapper 物件，
    // 所以在 UserController 的建構子中需要先呼叫基底類別的建構子，
    // 並傳入 IMapper 物件。使用 base(mapper) 的方式可以達到這個目的。

    public UserController(IMapper mapper, IUserService userService) : base(mapper)
    {
        _userService = userService;
    }

    public IActionResult GetUser(int id)
    {
        var user = _userService.GetUser(id);
        var userDto = _mapper.Map<UserDto>(user);
        return Ok(userDto);
    }
}
```

# 參考資料

[AutoMapper 官網](https://docs.automapper.org/en/latest/Getting-started.html)
