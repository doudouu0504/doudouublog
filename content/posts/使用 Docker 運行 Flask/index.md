---
date: "2025-02-05T22:44:15+08:00"
draft: false
title: "在 macOS M1 上使用 Docker 運行 Flask 應用程式"
tags: ["Docker", "Flask", "macOSM1"]
categories: ["python", "軟體教學"]
slug: "macOS-HowtouseDocker-Flask"
---

## 前言

在 **macOS M1（Apple Silicon）** 上運行 Docker 可能會遇到與傳統 x86 架構不同的挑戰，例如需要特定的架構支援。本篇文章將介紹如何使用 **Docker** 部署 Flask 應用程式，並逐步解析 `Dockerfile` 的內容，確保其可在 **macOS M1** 上順利運行。

<!--more-->

---

## **一、建立 Dockerfile**

我們將使用 Docker 來封裝一個簡單的 Flask 應用程式，並確保它能夠在 **macOS M1（ARM64 架構）** 上正常運行。

### 1.1 Dockerfile 內容

```dockerfile
# 適用於 macOS M1
FROM --platform=linux/arm64 python:3.9

# 設定工作目錄
WORKDIR /app

# 複製所有檔案到工作目錄
COPY . .

# 安裝 Flask
RUN pip install --no-cache-dir flask

# 開啟 Flask 服務
CMD ["python", "app.py"]
```

---

## **二、Dockerfile 解析**

### 2.1 指定基礎映像與架構

```dockerfile
FROM --platform=linux/arm64 python:3.9
```

這一行指定了 **Python 3.9** 作為基礎映像，並明確指定 **arm64** 平台，確保在 **macOS M1（Apple Silicon）** 上運行時，不會下載與 ARM 架構不相容的 x86 版本。

### 2.2 設定工作目錄

```dockerfile
WORKDIR /app
```

這行指令設定容器內的工作目錄為 `/app`，確保所有操作（如 `COPY` 和 `RUN`）都在該目錄內執行，提高可維護性。

### 2.3 複製專案文件

```dockerfile
COPY . .
```

- 第一個 `.`：代表本機端的當前目錄。
- 第二個 `.`：代表容器內的 `/app` 目錄。

這樣可以確保 `app.py` 和相關文件成功複製到容器內。

### 2.4 安裝 Flask

```dockerfile
RUN pip install --no-cache-dir flask
```

這行指令負責安裝 Flask，並確保不會在 Docker 鏡像中留下安裝快取，減少最終映像的大小。

### 2.5 設定容器啟動命令

```dockerfile
CMD ["python", "app.py"]
```

這行設定了容器啟動後執行的預設命令，即 **運行 `app.py` 啟動 Flask 伺服器**。

> **注意**：`CMD` 只能在 `Dockerfile` 中出現一次，否則後面的 `CMD` 會覆蓋前一個。

---

## **三、建置與運行容器**

### 3.1 建立 Docker 映像

執行以下指令來建立 Docker 映像：

```bash
docker build -t my-flask-app .
```

- `-t my-flask-app`：指定映像名稱為 `my-flask-app`。
- `.`：代表 `Dockerfile` 所在的目錄（當前目錄）。

### 3.2 運行 Docker 容器

執行以下指令來啟動 Flask 應用程式：

```bash
docker run -p 5000:5000 my-flask-app
```

- `-p 5000:5000`：將容器內的 **5000 埠** 映射到本機端的 **5000 埠**，這樣可以透過 `http://localhost:5000` 訪問 Flask 服務。
- `my-flask-app`：指定要運行的映像名稱。

### 3.3 確認 Flask 服務運行

如果一切正常，終端機應該會顯示 Flask 伺服器正在運行，並且可以開啟瀏覽器訪問：

```bash
http://localhost:5000
```

> **提示**：如果發生錯誤，請確保 `app.py` 存在，且 Flask 已安裝成功。

---

## **四、結論**

透過本篇文章，我們學習了如何在 **macOS M1** 上使用 Docker 部署 Flask 應用程式，並解析了 `Dockerfile` 的每個步驟。

### **回顧學習重點**

1. `FROM --platform=linux/arm64 python:3.9` 確保與 macOS M1 相容。
2. `WORKDIR /app` 設定工作目錄，方便管理文件。
3. `COPY . .` 將專案文件複製到容器內。
4. `RUN pip install --no-cache-dir flask` 安裝 Flask。
5. `CMD ["python", "app.py"]` 啟動 Flask 應用程式。
6. `docker build -t my-flask-app .` 建立映像。
7. `docker run -p 5000:5000 my-flask-app` 啟動 Flask 服務。

這些步驟不僅適用於 Flask，也可以用來封裝其他 Python 應用程式，讓你在 **macOS M1** 上輕鬆部署自己的應用！🚀
