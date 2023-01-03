---
layout: post
title: 使用 Selenium 和手打驗證碼登入網頁
author: Casey
date: 2023-01-03
categories: templates
tags: python
---

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
import time

chrome_options = Options()
chrome_options.add_experimental_option("detach", True)
driver = webdriver.Chrome(options=chrome_options)

# 開啟登入網頁
driver.get('login page url')

# Account
input_acct_box = driver.find_element('xpath', '//*[@id="Acct"]')
input_acct_box.send_keys('')

# password
input_pwd_box = driver.find_element('xpath', '//*[@id="Pwd"]')
input_pwd_box.send_keys('')

# 在 termianl 上面輸入 input
captcha = input('Please enter the CAPTCHA: ')
captcha_input = driver.find_element('xpath', '//*[@id="Captcha"]')
captcha_input.send_keys(captcha)

print('驗證碼已完成')

# 停2s
time.sleep(2)

# Find the submit button and click it
submit_button = driver.find_element('xpath', '//*[@id="Login_box"]/form/div/div/div/div[3]/input')
submit_button.click()

print('登入已完成')

#如果需要執行完自動關閉，就要加上下面這一行
#browser.close()
```