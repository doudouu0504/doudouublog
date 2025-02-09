---
date: "2024-11-22T10:41:17+08:00"
draft: false
title: "使用 Django 建立一個頁面"
tags: ["Django", "CRUD"]
categories: ["python", "軟體教學"]
---

## 前言

安裝 Django、MTV 模式中的 Template (T) 與 View (V) 實作練習。

本篇文章將介紹如何使用 Django 建立一個 `about` 頁面。

<!--more-->

---

> **首先，先分享完整ＣＲＵＤ流程!!!**

{{< youtubeLite id="jhw5rzoMCPM" label="Django-CRUD 練習(快速版)" >}}
{{<alert>}}本篇文章將實作 **T (Template) 和 V (View)** 的部分。{{</alert>}}

## 一、MVC 與 MTV 模式簡介

### 1.1 MVC（Model-View-Controller）

- <span style="color:red">M</span>（Model，模型）：負責與資料庫交互，執行 CRUD（新增、讀取、更新、刪除）。
- <span style="color:red">V</span>（View，視圖）：負責處理業務邏輯並渲染頁面。
- <span style="color:red">C</span>（Controller，控制器）：處理 Request、Response，管理 Model 與 View 之間的交互。

### 1.2 MTV（Model-Template-View）

Django 採用 MTV 模式，概念上類似 MVC，但有所區別：

- <span style="color:red">M</span>（Model）：與 MVC 的 Model 相同。
- <span style="color:red">T</span>（Template）：負責前端頁面（HTML、CSS、JavaScript）。
- <span style="color:red">V</span>（View）：負責處理請求並回傳適當的模板頁面。
- Django 的 **Controller 角色由框架本身處理**。

## 二、安裝 Django 並建立專案

### 2.1 使用 Poetry 安裝 Django

建議使用 **Poetry** 來建立虛擬環境並安裝 Django。

```sh
poetry new myproject
cd myproject
poetry add django
```

> **注意**：確保 **app 資料夾** 必須放在 **專案根目錄**，並寫入 `settings.py` 的 `INSTALLED_APPS` 內。

### 2.2 建立 Django 專案

```sh
django-admin startproject pydev .
```

> **注意**：最後的 `.` 代表將專案初始化在目前目錄。

### 2.3 設定專案 URL

在 `pydev/urls.py` 中新增路由：

```py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("pages.urls")),
]
```

> `include("pages.urls")` 允許我們將應用程式的 URL 組織到單獨的 `urls.py` 檔案。

## 三、建立 `about` 頁面

### 3.1 建立 `pages` 應用程式

```sh
python manage.py startapp pages
```

在 `pages/` 內建立 **以下結構**：

```
pages/
│── migrations/
│── templates/
│   └── pages/
│       └── about.html
│── views.py
│── urls.py
```

### 3.2 設定 `pages/urls.py`

```py
from django.urls import path
from pages.views import about

urlpatterns = [
    path("about/", about),
]
```

### 3.3 設定 `pages/views.py`

```py
from django.shortcuts import render

def about(request):
    return render(request, "pages/about.html")
```

### 3.4 建立 `about.html`

建立 `pages/templates/pages/about.html`：

```html
{% extends "shared/layout.html" %} {% block content %}
<h1>About</h1>
{% endblock %}
```

### 3.5 建立 `layout.html`

建立 `templates/shared/layout.html`：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My Django App</title>
  </head>
  <body>
    {% block content %}{% endblock %}
  </body>
</html>
```

> **注意**：必須確保 `settings.py` 中 `TEMPLATES` 設定的 `DIRS` 內包含 `templates/` 目錄，否則無法找到 `layout.html`。

```py
TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": ["templates"],
        "APP_DIRS": True,
        "OPTIONS": {...},
    },
]
```

## 四、啟動伺服器並測試

```sh
python manage.py runserver
```

打開瀏覽器，訪問 `http://127.0.0.1:8000/about/`，應該可以看到 `about` 頁面。

---

## 五、Django 註解語法

```html
{% comment %} 這是一個 Django 註解 {% endcomment %}
```

> Django 使用 **Django Template Language (DTL)**，雖然語法類似 Jinja2，但實際上是 Django 獨有的模板語言。

---

## 六、結論

本篇文章示範了 **如何使用 Django 建立一個簡單的 `about` 頁面**，並介紹了 MTV 模式中的 **Template (T) 與 View (V)**。

**重點回顧**：

1. 使用 `Poetry` 安裝 Django 並建立專案。
2. 建立 Django 應用程式 `pages` 並新增路由與視圖。
3. 使用 `render` 方法回傳 HTML 模板。
4. 設定 `layout.html` 讓多個頁面共用模板結構。

希望這篇文章能幫助你更快掌握 Django 的基本概念！🚀
