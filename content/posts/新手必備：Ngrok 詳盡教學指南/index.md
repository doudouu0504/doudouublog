---
date: "2025-01-01T19:04:47+08:00"
draft: false
title: "新手必備：Ngrok 詳盡教學指南"
tags: ["Ngrok", "Django"]
categories: ["軟體教學"]
slug: "Ngrok-easyuse"
---

## 前言

這篇教學針對新手，將以簡單易懂的方式，教您如何在 **Mac 的 VSCode 終端機** 中，使用 Ngrok 來分享 Django 專案。

<!--more-->

Ngrok 是一個非常實用的工具，可以快速將本地服務分享至外部網絡，適用於 API 測試、Webhook 回調或遠端開發。本篇也會提供可能遇到的問題及解決方法，讓您能順利完成操作。

---

## 一、什麼是 Ngrok？

### 1.1 Ngrok 是什麼？

Ngrok 是一款強大的內網穿透工具，可將本地開發環境映射為可從外部訪問的網址，無需進行繁瑣的伺服器設定。它適用於：

- **測試 API**：無需將程式部署到線上環境，即可供測試。
- **展示本地專案**：可將開發中的網站分享給團隊或客戶。
- **Webhook 回調**：用於接收第三方服務的請求，進行開發與調試。

### 1.2 主要功能簡介

- **內網穿透**：快速將本地服務轉換為外部網址。
- **即時流量監控**：檢視請求的詳細資訊，方便開發調試。
- **高級功能（付費版）**：支援自訂域名、TLS 加密等進階功能。

## 二、安裝和設置 Ngrok

### 2.1 安裝 Ngrok

#### (a) 安裝 Homebrew（如果尚未安裝）

在 VSCode 的終端機中執行以下指令來安裝 Homebrew：

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

驗證 Homebrew 是否安裝成功：

```sh
brew --version
```

#### (b) 使用 Homebrew 安裝 Ngrok

安裝 Ngrok：

```sh
brew install ngrok
```

驗證安裝是否成功：

```sh
ngrok version
```

### 2.2 註冊與認證 Ngrok

#### (a) 註冊帳戶

- 前往 [Ngrok 官網](https://ngrok.com/) 註冊免費帳戶。

#### (b) 獲取認證碼

- 登入後，在控制台找到您的 `authtoken`。

#### (c) 在終端機中認證

- 在 VSCode 終端機執行：

```sh
ngrok authtoken <您的認證碼>
```

認證成功後，Ngrok 即可正常使用。

## 三、啟動 Ngrok（以 Django 為例）

### 3.1 啟動 Django 開發伺服器

進入 Django 專案目錄，啟動伺服器：

```sh
python manage.py runserver
```

此時，伺服器會運行在 `http://127.0.0.1:8000`。

### 3.2 啟動 Ngrok

在另一個終端機視窗執行：

```sh
ngrok http 8000
```

Ngrok 啟動後，您會看到類似以下的輸出：

```sh
Forwarding                    https://abc123.ngrok.io -> http://127.0.0.1:8000
```

### 3.3 訪問專案

- 複製 `https://abc123.ngrok.io`，在瀏覽器中開啟，即可透過外部網絡訪問 Django 專案。
- 團隊或客戶可直接透過該網址進行測試。

## 四、常見問題與解決方法

### 4.1 常見問題

- **無法分享網址**：請確保 Django 伺服器已成功啟動，並確認埠號配置正確。
- **認證失敗**：請確認輸入的 `authtoken` 無誤。

### 4.2 解決方法

- **重啟服務**：重新啟動 Django 開發伺服器與 Ngrok。
- **升級版本**：確保 Ngrok 是最新版本。
- **檢查網路**：確保網路穩定，避免 Ngrok 無法正常運行。

## 五、進階功能介紹

### 5.1 自訂域名（付費功能）

若使用付費版 Ngrok，可設定自訂域名：

```sh
ngrok http -hostname=custom.yourdomain.com 8000
```

### 5.2 即時流量監控

Ngrok 提供本地監控介面，允許開發者檢視所有進入隧道的請求詳情，幫助偵錯與分析流量模式。

- 在瀏覽器中輸入：

```sh
http://127.0.0.1:4040
```

- 可檢視請求 Headers、Payload 等細節。

## 六、Django 相關設定建議

### 6.1 允許外部連接

在 `settings.py` 設定 `ALLOWED_HOSTS`：

```py
ALLOWED_HOSTS = ['127.0.0.1', '.ngrok.io']
```

### 6.2 調整 Debug 模式

確保 `DEBUG = True` 以便在開發環境中正常使用 Ngrok，避免請求被 Django 的安全設定攔截：

```py
DEBUG = True
```

## 七、Ngrok 與其他工具比較

除了 Ngrok，還有其他內網穿透工具可供選擇，以下是三種常見工具的簡要比較：

| 工具        | 免註冊 | 自訂域名   | 連線穩定性 | 適用場景                   |
| ----------- | ------ | ---------- | ---------- | -------------------------- |
| LocalTunnel | ✅     | ❌         | 較低       | 短期測試 API、簡單展示     |
| Expose      | ❌     | ✅         | 中等       | 需要自訂域名與免費 SSL     |
| Ngrok       | ❌     | ✅（付費） | 高         | 長期穩定應用、Webhook 測試 |

**選擇建議**：

- **短期測試**：使用 LocalTunnel，快速建立臨時測試環境。
- **需要自訂域名**：選擇 Expose，免費支援 SSL，適合展示應用。
- **穩定性與進階功能**：Ngrok 提供強大監控與 CI/CD 整合，適合長期專案。

## 八、結論

Ngrok 是一款功能強大的內網穿透工具，適用於各種開發需求，特別是在 API 測試、Webhook 回調與遠端開發等場景。透過本文的教學，你應該已經掌握了如何 **安裝、認證、使用 Ngrok**，並了解了它與其他工具的比較。

如果你的需求只是 **短期測試或臨時展示**，LocalTunnel 可能是更快的選擇；如果需要 **穩定的連線與監控功能**，Ngrok 依然是最佳方案。

希望這篇教學能幫助你更順利地使用 Ngrok，提升開發效率！🚀
