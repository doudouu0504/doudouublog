---
title: "Python 資料工程師面試指南：必考問題與回答"
draft: false
date: 2025-02-11T19:28:08+08:00
tags: ["面試", "爬蟲", "API 開發"]
categories: ["python"]
slug: "python-interview-good"
---

## 前言

如果你正在準備 **Python 資料工程師** 的面試，那麼這篇文章將幫助你掌握關鍵的考題與最佳回答。我將依據實際職缺需求，涵蓋 **Python 基礎、爬蟲、API 開發、資料庫處理、效能優化** 等技術問題，確保你能順利通過面試！

<!--more-->

---

## 一、 Python 基礎與物件導向

### Q1: Python 內建的基本資料結構有哪些？它們的時間複雜度？

A: Python 內建的資料結構包含：

- list（動態陣列）：索引/插入 O(1), 搜尋 O(n)
- dict（哈希表）：插入/查找 O(1)（最壞 O(n)）
- set（哈希表）：插入/查找 O(1)
- tuple（不可變）：索引 O(1)，但不可修改
- deque（雙端佇列）：兩端插入 O(1)

```py
list_data = [1, 2, 3] # 動態陣列 O(1) 插入
set_data = {1, 2, 3} # 哈希表 O(1) 查找

dict_data = {"key": "value"} # 哈希表 O(1) 查找

```

> **考點：Python 基本資料結構的時間複雜度、應用場景**
>
> - `list` 適用於順序存取，增刪操作較慢。
> - `dict` 適用於快速查找，但哈希碰撞可能影響效能。
> - `set` 可用來去除重複元素。

### Q2: 什麼是 dict 和 set，它們的底層原理？

A:

- dict 和 set 底層都是 哈希表 (Hash Table)，但 set 只儲存鍵而沒有值。
- dict 會根據鍵的哈希值快速定位到對應的值，所以查找和插入的時間複雜度通常是 O(1)，但如果發生哈希碰撞則可能退化為 O(n)。

### Q3: 請實作一個 Python class，並說明 **init**、self 的作用。

```py
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def get_info(self):
        return f"{self.title} by {self.author}"

book = Book("Python 程式設計", "邱佳瑜")
print(book.get_info())  # "Python 程式設計 by 邱佳瑜"

```

> **init** 是建構子，在物件初始化時執行，self 代表該實例本身。

---

## 二、 爬蟲與資料搜集

### Q4: 你有使用 BeautifulSoup 或 Selenium 嗎？它們的適用場景？

A:

- BeautifulSoup 適合靜態網頁，解析 HTML 提取資料。
- Selenium 用於動態網頁（JS 生成內容），可模擬瀏覽器操作。

### Q5: 如果網站有 反爬機制（CAPTCHA, 限制 IP），你會怎麼處理？

A:

- 使用 User-Agent 模擬正常瀏覽器訪問
- 使用 Proxy 或 Tor 變換 IP
- 透過 Headless Browser（如 Selenium）模擬人類行為
- 嘗試 API（如果網站有開放）
- 若遇到 CAPTCHA，可用 2Captcha 或 OCR 技術破解

### Q6: 請實作一個爬蟲，擷取 PTT 八卦版的標題：

```py
import requests
from bs4 import BeautifulSoup

url = "https://www.ptt.cc/bbs/Gossiping/index.html"
headers = {"User-Agent": "Mozilla/5.0"}
session = requests.Session()
session.cookies.set("over18", "1")  # 針對 PTT 18+ 確認

res = session.get(url, headers=headers)
soup = BeautifulSoup(res.text, "html.parser")

titles = [t.text for t in soup.select(".title a")]
print(titles)

```

### Q7: 如何爬取 PTT 文章標題？

使用 `requests` + `BeautifulSoup` 來擷取 PTT 文章標題

```py
import requests
from bs4 import BeautifulSoup

url = "https://www.ptt.cc/bbs/Gossiping/index.html"
headers = {"User-Agent": "Mozilla/5.0"}
session = requests.Session()
session.cookies.set("over18", "1") # PTT 18+ 免驗證

res = session.get(url, headers=headers)
soup = BeautifulSoup(res.text, "html.parser")

titles = [t.text for t in soup.select(".title a")]
print(titles)
```

