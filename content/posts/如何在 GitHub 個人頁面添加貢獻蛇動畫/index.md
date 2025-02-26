---
date: 2025-02-27T00:17:00+08:00
draft: false
title: "如何在 GitHub 個人頁面添加貢獻蛇動畫 (GitHub Snake Animation)"
tags: ["GitHub Actions", "自動化", "Snake Animation", "README", "開發技巧"]
categories: ["軟體教學"]
slug: "Gitsnake"
---

## 🐍 如何在 GitHub 個人頁面添加貢獻蛇動畫？

教你如何在 GitHub Profile 加入 GitHub Snake Animation，讓你的貢獻紀錄動起來！
想要讓你的 GitHub 貢獻紀錄變得更酷炫嗎？這篇教學將帶你一步步設定 **GitHub Snake Animation**，讓你的 GitHub Profile 更加吸睛！🚀

<!--more-->

---

## 一、 建立 GitHub 專屬倉庫

1. 進入 [GitHub](https://github.com/) 並登入帳戶。
2. **建立一個新的 Repository**，名稱與你的 GitHub **用戶名相同**。
   - **範例：** 如果你的 GitHub 用戶名是 `doudou0504`，那麼倉庫名稱也要是 `doudou0504`。
3. **確保儲存庫是公開 (Public)**，這樣動畫才能正確顯示。
4. **初始化 README.md**，這樣你的 GitHub Profile 就能顯示內容。

---

## 二、 建立 GitHub Actions 來自動生成蛇動畫

1. 在你的 Repository **建立 GitHub Actions Workflow**：
   - 進入 `你的GitHub倉庫 > Actions`
   - 點擊 `New workflow`
   - 選擇 `Set up a workflow yourself`
   - **建立 `.github/workflows/snake.yml`**，內容如下：

```yaml
title: "Generate Snake Animation"

on:
  schedule:
    - cron: "0 0 * * *" # 每天執行
  workflow_dispatch: # 允許手動執行

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write # 讓 Actions 可以推送到 output 分支
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate Snake Animation
        uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: dist/snake.svg

      - name: Push snake.svg to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
          commit_message: "Update snake animation"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

2. **提交 (Commit changes)**，GitHub Actions 會自動執行。
3. **等待 1~2 分鐘，檢查 `Actions` 頁面**，確保 workflow 成功執行。
4. **檢查 `output` 分支**，應該會有 `snake.svg` 檔案。

---

## 三、 修改 README.md 顯示蛇動畫

1. 進入 `README.md`，新增以下內容：

```markdown
![GitHub Snake Animation](https://raw.githubusercontent.com/你的GitHub用戶名/你的GitHub用戶名/output/snake.svg)
```

2. **提交變更**，並回到 GitHub Profile 查看效果！

---

## 四、 讓貢獻蛇動畫變亮！

你可以讓蛇的顏色變亮，增加 `invert_colors: true` 來反轉顏色。

**修改 `snake.yml`** 這一行：

```yaml
- name: Generate Snake Animation
  uses: Platane/snk@v3
  with:
    github_user_name: ${{ github.repository_owner }}
    outputs: dist/snake.svg
    invert_colors: true # 🔥 讓蛇顏色反轉，讓背景變暗，蛇變亮
```

這樣蛇在 **深色模式** 下會變亮，讓動畫更有層次感！

---

## 五、 進階：讓貢獻蛇動畫變成 GIF

如果你希望貢獻蛇動畫更動感，可以輸出 GIF 檔案：

**修改 `snake.yml`** 這一行：

```yaml
- name: Generate Snake Animation (GIF)
  uses: Platane/snk@v3
  with:
    github_user_name: ${{ github.repository_owner }}
    outputs: dist/snake.gif # 讓輸出變成 GIF 動畫
```

**修改 `README.md`，改用 GIF**

```markdown
![GitHub Snake Animation](https://raw.githubusercontent.com/你的GitHub用戶名/你的GitHub用戶名/output/snake.gif)
```

這樣蛇就能以 GIF 形式動起來了！🐍✨

---

## 六、 調整動畫在 GitHub Profile 的位置

你可以調整 `README.md` 讓蛇動畫顯示在適合的位置，例如：

```markdown
## 🐍 GitHub Snake Animation

<p align="center">
  <img src="https://raw.githubusercontent.com/你的GitHub用戶名/你的GitHub用戶名/output/snake.svg" alt="GitHub Snake Animation">
</p>
```

這樣蛇動畫會置中顯示，更加美觀！

---

## 結語

現在你的 GitHub Profile 已經有 **酷炫的 GitHub Snake Animation** 了！🎉

**完整步驟回顧：**

1. **建立 GitHub Actions 自動生成蛇動畫**
2. **讓動畫顯示在 `README.md`**
3. **調整顏色 (`invert_colors: true`)** 讓蛇更亮
4. **輸出 GIF，讓蛇動畫更流暢**
5. **調整 `README.md` 讓動畫顯示在最佳位置**

現在，快去讓你的 GitHub 貢獻紀錄「動起來」吧！🚀🐍✨
