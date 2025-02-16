---
title: "Python 格式化字串 (String Formatting)"
draft: false
date: "2025-02-16T21:46:00+08:00"
categories: ["python"]
tags: ["字串操作", "格式化"]
slug: "python-fstring"
series: ["字串基礎認識"]
series_order: 3
---

## 前言

在 Python 中，格式化字串是一種常見的操作，尤其當我們需要將 **變數、數字、運算結果** 與字串結合時，Python 提供了多種格式化字串的方法，例如 **F-String** (Python 3.6+)、`format()` 方法等。

本篇文章將介紹 **如何在 Python 中格式化字串**，並說明不同的應用方式與範例。

<!--more-->

---

## 一、無法直接組合字串與數字

在 Python 中，不能直接將字串與數字相加，否則會產生錯誤。

**錯誤範例：嘗試直接組合字串與數字**

```python
age = 36
txt = "My name is John, I am " + age  # 會發生錯誤
print(txt)
```

📌 **原因**：Python 無法直接將 `int` (數字) 與 `str` (字串) 進行串接。

解決方法：使用 **F-String** 或 `format()` 方法。

---

## 二、使用 F-String (Python 3.6+)

### 2.1 F-String 是什麼？

F-String 是 **Python 3.6 之後** 引入的字串格式化方式，是目前最推薦的方法。

**範例：建立一個 F-String**

```python
age = 36
txt = f"My name is John, I am {age}"
print(txt)  # 輸出: My name is John, I am 36
```

📌 **語法**：在字串前加上 `f`，並使用 `{}` 來放置變數。

---

## 三、佔位符與修飾符

### 3.1 變數佔位符

可以在 F-String 內使用佔位符，讓變數值動態插入字串中。

**範例：新增佔位符**

```python
price = 59
txt = f"The price is {price} dollars"
print(txt)  # 輸出: The price is 59 dollars
```

---

### 3.2 格式化數字 (修飾符)

F-String 允許在佔位符內添加修飾符來調整輸出格式，例如控制 **小數點位數**。

**範例：顯示價格到 2 位小數**

```python
price = 59
txt = f"The price is {price:.2f} dollars"
print(txt)  # 輸出: The price is 59.00 dollars
```

📌 **解釋**：`:.2f` 代表 **格式化為小數點後 2 位的浮點數**。

---

### 3.3 佔位符內進行運算

F-String 也允許在 `{}` 內執行 **數學運算**，並將結果格式化輸出。

**範例：計算價格總額**

```python
txt = f"The price is {20 * 59} dollars"
print(txt)  # 輸出: The price is 1180 dollars
```

📌 **解釋**：`{20 * 59}` 直接計算 20 乘 59，並將結果插入字串中。

---

## 四、使用 `format()` 方法

### 4.1 `format()` 的基本用法

在 Python 3.0+ 版本中，`format()` 方法是一種傳統但仍然有效的字串格式化方式。

**範例：使用 `format()` 方法插入變數**

```python
age = 36
txt = "My name is John, I am {} years old.".format(age)
print(txt)  # 輸出: My name is John, I am 36 years old.
```

📌 **語法**：使用 `{}` 作為佔位符，`format()` 會自動填充變數內容。

---

### 4.2 多個變數的 `format()`

你可以在 `format()` 中傳遞多個變數，並對應到 `{}` 內的索引位置。

**範例：多個變數格式化**

```python
name = "John"
age = 36
txt = "My name is {}, and I am {} years old.".format(name, age)
print(txt)  # 輸出: My name is John, and I am 36 years old.
```

📌 **解釋**：

- `{}` 內的值會按順序填充 `format()` 中的參數。

---

### 4.3 使用索引或關鍵字參數

你可以在 `{}` 內指定索引或關鍵字來確保變數對應正確。

**範例：索引與關鍵字參數**

```python
name = "John"
age = 36
txt1 = "My name is {0}, and I am {1} years old.".format(name, age)
txt2 = "My name is {name}, and I am {age} years old.".format(name="John", age=36)
print(txt1)  # 輸出: My name is John, and I am 36 years old.
print(txt2)  # 輸出: My name is John, and I am 36 years old.
```

📌 **解釋**：

- `{0}, {1}` 使用數字索引對應 `format()` 內的變數。
- `{name}, {age}` 使用關鍵字參數提高可讀性。

---

## 五、總結

| 方法       | 說明             | 範例                 | 輸出           |
| ---------- | ---------------- | -------------------- | -------------- |
| F-String   | 動態插入變數     | `f"My age is {age}"` | `My age is 36` |
| 格式化數字 | 調整小數點位數   | `f"{price:.2f}"`     | `59.00`        |
| 數學運算   | 佔位符內執行計算 | `f"{20 * 59}"`       | `1180`         |

使用 **F-String**，可以讓字串格式化更簡潔、更直觀，提高程式的可讀性與可維護性！🚀
