---
layout: post
title: 設置 Git SSH key - Windows11 版本 | Git
author: Casey
date: 2022-08-27 23:11:00 +08:00
categories: Blogging
tags: git
---

## 設置步驟

這一篇主要紀錄設定 Github 的 SSH key - Windows 11 版本

1. 安裝 Git ：[下載網址](https://git-scm.com/)

`git --version`

如果不確定電腦有沒有安裝 Git，可以使用 `git --version` 確認，如果有，會顯示安裝的版本，如果沒有，請去官網下載，基本上只要一直按下一步即可。

2. 產生 SSH key

為 4 個步驟。

```
ssh-keygen
按下 Enter - 使用預設路徑，檔案
按下 Enter - 不使用密碼保護私鑰
按下 Enter - 確認上述動作
```

![Imgur](https://i.imgur.com/PZbLHWh.png)

使用 `ssh-keygen` 可以產生 SSH key ，接下來會被問到你想要把 SSH key 放在哪一個 file，直接按下 Enter，即是放在預設路徑，檔案。

![Imgur](https://i.imgur.com/mJl0xUQ.png)

完成檔案新增後，會要求輸入 `passphrase`，`passphrase` 就是密碼，這一個密碼可以用來保護私鑰，雖然設置密碼保護私鑰能多一層的保障，但是每一次執行 Git 時就會被要求輸入密碼，這倒是一大缺點，這裡我不使用密碼。

![Imgur](https://i.imgur.com/t0JrA9b.png)

按下 Enter 後會被要求再輸入一次密碼，如果剛剛沒有設定密碼，直接按 Enter，反之打上剛剛設定的密碼。

![Imgur](https://i.imgur.com/W5U37Wz.png)

![Imgur](https://i.imgur.com/OxpD3pB.png)

如果有看到像是亂碼的東西，表示 SSH Key 已經新增成功，如要看 SSH Key 放在哪一個檔案，可以到 C 槽的使用者底下有一個 `.ssh` 的資料夾，點開後就會有檔案 (假設使用的是預設路徑)。

- `id_rsa` 存放的是 Private Key
- `id_rsa.pub` 存放的是 Public Key

3. 將 SSH Key 加入 Github
   開啟 `id_rsa.pub` ，這邊可以使用任何的 text editor，我使用的是 `Notepad++`，打開之後會如圖所示。

![Imgur](https://i.imgur.com/uanwXS6.png)

將上述的文字全選之後複製，貼在我們自己的 [Github](https://github.com/settings/ssh/new) 上。

![Imgur](https://i.imgur.com/UnGChLq.png)

貼上之後加入 Title，點擊 Add SSH key 按鈕，Github 會要求輸入密碼，輸入後就完成 SSH key 的設定。

![Imgur](https://i.imgur.com/px5wXi3.png)

![Imgur](https://i.imgur.com/V7dpNYL.png)

完成圖

![Imgur](https://i.imgur.com/BEiJeOo.png)

---

## 測試

這邊我隨便打開一個 repo，使用 SSH clone

![Imgur](https://i.imgur.com/ZtCPXsd.png)

複製完網址後貼到 VSCODE 即可。

---

## Bugs

如果 clone 遇到 `Git error: "Host Key Verification Failed" when connecting to remote repository`

只要在 Git Bash 打上 `ssh -T git@github.com` ，並打 `yes`，就可以成功 clone repo。

![Imgur](https://i.imgur.com/yO1jNnM.png)

參考資料：

[[2022] How to Set Up your SSH key for GitHub on Windows 10](https://medium.com/devops-with-valentine/2021-how-to-set-up-your-ssh-key-for-github-on-windows-10-afe6e729a3c0)

[Git error: "Host Key Verification Failed" when connecting to remote repository](https://stackoverflow.com/questions/13363553/git-error-host-key-verification-failed-when-connecting-to-remote-repository)
