---
date: "2024-11-17T18:46:07+08:00"
draft: false
title: "環境安裝 - 踏入 Python 第一步"
tags: ["環境安裝", "Django"]
categories: ["python"]
slug: "enviroment-vscode-poetry&venv"
----------------------

## 前言

在進入 Python 領域之前，建議先安裝相關工具與套件，這樣可以邊學習邊實作，提高學習效率。本篇文章將介紹 Python 環境安裝的各種方式，適用於 **macOS 使用者**。

<!--more-->
---

## 一、安裝 Python

首先，需要從 Python 官網下載並安裝最新版本，安裝完成後可進行以下步驟確認安裝是否成功。

### 1.1 在終端機輸入以下指令：

```sh
which python3  # 檢查 Python3 位置
python3  # 進入 Python 互動模式（REPL）
exit() 或 按 Control+D  # 離開 Python 環境
```

---

## 二、了解 REPL 環境

**REPL（Read-Eval-Print-Loop）** 是 Python 內建的交互式執行環境。

在這個環境底下會**讀取**輸入的指令，然後**評估**是否可執行。

如果可以就把結果**印出來**，不行就會出現錯誤的訊息。

最後不管能不能執行，都會進入下一個指令的**迴圈**。

- **讀取（Read）**：讀取使用者輸入的指令。
- **評估（Eval）**：執行輸入的指令。
- **輸出（Print）**：印出執行結果。
- **循環（Loop）**：回到下一個指令輸入。

{{<alert>}}適合進行 **簡單測試** 或 **程式驗證**。{{</alert>}}

---

## 三、安裝 `pyenv`

pyenv 是什麼：`pyenv` 是一款管理 **多個 Python 版本** 的工具，可以輕鬆切換不同版本。

### 3.1 安裝 `pyenv`

請參考官方文件：[pyenv 官方安裝指南](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv)

### 3.2 常用指令

在終端機輸入以下內容，並分別為：

```sh
which pyenv  # 確認 pyenv 位置
pyenv #出現指令
pyenv -v  # 查看 pyenv 版本
pyenv install --list  # 列出可安裝的 Python 版本
pyenv install 3.12.4  # 安裝指定版本，可下載最新的
pyenv global 3.12.4  # 設定預設 Python 版本，此時就可以隨意打python不用加3
pyenv versions  # 列出已安裝的 Python 版本
pyenv shell 3.12.4 #若沒改成預設值，可以用叫的叫出這個版本
```

---

## 四、安裝 VS Code

安裝後可透過快捷鍵提升開發效率。

### 4.1 常用快捷鍵

