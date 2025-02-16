---
title: "Python 字串方法 (String Methods)"
draft: false
date: "2025-02-16T22:23:00+08:00"
categories: ["python"]
tags: ["字串操作", "內建方法"]
slug: "python-import-method"
series: ["字串基礎認識"]
series_order: 4
---

## 前言

在 Python 中，字串 (String) 是最常使用的資料型態之一。為了方便處理字串，Python 提供了一組內建方法，讓開發者可以 **轉換大小寫、查找、修改、格式化、分割與拼接字串**。

本篇文章將介紹 **Python 常見的字串方法**，並搭配範例來幫助理解與應用。

<!--more-->

{{<alert>}}所有字串方法都會傳回新值，它們不會改變原始字串。{{</alert>}}

---

## 一、大小寫轉換

### 1.1 `capitalize()`

將字串的第一個字母轉換為大寫，其他字母保持小寫。

```python
txt = "hello, world!"
print(txt.capitalize())  # Hello, world!
```

### 1.2 `upper()` & `lower()`

- `upper()`: 將字串轉換為 **全部大寫**。
- `lower()`: 將字串轉換為 **全部小寫**。

```python
txt = "Hello, World!"
print(txt.upper())  # HELLO, WORLD!
print(txt.lower())  # hello, world!
```

### 1.3 `swapcase()` & `title()`

- `swapcase()`: 大寫變小寫，小寫變大寫。
- `title()`: 每個單詞的首字母轉換為大寫。

```python
txt = "hello, WORLD!"
print(txt.swapcase())  # HELLO, world!
print(txt.title())    # Hello, World!
```

---

## 二、搜尋與計數

### 2.1 `find()` & `rfind()`

- `find()`：回傳指定子字串的 **第一個** 出現位置。
- `rfind()`：回傳指定子字串的 **最後一個** 出現位置。

```python
txt = "Hello, world!"
print(txt.find("o"))   # 4
print(txt.rfind("o"))  # 8
```

### 2.2 **`count()`**

回傳指定子字串在字串中出現的次數。

```python
txt = "banana"
print(txt.count("a"))  # 3
```

---

## 三、字串修改

### 3.1 **`strip()`**, **`lstrip()`**, **`rstrip()`**

- `strip()`：移除字串開頭與結尾的空白。
- `lstrip()`：移除 **左側** 的空白。
- `rstrip()`：移除 **右側** 的空白。

```python
txt = "  Hello, World!  "
print(txt.strip())   # "Hello, World!"
print(txt.lstrip())  # "Hello, World!  "
print(txt.rstrip())  # "  Hello, World!"
```

### 3.2 **`replace()`**

替換字串中的某個子字串。

```python
txt = "Hello, World!"
print(txt.replace("H", "J"))  # Jello, World!
```

---

## 四、字串分割與合併

### 4.1 **`split()`** & **`rsplit()`**

- `split()`：依照指定的分隔符號，將字串分割成 **列表 (list)**。
- `rsplit()`：從 **右側** 開始分割。

```python
txt = "apple,banana,orange"
print(txt.split(","))   # ['apple', 'banana', 'orange']
```

### 4.2 **`join()`**

使用指定的字串來連接列表中的元素。

```python
words = ["apple", "banana", "orange"]
print(" - ".join(words))  # apple - banana - orange
```

---

## 五、字串對齊

### 5.1 **`center()`**, **`ljust()`**, **`rjust()`**

- `center(width)`：將字串置中，並填充左右的空白。
- `ljust(width)`：將字串靠左，並填充右側的空白。
- `rjust(width)`：將字串靠右，並填充左側的空白。

```python
txt = "Python"
print(txt.center(10, "-"))  # --Python--
print(txt.ljust(10, "-"))  # Python----
print(txt.rjust(10, "-"))  # ----Python
```

---

## 六、其他常見字串方法

| 方法           | 說明                             |
| -------------- | -------------------------------- |
| `isalnum()`    | 是否只包含字母與數字             |
| `isalpha()`    | 是否只包含字母                   |
| `isdigit()`    | 是否只包含數字                   |
| `isspace()`    | 是否只包含空白字符               |
| `startswith()` | 是否以指定字串開頭               |
| `endswith()`   | 是否以指定字串結尾               |
| `zfill(width)` | 在字串前填充 0，使其符合指定寬度 |

---

## 七、總結

Python 提供了許多內建字串方法，可以方便地 **轉換大小寫、搜尋、計數、修改、分割、對齊** 等。

**📌 應該記住的重要方法**：

- **大小寫轉換**：`upper()`, `lower()`, `capitalize()`, `swapcase()`
- **搜尋與計數**：`find()`, `count()`
- **字串修改**：`strip()`, `replace()`
- **分割與合併**：`split()`, `join()`
- **對齊**：`center()`, `ljust()`, `rjust()`

這些方法能夠幫助你更有效率地處理字串，提升 Python 開發的便利性！🚀