> **補充：如何應對反爬機制？**
>
> - 使用 **不同 User-Agent** 模擬瀏覽器訪問。
> - 加入 **隨機延遲** (`time.sleep()`)，避免被封鎖。
> - 若是動態內容，則使用 **Selenium** 爬取 JavaScript 渲染的頁面。

---

## 三、 API 開發與框架（Django, Flask, FastAPI）

### Q8: 你有用過 Flask、FastAPI 或 Django 嗎？它們的主要差異？

A:

- Django：全功能框架，適合大型專案，內建 ORM、Admin、Auth
- Flask：輕量框架，彈性大，但需手動選擇 ORM、Auth
- FastAPI：適合高效能 API，支援 async，自動生成 OpenAPI

### Q9: 設計一個簡單的 FastAPI API

```py
from fastapi import FastAPI

app = FastAPI()

@app.get("/hello")
def read_root():
return {"message": "Hello, World!"}
```

> **API 設計重點：**
>
> - 使用 `GET`, `POST`, `PUT`, `DELETE` 遵循 **RESTful API 原則**。
> - 使用 **JWT 驗證** 保護 API。
> - 使用 **SQLAlchemy ORM** 操作資料庫，提升開發效率。

---

## 四、 資料處理與資料庫

### Q10: 你熟悉 SQL 嗎？請寫一個 SQL 查詢語句，查詢某個欄位的前 10 大資料。

```sql
SELECT name, COUNT(*)
FROM orders
GROUP BY name
ORDER BY COUNT(*) DESC
LIMIT 10;

```

### Q11: SQL 查詢：找出前 10 名最常購買的商品

```sql
SELECT product_name, COUNT(\*) AS purchase_count
FROM orders
GROUP BY product_name
ORDER BY purchase_count DESC
LIMIT 10;
```

### Q12: 什麼是 ORM？優缺點？

A: ORM（Object-Relational Mapping）讓我們用 Python 類別來操作資料庫，而不用直接寫 SQL。
優點：可讀性高、可跨資料庫（MySQL, PostgreSQL）。
缺點：效能比純 SQL 差，複雜查詢時可能影響效率。

### Q13: ORM 操作資料庫（Django ORM）

```sql
from myapp.models import Order

top_products = Order.objects.values("product_name").annotate(count=Count("product_name")).order_by("-count")[:10]
```

---

## 五、 進階技能：Celery 與 LangChain

### Q14: 什麼是 Celery？它的作用是什麼？

A: Celery 是 非同步任務隊列，可讓程式在背景執行耗時任務，例如：

> 定期爬取資料
> 影像處理
> 發送通知

### Q15: Celery 非同步處理（背景任務）

```py
from celery import Celery

app = Celery("tasks", broker="redis://localhost:6379/0")

@app.task
def add(x, y):
return x + y
```

### Q16: 你有使用 Git 進行版本控制嗎？

A: 是的，我熟悉 Git Flow，可用 git rebase 整理 commit，並用 git merge 進行分支合併。

### Q17: LangChain 處理 NLP 任務是什麼

- LangChain 可與 ChatGPT 整合，開發自動化聊天機器人。
- 使用 **Memory** 來存取上下文，提高對話理解度。

---

## 六、面試技巧與行為問題

📌 **為什麼想加入這家公司？**

> 我對 **非結構化資料處理與語意分析** 很有興趣，這份工作涉及 **爬蟲、API 開發、資料庫維護**，符合我的技能組合。此外，貴公司是該領域的領導者，我希望能參與大規模數據處理專案，提升自己的技術能力。

📌 **如何學習新技術？**

- 閱讀官方文件（如 Python, Django, FastAPI）。
- 參與開源專案，提升實戰經驗。
- 透過技術部落格紀錄學習心得。

---

## 結論

準備 Python 資料工程師的面試，關鍵在於熟悉 **Python 語法、爬蟲、API 開發、資料庫處理**，並且理解 **系統設計與效能優化**。希望這篇文章能幫助你提升面試表現，順利拿到理想的工作！🚀
