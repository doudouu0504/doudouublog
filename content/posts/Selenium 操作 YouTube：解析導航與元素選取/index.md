---
date: "2025-02-01T21:07:38+08:00"
draft: false
title: "Selenium 操作 YouTube：解析導航與元素選取"
tags: ["Selenium", "爬蟲"]
categories: ["python"]
series: ["Selemium爬取Youtube標題"]
series_order: 3
slug: "Selenium-comment-element"
---

## 前言

Selenium 中的導航與元素選取，包括 driver.back()、driver.forward()、WebDriverWait 及 XPath 。
在這篇文章中，我們將使用 `Selenium` 來搜尋 YouTube 上的比特幣相關影片，並詳細解析 **網頁導航** 與 **元素選取** 的關鍵函式。

<!--more-->

---

包括：

- `driver.back()` 與 `driver.forward()` 用於瀏覽器導航
- `time.sleep(5)` 控制頁面載入時間
- XPath 語法來選取特定元素，如 `first_video = driver.find_element(By.XPATH, '(//a[@id="video-title"])[1]')`
- `WebDriverWait(driver, 10).until(EC.presence_of_element_located(...))` 來確保元素已經載入

---

## 一、完整程式碼

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.keys import Keys
import selenium
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

# 設定 ChromeDriver 路徑
PATH = "/Users/doudouu0504/Desktop/chromedriver-mac-arm64/chromedriver"

driver = webdriver.Chrome(service=Service(PATH))
driver.get("https://www.youtube.com/")

# 搜尋關鍵字 "比特幣"
search = driver.find_element(By.NAME, "search_query")
search.clear()
search.send_keys("比特幣")
search.send_keys(Keys.RETURN)

# 等待搜尋結果載入
WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.XPATH, '//a[@id="video-title"]'))
)

# 取得所有搜尋結果的標題
titles = driver.find_elements(By.XPATH, '//a[@id="video-title"]')
for title in titles:
    print(title.text)

# 選取第一個搜尋結果
first_video = driver.find_element(By.XPATH, '(//a[@id="video-title"])[1]')
print("即將點擊影片:", first_video.text)
first_video.click()

# 等待影片載入
time.sleep(5)

# 返回上一頁
driver.back()
time.sleep(2)  # 等待返回頁面載入

# 前進至影片頁面
driver.forward()
time.sleep(2)  # 等待前進頁面載入

input("按 Enter 鍵結束程式並關閉瀏覽器...")
driver.quit()
```

---

## 二、程式碼解析

### 2.1 WebDriverWait(driver, 10).until(...)

這段程式碼確保搜尋結果已經載入，避免 `find_element` 找不到元素導致錯誤：

```python
WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.XPATH, '//a[@id="video-title"]'))
)
```

- `WebDriverWait(driver, 10)`: 最多等待 **10 秒**。
- `EC.presence_of_element_located((By.XPATH, '//a[@id="video-title"]'))`: **確認該元素已經出現在 DOM 中，但不一定可見**。

### 2.2 driver.find_element()

這行程式碼選取 **第一個搜尋結果** 並印出其標題：

當我們打開 YouTube 搜尋結果頁面，按下 `F12` 進入開發者工具，使用 `Elements` 檢視網頁的 HTML 結構時，可以發現影片標題的連結 `<a>` 元素具有 `id="video-title"`，這表示我們可以透過 XPath `//a[@id="video-title"]` 來選取所有影片標題。

```python
first_video = driver.find_element(By.XPATH, '(//a[@id="video-title"])[1]')
print("即將點擊影片:", first_video.text)
```

- `(//a[@id="video-title"])[1]`：選取 **第一個影片標題連結**。
- `print(first_video.text)`：顯示影片標題，讓使用者確認即將點擊的內容。

這樣的 XPath 表達式能幫助我們鎖定 YouTube 影片搜尋結果中的第一個影片，確保自動化腳本能夠點擊正確的影片。

### 2.3 driver.back() 與 driver.forward()

這兩行程式碼負責 **模擬瀏覽器的返回與前進操作**：

```python
driver.back()
time.sleep(2)  # 等待返回頁面載入
driver.forward()
time.sleep(2)  # 等待前進頁面載入
```

- `driver.back()`：返回上一頁（搜尋結果頁）。
- `time.sleep(2)`：等待頁面載入完成。
- `driver.forward()`：前進到影片播放頁面。

> **提示**：`time.sleep()` 是強制等待，較佳做法是使用 `WebDriverWait` 確保頁面載入。

---

## 三、結論

這篇文章示範了如何使用 Selenium **自動搜尋 YouTube 影片**，並解析了幾個重要的功能：

1. `WebDriverWait(driver, 10).until(...)` 確保搜尋結果已載入。
2. `first_video = driver.find_element(By.XPATH, '(//a[@id="video-title"])[1]')` 選取第一個搜尋結果。
3. `driver.back()` 與 `driver.forward()` 用於網頁導航。
4. `time.sleep(5)` 等待頁面載入，但可用 `WebDriverWait` 優化。

這些技術對於爬蟲開發與自動化測試都十分重要，建議讀者可以進一步嘗試不同的關鍵字搜尋，或結合其他 Selenium 方法來提升爬取效率。