```sh
Command+Shift+P  # 開啟命令面板
Control+`  # 開啟終端機
Command+D  # 選取下一個相同項目
Option+Shift+↓  # 複製整行
Command+/  # 註解/取消註解
直接再游標那行按複製 #可貼上到任一游標處
Option+游標處＋上下鍵 #可移動整行
```

---

## 五、執行第一個 Python 程式

### 5.1 使用內建終端機

```sh
cd 資料夾名稱  # 切換到目標資料夾
ls -al  # 查看資料夾內容
python3 檔案名稱.py  # 執行 Python 程式，例如：python3 hi.py
```

### 5.2 在 VS Code 執行

```sh
pwd  # 確認當前目錄
python3 檔案名稱.py  # 執行 Python 程式，例如：python3 hi.py
```

---

## 六、安裝 Python 套件

### 6.1 使用 `pip` 安裝套件

先到 [PyPI](https://pypi.org/) 的網站，例如要下載 request 套件，搜尋 request。

複製指令到 Vscode 的終端機安裝。

```sh
pip install requests  # 安裝 requests 套件
pip uninstall requests  # 卸載 requests
(但不會全部刪掉，會有混雜的套件留存，造成空間浪費)
pip list  # 查看已安裝的套件
```

---

## 七、建立虛擬環境（venv）

目的：不會影響其他專案，因為同樣套件只能安裝一個版本，所以沒加會覆蓋。

### 7.1 建立虛擬環境

以下內容-m 是指載入，venv 是內建虛擬模組，myenv 是自己取的虛擬環境名字

```sh
python -m venv myenv  # 建立名為 myenv 的虛擬環境
python -m venv myenv --prompt="hello"
#如同上述，不過這行--prompt="自己取名字"，為Vscode開啟終端機時「名稱」會變hello
```

### 7.2 啟動虛擬環境

左側欄位會出現一個 myenv 資料夾，裡面有一些資料夾，在使用虛擬環境時，不太管它。但啟動虛擬環境，裡面有一個 bin 資料夾，底下有 activate，執行輸入。

```sh
source myenv/bin/activate  # 啟動虛擬環境
```

### 7.3 在虛擬環境內安裝套件

```sh
pip install django  # 安裝 Django
pip list #若要看內容，領域展開，輸入以上
pip freeze > requirements.txt  # 產生套件清單
pip install -r requirements.txt  # 依據套件清單安裝
```

### 7.4 停用虛擬環境

```sh
deactivate  # 離開虛擬環境
```

---

## 八、使用 Poetry 進行套件管理

`Poetry` 是一款現代化的 Python 套件管理工具，提供 **安裝、版本控制、打包與發布** 等功能。

### 8.1 安裝 `Poetry`

```sh
pip install poetry  # 安裝 Poetry
```

### 8.2 初始化或安裝 Poetry 專案

#### 8.2.1 建立新專案

如果是全新的專案，可以使用 `poetry new` 來建立專案目錄，並自動生成 `pyproject.toml`：

```sh
poetry new myproject  # 建立新專案
cd myproject  # 進入專案目錄
pwd #確認輸入位置沒錯
```

#### 8.2.2 在現有專案初始化 Poetry

如果你已經有一個資料夾，並希望使用 `Poetry` 來管理它，請執行：

```sh
cd existing_project  # 進入現有專案目錄
poetry init  # 初始化 Poetry，建立 pyproject.toml
```

#### 8.2.3 安裝專案依賴

當 `pyproject.toml` 檔案已經存在時（無論是透過 `poetry new` 或 `poetry init` 建立），使用以下指令來安裝所有依賴：

```sh
poetry install  # 根據 pyproject.toml 安裝所有依賴，創一個.venv資料夾
```

### 8.3 使用 `Poetry` 管理套件

```sh
poetry shell #先切換到虛擬目錄裡面，在poetry執行
poetry add requests  # 安裝套件，例如套件名稱為requests
poetry remove requests  # 移除 requests 套件，或是可以刪掉資料夾
pip list #看內容
poetry show #可以看裝的套件及版本資訊（較詳細）
poetry show --tree  # 查看依賴樹狀結構
poetry add pre-commit --group dev #裝到不同群組裡佈置時使用
poetry env info #看poetry位置裝到哪
poetry env remove 位置 #刪除指定位置虛擬環境
poetry cofing --list #檢查內容
```

---

## 九、語意化版本控制

在 `pyproject.toml` 內使用 **語意化版本規則** 來管理依賴。

```sh
"^5.0.3"  # ^是中間數字0有跳動，會自動抓到新版本，是部分更動，升級中間的版本
"~5.0.3"  # 允許修正版本更新，但不變更次要版本，~是3有跳動，只裝這個後面的，算是小地方更動
">=5.0.3"  # 安裝 5.0.3 以上的版本，只要大於等於這個版本就安裝
"==5.0.3"  # 僅安裝 5.0.3，不升級，這個就好！
```

---

## 結論

本篇文章介紹了 **Python 環境安裝、套件管理、虛擬環境與 VS Code 使用技巧**，這些概念是學習 Python 及 Django 等框架的重要基礎。

**學習重點回顧：**

1. `pyenv` 可用於管理多版本 Python。
2. `venv` 和 `Poetry` 讓專案環境更獨立。
3. `pip` 和 `Poetry` 幫助管理 Python 套件。
4. VS Code 提供便利的開發工具與快捷鍵。

希望這篇文章能幫助你順利開始 Python 開發旅程！
