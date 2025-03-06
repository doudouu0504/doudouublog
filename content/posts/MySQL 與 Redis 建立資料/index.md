---
date: "2025-03-06T17:00:00+08:00"
draft: false
title: "MySQL 與 Redis 建立資料操作指南"
tags: ["MySQL", "Redis", "資料庫教學"]
categories: ["python"]
slug: "bkend-anspy-mysql-redis"
series: ["FastAPI 後端測試實作"]
series_order: 2
---

## 前言

在後端開發過程中，經常需要使用 MySQL 和 Redis 來儲存與操作資料。  
這篇文章將一步步示範如何在本機建立 MySQL 資料庫與 Redis 資料，並進行基本操作。

<!--more-->

---

## 一、MySQL 資料建立流程

### 1.1 進入 MySQL

```bash
mysql -u root -p
```

### 1.2 建立資料庫

```sql
SHOW DATABASES;
CREATE DATABASE test_db;
USE test_db;
```

### 1.3 建立 users 表

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  username VARCHAR(50),
  email VARCHAR(100)
);
```

### 1.4 插入範例資料

```sql
INSERT INTO users (id, username, email) VALUES
(1, 'user1', 'user1@example.com'),
(2, 'user2', 'user2@example.com');
```

### 1.5 確認資料是否成功

```sql
SELECT * FROM users;
```

---

## 二、Redis 資料建立流程

### 2.1 進入 Redis CLI

```bash
redis-cli
```

### 2.2 插入需要的資料

```bash
SET user1 redis_value1
SET user2 redis_value2
```

### 2.3 確認資料是否成功

```bash
GET user1
GET user2
```

#### 預期結果：

```
"redis_value1"
"redis_value2"
```

---

## 結論

透過以上步驟，我們完成了：

- MySQL 的資料庫與資料表建立。
- 插入並查詢 MySQL 資料。
- Redis 的基本資料設定與查詢。

這些都是後端基礎的資料操作流程，能協助你快速理解並上手實務操作。🚀
