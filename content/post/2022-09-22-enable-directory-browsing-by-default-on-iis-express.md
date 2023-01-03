---
layout: post
title: 未設定所要求 URL 的預設文件，且未在伺服器上啟用瀏覽目錄 | c#
author: Casey
date: 2022-09-22 23:00:00 +08:00
categories: Debugging
tags: c#
---

![Imgur](https://i.imgur.com/7XdrHH0.png)

問題：

未設定所要求 URL 的預設文件，且未在伺服器上啟用瀏覽目錄。

解決方法：

其實下面有提示解決方法，「確認網站或應用程序配置文件中的 configuration/system.webServer/directoryBrowse@enabled 屬性已設置為 true。」

實際的運作：

1.  在專案中打開 `web.config` 檔案
2.  將`<system.webServer>`加入 `web.config` 並將以下 2 個 tag 寫入`<system.webServer>`裡面

`<directoryBrowse enabled="true" />`

`<modules runAllManagedModulesForAllRequests="true" />`

更正後的 `web.config` 大概會長這樣：

```
<configuration>
  <system.webServer>
    <directoryBrowse enabled="true" />
    <modules runAllManagedModulesForAllRequests="true" />
  </system.webServer>
</configuration>
```

---

參考資料：

[How to enable Directory browsing by default on IIS Express](https://stackoverflow.com/questions/8543761/how-to-enable-directory-browsing-by-default-on-iis-express)
