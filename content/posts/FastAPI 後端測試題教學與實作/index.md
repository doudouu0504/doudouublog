---
date: "2025-03-06T17:01:00+08:00"
draft: false
title: "FastAPI 後端測試題教學與實作"
tags: ["Python", "MySQL", "Redis", "API"]
categories: ["python"]
slug: "bkend-anspy"
series: ["FastAPI 後端測試實作"]
series_order: 1
---

# 前言

使用 FastAPI、MySQL、Redis 實作 API 並結合 Crontab 啟動，完整操作教學。
在這篇文章中，我將分享如何利用 FastAPI 搭配 MySQL 與 Redis 完成一個後端測試題的實作，並說明每個步驟，包含環境設置、程式撰寫以及啟動方式，適合初學者理解與實作。

<!--more-->

---

## 一、環境準備

### 1.1 必要工具

首先，在桌面創建 practice 資料夾，內容所需為以下：

- Python 3.13
- FastAPI
- MySQL
- Redis
- Uvicorn
- Crontab (用於自動啟動)
- python-dotenv (環境變數管理)

### 1.2 安裝步驟

```bash
sudo apt-get update
sudo apt-get install uvicorn cron pip -y
pip install -r requirements.txt
```

## 二、專案結構與內容

### 2.1 專案結構

```
practice/
├── ans.py
├── run_ans.sh
├── requirements.txt
├── ans.log （執行指令後會生出，不用自己建立）
├── .env
└── __pycache__/
```

### 2.2 ans.py 程式碼

```python
from fastapi import FastAPI, HTTPException
from fastapi.responses import JSONResponse
import mysql.connector
import redis

app = FastAPI()

mysql_conn = mysql.connector.connect(
    host="localhost", user="root", password="你的密碼", database="test_db"
)
mysql_cursor = mysql_conn.cursor(dictionary=True)

redis_client = redis.Redis(host="localhost", port=6379, decode_responses=True)

@app.get("/users/{id}")
def get_user(id: int):
    try:
        mysql_cursor.execute("SELECT username, email FROM users WHERE id = %s", (id,))
        user = mysql_cursor.fetchone()

        if not user:
            raise HTTPException(status_code=400, detail="User not found in MySQL")

        username = user["username"]
        email = user["email"]

        redis_value = redis_client.get(username)
        if not redis_value:
            raise HTTPException(status_code=400, detail="Value not found in Redis")

        return JSONResponse({"username": username, "email": email, "redis_value": redis_value})

    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))
```

### 2.3 run_ans.sh

```bash
#!/bin/bash
cd /Users/doudou0504/Desktop/practice （/Users/doudou0504/要變更為你的路徑）
nohup uvicorn ans:app --timeout-keep-alive 300 --host 0.0.0.0 --port 8888 --reload >> ans.log 2>&1 &
```

### 2.4 .env 檔案 (非必須)

```
MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=你的密碼
MYSQL_DATABASE=test_db
REDIS_HOST=localhost
REDIS_PORT=6379
```

## 三、執行操作

### 3.1 放入測試資料

詳細內容，可以先參考[這一篇文章](https://doudouu0504.github.io/doudouublog/posts/bkend-anspy-mysql-redis/)

#### MySQL (test_db > users)

```sql
INSERT INTO users (id, username, email) VALUES (1, 'user1', 'user1@example.com');
```

#### Redis

```bash
SET user1 redis_value1
```

### 3.2 啟動服務

```bash
chmod +x run_ans.sh
./run_ans.sh
```

服務將運行於：

```
http://0.0.0.0:8888
```

### 3.3 測試 API

請求：

```
GET http://127.0.0.1:8888/users/1
```

或是於網址輸入`http://127.0.0.1:8888/users/1`

回應範例：

```json
{
  "username": "user1",
  "email": "user1@example.com",
  "redis_value": "redis_value1"
}
```

### 3.4 Crontab 自動啟動設定

```bash
crontab -e
```

新增：

```
@reboot /Users/doudou0504/Desktop/practice/run_ans.sh
```

---

以上就是完整的 FastAPI 測試題實作與教學流程，希望對你有所幫助！
