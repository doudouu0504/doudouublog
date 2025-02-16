---
title: "Python 字串修改 (Modify Strings)"
draft: false
date: "2025-02-16T20:14:00+08:00"
categories: ["python"]
tags: ["字串操作", "upper", "lower", "replace", "split"]
slug: "python-modify-string"
series: ["字串基礎認識"]
series_order: 2
---

## 前言

在 Python 中，**字串 (String)** 是不可變的，但 Python 提供了一組 **內建方法 (Built-in Methods)** 來修改字串的內容，如 **轉換大小寫、去除空白、替換字元** 等。

本篇文章將介紹常見的字串修改方法，並包含範例程式碼。

<!--more-->

---

## 一、轉換大小寫 (Change Case)

### 1.1 轉換為大寫

`upper()` 方法可以將字串內的所有字母轉換為大寫。

**範例：將字串轉為大寫**

```python
a = "Hello, World!"
print(a.upper())  # 輸出: HELLO, WORLD!
```

---

### 1.2 轉換為小寫

`lower()` 方法可將字串內的所有字母轉換為小寫。

**範例：將字串轉為小寫**

```python
a = "Hello, World!"
print(a.lower())  # 輸出: hello, world!
```

---

## 二、去除空白 (Remove Whitespace)

在某些情況下，字串的開頭或結尾可能包含空格，這些空格可以使用 `strip()` 方法去除。

### 2.1 去除首尾空格

**範例：去除字串首尾空白**

```python
a = "  Hello, World!  "
print(a.strip())  # 輸出: "Hello, World!"
```

📌 **注意**：`strip()` 只會移除字串開頭和結尾的空白，不影響字串中間的空格。

---

## 三、替換字串 (Replace String)

`replace()` 方法可以用來將特定字元或子字串替換為新的字元或子字串。

### 3.1 替換字母或單詞

**範例：將 'H' 替換為 'J'**

```python
a = "Hello, World!"
print(a.replace("H", "J"))  # 輸出: Jello, World!
```

📌 **注意**：`replace()` 不會修改原字串，而是回傳一個新的字串。

---

## 四、拆分字串 (Split String)

`split()` 方法可以根據指定的分隔符，將字串拆分為 **一個列表 (List)**。

### 4.1 使用 `split()` 進行字串拆分

**範例：使用逗號分隔字串**

```python
a = "Hello, World!"
print(a.split(","))  # 輸出: ['Hello', ' World!']
```

📌 **注意**：`split()` 回傳一個 **列表 (List)**，其中包含分隔後的子字串。

---

## 五、總結

| 方法        | 用途             | 範例                  | 輸出                   |
| ----------- | ---------------- | --------------------- | ---------------------- |
| `upper()`   | 轉換字串為大寫   | `a.upper()`           | `HELLO, WORLD!`        |
| `lower()`   | 轉換字串為小寫   | `a.lower()`           | `hello, world!`        |
| `strip()`   | 去除字串首尾空白 | `a.strip()`           | `Hello, World!`        |
| `replace()` | 替換字元或單詞   | `a.replace("H", "J")` | `Jello, World!`        |
| `split()`   | 拆分字串為列表   | `a.split(",")`        | `['Hello', ' World!']` |

透過這些 **Python 內建字串方法**，你可以輕鬆地修改與處理字串，提升程式的靈活性與可讀性！🚀
