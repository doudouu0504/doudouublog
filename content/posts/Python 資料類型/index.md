---
title: "Python 資料類型完整解析"
draft: false
date: "2025-02-16T14:05:08+08:00"
categories: ["python"]
tags: ["資料類型", "內建型別", "程式設計"]
slug: "python-basic-datatypes"
--------------------------

## 前言

在程式設計中，**資料型態** 是一個重要的概念。變數可以儲存不同類型的數據，而不同的數據類型提供不同的功能。
此篇文章了解 Python 內建資料類型，包括文字、數字、序列、映射、設定、布林和二進位類型，並學習如何設定與獲取資料型態。

<!--more-->

---

Python 預設內建了多種資料類型，可以大致分為以下幾類：

## 一、Python 內建資料類型

### 1.1 資料類型分類

Python 內建的資料型態主要分為以下幾類：

- **文字類型（Text Type）：** `str`
- **數字類型（Numeric Types）：** `int`、`float`、`complex`
- **序列類型（Sequence Types）：** `list`、`tuple`、`range`
- **映射類型（Mapping Type）：** `dict`
- **集合類型（Set Types）：** `set`、`frozenset`
- **布林類型（Boolean Type）：** `bool`
- **二進位類型（Binary Types）：** `bytes`、`bytearray`、`memoryview`
- **無類型（None Type）：** `NoneType`

### 1.2 取得資料類型

可以使用 `type()` 函數來取得變數的資料類型。

**範例：取得變數 `x` 的類型**

```python
x = 5
print(type(x))
```

**輸出：**

```
<class 'int'>
```

## 二、設定資料類型

### 2.1 預設資料類型

當你為變數賦值時，Python 會自動設定適當的資料類型。

| 變數 | 值                                         | 資料類型     |
| ---- | ------------------------------------------ | ------------ |
| `x`  | `"Hello World"`                            | `str`        |
| `x`  | `20`                                       | `int`        |
| `x`  | `20.5`                                     | `float`      |
| `x`  | `1j`                                       | `complex`    |
| `x`  | `['apple', 'banana', 'cherry']`            | `list`       |
| `x`  | `('apple', 'banana', 'cherry')`            | `tuple`      |
| `x`  | `range(6)`                                 | `range`      |
| `x`  | `{"name": "John", "age": 36}`              | `dict`       |
| `x`  | `{"apple", "banana", "cherry"}`            | `set`        |
| `x`  | `frozenset({"apple", "banana", "cherry"})` | `frozenset`  |
| `x`  | `True`                                     | `bool`       |
| `x`  | `b"Hello"`                                 | `bytes`      |
| `x`  | `bytearray(5)`                             | `bytearray`  |
| `x`  | `memoryview(bytes(5))`                     | `memoryview` |
| `x`  | `None`                                     | `NoneType`   |

### 2.2 使用建構子設定資料類型

如果想要指定特定的資料類型，可以使用對應的建構子來轉換。

**範例：指定不同資料類型**

```python
x = str("Hello World")  # str
x = int(20)  # int
x = float(20.5)  # float
x = complex(1j)  # complex
x = list(("apple", "banana", "cherry"))  # list
x = tuple(("apple", "banana", "cherry"))  # tuple
x = range(6)  # range
x = dict(name="John", age=36)  # dict
x = set(("apple", "banana", "cherry"))  # set
x = frozenset(("apple", "banana", "cherry"))  # frozenset
x = bool(5)  # bool
x = bytes(5)  # bytes
x = bytearray(5)  # bytearray
x = memoryview(bytes(5))  # memoryview
```

## 三、類型轉換（Type Conversion）

在 Python 中，可以使用 `int()`、`float()` 和 `complex()` 方法將數據從一種類型轉換為另一種類型。

### 3.1 數字類型轉換

```py
x = 1    # int
y = 2.8  # float
z = 1j   # complex

# 轉換 int 為 float
a = float(x)

# 轉換 float 為 int
b = int(y)

# 轉換 int 為 complex
c = complex(x)

print(a)
print(b)
print(c)

print(type(a))
print(type(b))
print(type(c))
```

輸出：

```
1.0
2
(1+0j)
<class 'float'>
<class 'int'>
<class 'complex'>
```

這些轉換允許開發者根據需求動態轉換變數的數據類型。例如，將整數轉換為浮點數可以在數學計算中提高精度，而將整數轉換為複數則適用於科學計算。

## 總結

Python 內建了多種資料類型，能夠適應不同的應用場景。在開發過程中，了解這些類型的特性與使用方式，有助於撰寫高效且穩定的程式。

---

這篇文章介紹了 Python 的內建資料型態，如何取得變數類型，以及如何設定與轉換不同的資料型態。希望這些概念能幫助你更深入理解 Python 的變數與資料類型！🚀
