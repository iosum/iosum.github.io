---
layout: post
title: 執行 selenium 出包，此版本的 %1 與您執行的 Windows 版本不相容
author: Casey
date: 2022-12-15
categories: Debugging
tags: selenium
---



## 錯誤訊息

> OSError: [WinError 216] 此版本的 %1 與您執行的 Windows 版本不相容。請檢查電腦的系統資訊，然後連絡軟體發行者。
> The version of %1 is not compatible with the version of Windows you're running.


## 解決方法

通常是 x86 和 x64 位元的衝突，不過這邊指的是 Driver 和電腦的安裝版版本不一致，需下載一樣的版本。

以 Google Chrome 為例：

![https://i.imgur.com/prLfuQ0.png](https://i.imgur.com/prLfuQ0.png)

可以看到我的 Chrome 是安裝 108.0.5359.125

![https://i.imgur.com/or9fF2R.png](https://i.imgur.com/or9fF2R.png)

Driver 也需要下載相同的版本

![https://i.imgur.com/LwO9Mix.png](https://i.imgur.com/LwO9Mix.png)

將下載好的 Driver 放在跟 `python.exe` 同一個資料夾

![https://i.imgur.com/pxI5Wrc.png](https://i.imgur.com/pxI5Wrc.png)

可以執行 Sample Code 看能不能成功

```python
from  selenium  import  webdriver
from  selenium.webdriver.chrome.options  import  Options

#使用chrome的webdriver
chrome_options = Options()
chrome_options.add_experimental_option("detach", True)
driver = webdriver.Chrome(options=chrome_options)

#開啟google首頁
driver.get('https://www.google.com/')

#如果需要執行完自動關閉，就要加上下面這一行
#browser.close()

```

成功的畫面

![https://i.imgur.com/kYFb9e5.png](https://i.imgur.com/kYFb9e5.png)