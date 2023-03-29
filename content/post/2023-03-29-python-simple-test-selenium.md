---
layout: post
title: 簡單 UI Testing Script
date: 2023-03-29
categories: Snippets
tags: python
---

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
import time

#使用chrome的webdriver
chrome_options = Options()
chrome_options.add_experimental_option("detach", True)

driver = webdriver.Chrome(options=chrome_options)

# 開啟全螢幕
driver.maximize_window()

#開啟google首頁
driver.get('https://personal-vknq.outsystemscloud.com/Test/WebScreen3.aspx')


# Pagination
pagination = driver.find_element('xpath', '//*[@id="wt70_OutSystemsUIWeb_wt18_block_wtContent_wtMainContent_RichWidgets_wt31_block_wtPageNavigator_ctl02_wtLink8"]')

pagination.click()

time.sleep(5)

print('2nd page 已完成')


# Search Keyword
input_search = driver.find_element('xpath', '//*[@id="wt70_OutSystemsUIWeb_wt18_block_wtContent_wtMainContent_OutSystemsUIWeb_wt13_block_wtInput_wtSearchInput"]')
input_search.send_keys('some')

time.sleep(5)

print('Search已完成')

# Table Sort
columns = [1, 3, 4]

for col_num in columns:
    col = driver.find_element('xpath', '//*[@id="wt70_OutSystemsUIWeb_wt18_block_wtContent_wtMainContent_wtTable"]/thead/tr/th[{}]'.format(col_num))
    col.click()
    time.sleep(5)
    print('col{}正向已完成'.format(col_num))


# Table Sort
columns = [1, 3, 4]

for col_num in columns:
    col = driver.find_element('xpath', '//*[@id="wt70_OutSystemsUIWeb_wt18_block_wtContent_wtMainContent_wtTable"]/thead/tr/th[{}]'.format(col_num))
    col.click()
    time.sleep(5)
    print('col{}反向已完成'.format(col_num))

```
