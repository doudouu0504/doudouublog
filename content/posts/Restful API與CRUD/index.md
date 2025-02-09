---
date: "2024-11-23T13:08:55+08:00"
draft: false
title: "RESTful API 與 CRUD"
tags: ["CRUD", "RESTful API"]
categories: ["軟體教學"]
---

## 前言

RESTful API 是一種設計方式，讓不同的應用程式能夠透過網路互相溝通。它使用標準的 **HTTP 方法**（如 GET、POST、PUT、DELETE）來存取和管理資源，使得前端和後端可以更容易地分工合作。

<!--more-->

這篇文章將簡單介紹 RESTful API 的基本概念、設計原則，並說明它如何與 CRUD（Create、Read、Update、Delete）操作相對應，幫助新手更容易理解並開始使用 RESTful API。

---

## 一、RESTful API 介紹

RESTful API 是一種基於 **REST (Representational State Transfer)** 架構風格的 Web API 設計方式。其核心思想是透過統一的資源接口（URI）來操作資源，並使用標準的 HTTP 方法（如 **GET、POST、PUT、DELETE**）進行通信。

RESTful API 被廣泛應用於 **前後端分離架構**，使前端（如 Web 或手機應用）能與後端服務透過標準化接口進行交互。

## 二、RESTful API 的核心概念

RESTful API 的設計遵循一些核心概念，讓 API 更容易理解和使用，確保 API 結構清晰、易於維護。

1. **統一的資源路徑 (URI)**

   - 每個資源（如「用戶」或「文章」）都有固定的網址，例如：
     - `GET /users`：取得所有用戶
     - `POST /users`：新增用戶

2. **使用標準的 HTTP 方法來操作資源**

   - RESTful API 遵循 HTTP 標準，透過不同的方法來對資源進行操作：
     - `GET`：獲取資源，如 `GET /users` 來取得所有用戶。
     - `POST`：新增資源，如 `POST /users` 來新增用戶。
     - `PUT`：更新資源，如 `PUT /users/1` 來修改 ID 為 1 的用戶。
     - `DELETE`：刪除資源，如 `DELETE /users/1` 來移除 ID 為 1 的用戶。
   - 這些方法讓 API 更具一致性，使開發者能夠輕鬆理解和使用。
   - RESTful API 使用 **GET、POST、PUT、DELETE** 等 HTTP 方法來操作資源。

3. **請求與回應格式**

   - API 一般使用 **JSON** 來傳遞資料，因為它簡單易讀。

4. **無狀態性 (Statelessness)**

   - 每個請求都是獨立的，伺服器不會記住上一個請求的狀態。

5. **可擴展與靈活性**
   - API 設計應該允許未來擴充，例如 `GET /users?limit=10` 來限制回傳的用戶數量。

這些概念有助於 RESTful API 變得更具可讀性、可擴展性，並讓不同系統之間的溝通變得更加順暢。

## 三、HTTP 方法與資源操作

RESTful API 通常使用 **HTTP 方法** 來執行資源操作，對應如下：

| HTTP 方法 | 操作 | 用途                                |
| --------- | ---- | ----------------------------------- |
| GET       | 讀取 | 獲取單個或多個資源。                |
| POST      | 創建 | 在資源集合下新增一個資源。          |
| PUT       | 更新 | （整體替換） 更新整個資源。         |
| PATCH     | 更新 | （部分更新） 僅更新資源的部分字段。 |
| DELETE    | 刪除 | 移除指定資源。                      |

## 四、HTTP 狀態碼

RESTful API 通過 **HTTP 狀態碼** 來表示請求結果：

| 狀態碼 | 含義                               |
| ------ | ---------------------------------- |
| 200    | 成功 (GET、PUT、DELETE 成功)。     |
| 201    | 創建成功 (POST 成功)。             |
| 204    | 無內容 (DELETE 成功且無返回內容)。 |
| 400    | 壞請求 (請求格式錯誤)。            |
| 401    | 未授權 (需要身份驗證)。            |
| 404    | 找不到資源。                       |
| 500    | 服務器內部錯誤。                   |

## 五、CRUD 與數據操作

CRUD（Create、Read、Update、Delete）是數據操作的基本概念，對應於應用內部的數據管理。

| 操作   | SQL 對應      | ORM 對應（如 Django ORM） |
| ------ | ------------- | ------------------------- |
| Create | `INSERT INTO` | `.create()`               |
| Read   | `SELECT`      | `.all()`、`.filter()`     |
| Update | `UPDATE`      | `.update()`               |
| Delete | `DELETE`      | `.delete()`               |

## 六、RESTful API 設計與 CRUD 對應

| HTTP 方法 | RESTful API 功能 | CRUD 動作 | 範例                   |
| --------- | ---------------- | --------- | ---------------------- |
| POST      | 新增資源         | Create    | 新增一筆用戶數據       |
| GET       | 讀取資源         | Read      | 獲取所有用戶或單個用戶 |
| PUT       | 更新整個資源     | Update    | 更新用戶資料           |
| PATCH     | 部分更新資源     | Update    | 更新部分用戶資料       |
| DELETE    | 刪除資源         | Delete    | 刪除一筆用戶數據       |

## 七、CRUD 與 RESTful API 的區別

| 特性     | CRUD                 | RESTful API                  |
| -------- | -------------------- | ---------------------------- |
| 概念     | 針對數據的操作方法   | 一種 Web API 設計風格        |
| 技術     | 主要與數據庫操作相關 | 基於 HTTP 協議的資源操作     |
| 應用     | 用於內部系統邏輯處理 | 用於客戶端與伺服器之間的通信 |
| 數據存取 | 直接對接數據庫       | 透過 API 來存取資源          |

## 八、總結

- **CRUD** 是應用內部 **數據管理** 的基本操作。
- **RESTful API** 是 **對外提供接口** 的設計風格，基於 HTTP 協議。
- **兩者關聯**：CRUD 為內部邏輯，RESTful API 則透過標準 HTTP 方法對外暴露資源。

透過理解 CRUD 和 RESTful API 的概念，開發者能夠更好地設計 Web 應用程式，並提升 API 的可維護性與擴展性。

希望這篇文章能幫助你更好地掌握 RESTful API 與 CRUD 的關鍵概念！ 🚀
