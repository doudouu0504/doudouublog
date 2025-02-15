---
title: "Python 變數與全域變數解析"
draft: false
date: "2025-02-15T21:54:08+08:00"
categories: ["python"]
tags: ["變數", "全域變數", "程式設計"]
slug: "Python-basic-Variables"
---

## 前言

在 Python 中，變數是最基本的概念之一，它們用於儲存資料並在程式中使用。無需事先宣告變數的類型，Python 允許動態指派變數類型並支援多種操作方式。此外，Python 提供了全域變數與局部變數的概念，讓變數的作用域更加靈活。本篇文章將詳細介紹 Python 變數的基本操作、類型轉換、變數賦值、集合解壓縮與全域變數的應用。

<!--more-->

---

## 一、變數與基本操作

### 1.1 變數

變數是儲存資料值的容器。

### 1.2 創建變數

Python 沒有用於宣告變數的命令。當您第一次為變數賦值時，該變數就會被建立。

```python
x = 5
y = "John"
print(x)
print(y)
```

**輸出：**

```
5
John
```

變數不需要用任何特定類型聲明，甚至可以在設定後改變類型。

```python
x = 4       # x 是 int 類型
x = "Sally" # x 現在變成 str 類型
print(x)
```

**輸出：**

```
Sally
```

## 二、變數類型與操作

### 2.1 類型轉換（Casting）

如果您想指定變數的資料類型，可以透過強制轉換來完成。

```python
x = str(3)    # x 將變成 '3'
y = int(3)    # y 將變成 3
z = float(3)  # z 將變成 3.0
```

### 2.2 獲取變數類型

您可以使用 `type()` 函數取得變數的資料類型。

```python
x = 5
y = "John"
print(type(x))
print(type(y))
```

**輸出：**

```
<class 'int'>
<class 'str'>
```

## 三、變數賦值與運算

### 3.1 多個值對應多個變數

Python 允許你在一行中為多個變數賦值：

```python
x, y, z = "Orange", "Banana", "Cherry"
print(x)
print(y)
print(z)
```

**輸出：**

```
Orange
Banana
Cherry
```

### 3.2 一個值對應多個變數

您可以在一行中為多個變數指派相同的值：

```python
x = y = z = "Orange"
print(x)
print(y)
print(z)
```

**輸出：**

```
Orange
Orange
Orange
```

## 四、集合解壓縮與輸出變數

### 4.1 解壓縮集合（Unpacking Collections）

如果清單、元組等中有一個值集合，Python 允許您將這些值提取到變數中。這稱為解包。

```python
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits

print(x)
print(y)
print(z)
```

**輸出：**

```
apple
banana
cherry
```

### 4.2 輸出變數

Python `print()` 函數經常用來輸出變數。

**以逗號分隔多個變數：**

```python
x = "Python"
y = "is"
z = "awesome"
print(x, y, z)
```

**輸出：**

```
Python is awesome
```

**使用 `+` 運算子串接字串：**

```python
x = "Python "
y = "is "
z = "awesome"
print(x + y + z)
```

**輸出：**

```
Python is awesome
```

**`+` 運算子用於數字時為數學加法：**

```python
x = 5
y = 10
print(x + y)
```

**輸出：**

```
15
```

## 五、全域變數與 `global` 關鍵字

### 5.1 Python 全域變數

在函數外部建立的變數稱為**全域變數（Global Variable）**，可供任何人使用，無論是在函數內部還是外部。

```python
x = "awesome"

def myfunc():
  print("Python is " + x)

myfunc()
```

**輸出：**

```
Python is awesome
```

### 5.2 `global` 關鍵字

通常，當您在函數內部建立變數時，該變數是局部的，並且只能在該函數內部使用。

要在函數內部建立全域變數，可以使用 `global` 關鍵字。

```python
x = "awesome"

def myfunc():
  global x
  x = "fantastic"

myfunc()
print("Python is " + x)
```

**輸出：**

```
Python is fantastic
```

---

這篇文章介紹了 Python 變數的基本概念，如何建立與使用變數，以及如何在函數內外部管理全域變數。掌握這些概念有助於撰寫更可讀且可維護的 Python 程式！🚀
