---
date: 2025-04-29T00:21:00+08:00
draft: false
title: "如何使用 ffmpeg 下載線上串流影片 (.m3u8 格式)"
tags: ["ffmpeg", "m3u8下載", "自動化", "影片備份", "開發技巧"]
categories: ["我的日誌"]
slug: "download-m3u8-video"
---

在某些網站上，例如線上課程平臺、監看直播，影片播放常使用 `.m3u8` 串流格式。這種影片無法直接「右鍵另存」，但只要掌握方法，我們可以通過 `ffmpeg` 工具將影片完整下載下來！

這篇文章就教你：**如何用 ffmpeg 把 `.m3u8` 串流影片存成 `.mp4`**。

<!--more-->

---

## 前置準備

### 1. 安裝 Homebrew（如果未安裝）

Homebrew 是 macOS 上最常用的套件管理工具。如果你還沒有，可以在 Terminal 執行：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

官方網站：[https://brew.sh/](https://brew.sh/)

---

### 2. 安裝 ffmpeg

安裝好 Homebrew 後，直接在 Terminal 輸入：

```bash
brew install ffmpeg
```

這樣就可以全系統使用 `ffmpeg` 指令了。

---

## 抓取影片的 m3u8 連結

1. 打開影片播放頁面。
2. 按下 `F12`，或右鍵 → 檢查 (Inspect)，打開 **開發者工具**。
3. 切到「Network」分頁，並在 Filter 中輸入 `m3u8`。
   （或是使用選取網頁中的元素集可檢查功能，點擊影片，自動找到該 html，直接找到檔案）
4. 播放影片，此時會看到一串 `.m3u8` 檔案連結出現。
5. 右鍵複製該連結（Copy Link Address）。

---

## 使用 ffmpeg 下載影片

在 Terminal 中輸入下面這條指令：

```bash
ffmpeg -i "你的.m3u8網址" -c copy ~/Downloads/影片檔案名稱.mp4
```

範例：

```bash
ffmpeg -i "https://cloudflarestream.com/aaab0cce7b590e5097e063aa0fc1b116/manifest/video.m3u8" -c copy ~/Downloads/5xvideo.mp4
```

- `-i`：指定輸入來源，也就是 .m3u8 網址
- `-c copy`：直接複製串流內容，不重新編碼，速度最快
- `~/Downloads/5xvideo.mp4`：設定儲存到下載資料夾，檔名為 5xvideo.mp4

---

## 注意事項

- 下載速度取決於網路與伺服器限制，2 小時的影片通常幾分鐘內可下載完成。
- 若造成連結過期，請重新整理頁面，重新抓新的 `.m3u8`。
- 僅限於個人合法備份用途，請勿外流或企圖違法使用。

---

## 常見問答 Q&A

### Q1：下載過程中出現「404 Not Found」？

通常是因為 .m3u8 連結已經過期。請重新整理頁面，重新採集新連結。

### Q2：可以指定下載某一個畫質嗎？

可以。如果 `.m3u8` 中有多個解析度清單，可先分析清單，挑選想要的解析度再下載（進階技術）。

### Q3：可以批次下載多部影片嗎？

可以！只要寫一個簡單的 `.sh` 批次指令，就能一次下載多部影片。

---

# 結論

`ffmpeg` 是一個強大又免費的工具，只要掌握此技巧，即使遇到無法直接下載的網頁影片，我們也能簡單儲存到自己的電腦裡。

快來學會，ffmpeg 讓你從此擁有全部自己的影片資料吧！
