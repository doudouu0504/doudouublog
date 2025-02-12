---
date: "2024-12-21T21:17:34+08:00"
draft: false
title: "如何在 Django 中實現 LINE 登入功能"
tags: ["Django", "Line", "第三方金流"]
categories: ["軟體教學"]
slug: "Django-Line-Login"
---

## 前言

在這篇文章中，將詳細介紹如何在 Django 項目中實現 LINE 登入功能。我們會使用 django-allauth 這個強大的第三方庫，讓開發者可以輕鬆集成各種社交平台的登入功能。

<!--more-->

LINE 是一款流行的即時通訊軟體，它的開放平台為開發者提供了方便的 API，讓用戶可以使用 LINE 賬號快速登入網站或應用程式。對於需要快速提升用戶體驗的網站來說，社交登入是非常重要的功能。

本文的目標是幫助開發者從零到有，實現一個支持 LINE 登入的 Django 項目，並涵蓋完整的流程與實現細節。

---

## 流程圖

```css
[用戶點擊登入按鈕]
    ↓
[跳轉到 LINE 授權頁面]
    ↓
[用戶授權成功]
    ↓
[回調到 Django URL 並處理授權碼]
    ↓
[完成登入，跳轉到指定頁面]

```

## 一、環境準備

在開始之前，確保你已經準備好以下環境：

1 、安裝 Python 3.6 或更高版本。

2 、安裝並設定 Django（推薦版本 3.2 或更高）。

3 、熟悉基本的 Django 配置與開發流程。

此外，確保你已註冊 LINE Developers 賬號，因為稍後我們需要配置 LINE 的開發者平台。

## 二、註冊 LINE 開發者賬號並創建應用

1、 登錄 LINE Developers。

2、 創建一個新的 Channel：

- 點擊 Create a new provider，填寫應用名稱。

- 在 Channels 中選擇 Create a Messaging API channel 或 Create a Web App（此處我們選 Web App）。

3、 獲取 Channel ID 與 Channel Secret：

- Channel ID：稍後配置為 client_id。

- Channel Secret：稍後配置為 secret。

4、 配置 LINE Developers 中增加回調 URL：

- 在 LINE 開發者平台的應用設置中，找到 Callback URL。

```bash
https://yourdomain.com/accounts/line/login/callback/
```

- 如果在本地測試，可以使用工具如 ngrok，生成臨時的 HTTPS URL。

- 或是像我作為測試環境使用:

```bash
http://127.0.0.1:8000/accounts/line/login/callback/
```

5、在根目錄增加 URL

```bash
path("accounts/", include("allauth.urls"))
```

## 三、安裝必要的依賴

### 3.1 安裝 django-allauth

```bash
pip install django-allauth
```

若是使用 poetry 環境，則輸入：

```bash
poetry add django-allauth
```

## 四、配置 Django

### 4.1 添加應用到 INSTALLED_APPS

```py
# 在 settings.py 中添加應用
INSTALLED_APPS += [
    "django.contrib.sites", # 支持多站點功能，是 django-allauth 的依賴
    "allauth", # django-allauth 主框架
    "allauth.account", # 提供帳號註冊、登入等功能
    "allauth.socialaccount", # 支持社交平台登入
    "allauth.socialaccount.providers.line", # LINE 登入的支持
]
# 設置站點 ID，對應 Django sites 框架中的主站點
SITE_ID = 1
```

> `django.contrib.sites`：Django 的多站點框架，django-allauth 必需。
> `allauth.socialaccount.providers.line`：啟用 LINE 作為登入提供者。

### 4.2 配置 LINE 提供者

在 `settings.py` 中，添加 LINE 的社交登入配置：

```py
from dotenv import load_dotenv
import os
# 加載環境變量（來自 .env 文件）
load_dotenv()

SOCIALACCOUNT_PROVIDERS = {
    "line": {
        "APP": {
            "client_id": os.getenv("LINE_CLIENT_ID"),# 從環境變量中讀取 LINE Channel ID
            "secret": os.getenv("LINE_SECRET"),# 從環境變量中讀取 LINE Channel Secret
            "key": "",
        },
        "SCOPE": ["profile", "openid", "email"],# 要求的權限範圍：用戶資料、開放身份和電子郵件
        "AUTH_PARAMS": {"response_type": "code"}, # 授權類型：使用授權碼
    },
}

```

將 LINE 憑據存儲到 .env 文件中：

```bash
LINE_CLIENT_ID = 你的LINE Channel ID
LINE_SECRET = 你的LINE Channel Secret
```

### 4.3 配置登錄與跳轉

在 `settings.py` 中，配置登入和跳轉路徑：

```py
# 配置登入和跳轉的 URL
LOGIN_URL = "/users/login/" # 用戶未登錄時重定向的登錄頁面
LOGIN_REDIRECT_URL = "/" # 登錄成功後的重定向頁面
ACCOUNT_SIGNUP_REDIRECT_URL = "/" # 註冊成功後的重定向頁面

SOCIALACCOUNT_LOGIN_ON_GET = True # 點擊登入按鈕後立即跳轉到 LINE 授權頁面
```

> `LOGIN_URL` ：未登錄用戶被重定向的路徑。
> `LOGIN_REDIRECT_URL` ：登錄成功後的跳轉地址。
> `SOCIALACCOUNT_LOGIN_ON_GET` ：用戶點擊登入後直接跳轉授權頁面，無需額外操作。

## 五、運行數據庫遷移

啟用 `sites` 框架和社交賬號的數據模型：

```bash
python manage.py migrate
```

- 此命令應在終端中執行，用於創建 `django-allauth` 和 `django.contrib.sites` 所需的數據表。
- 確保所有配置和應用已正確添加到 `INSTALLED_APPS` 中。

## 六、添加登入按鈕

在網站的模板檔案中，使用 `django-allauth` 提供的模板標籤生成 LINE 登入按鈕：

```html
<!--templates/login.html-->
<a href="{% provider_login_url 'line' %}">Login with LINE</a>
```

這段代碼使用了 `django-allauth` 的模板標籤，生成 LINE 登入的 URL。當用戶點擊後，將被重定向到 LINE 的授權頁面。

## 七、測試登入流程

### 7.1 測試授權

1、啟動本地開發伺服器：

```bash
python manage.py runserver
```

2、打開瀏覽器，訪問 `/users/login/`，點擊 Login with LINE。

3、你將被重定向到 LINE 的授權頁面，允許訪問後返回網站。

### 7.2 獲取用戶數據

如果需要使用授權後的用戶資料，可以通過 `SocialAccount` 模型獲取：

```py
#views.py
from allauth.socialaccount.models import SocialAccount

# 獲取當前登錄用戶的 LINE 資料
def user_profile(request):
    user = request.user
    if user.is_authenticated:
        # 查詢 LINE 的 SocialAccount 資料
        social_account = SocialAccount.objects.filter(user=user, provider='line').first()
        if social_account:
            line_profile = social_account.extra_data  # 包含 LINE 用戶信息
            return JsonResponse(line_profile) # 返回用戶資料作為 JSON 響應
    return HttpResponse("Not logged in.") # 如果未登錄，返回提示

```

- `SocialAccount` 模型用於存儲來自社交平臺的用戶數據。
- 該視圖會返回當前用戶的 LINE 資料或提示未登錄。

## 八、部署到生產環境

在生產環境中部署時，需注意：
1、 使用 HTTPS：LINE 要求回調 URL 必須是 HTTPS。
2、 正確配置域名：確保在 LINE 開發者平台的 Callback URL 與你的站點域名一致。
3、 隱藏敏感信息：通過 `.env `文件或環境變量存儲 `client_id` 和 `secret`。

### 8.1 在部署時的配置內容

以下是使用 `zeabur 部署`時增加的內容

在 `settings.py` 中添加：

```bash
LINE_CALLBACK_URL = os.getenv(
    "LINE_CALLBACK_URL", "http://localhost:8000/accounts/line/login/callback/"
)

SECURE_PROXY_SSL_HEADER = ("HTTP_X_FORWARDED_PROTO", "https")

CSRF_TRUSTED_ORIGINS = [
    "https://trico.zeabur.app",
    "http://127.0.0.1:8000",
]
ALLOWED_HOSTS = [
    "127.0.0.1",
    "localhost",
    "*",
]
```

在`.env`中配置：

```bash
LINE_CALLBACK_URL=https://trico.zeabur.app/accounts/line/login/callback/

```

在 LINE Developers 的 Callback URL 中加入以下內容，一個是你的測試環境，一個是你部署的網址

```bash
http://127.0.0.1:8000/accounts/line/login/callback/
https://trico.zeabur.app/accounts/line/login/callback/
```

{{< alert >}}注意！！！ 不可以加逗號{{< /alert >}}

## 九、結語

這樣應該已經成功實現了 LINE 登入功能！

django-allauth 不僅支持 LINE，還可以輕鬆集成其他社交平台（如綁定多個賬號、用戶資料同步，像是 Google、Facebook 等）。

可以進一步探索其 API，實現更多功能，如用戶資料同步、綁定多個社交賬號等，讓網站更加實用。

**參考資源：**
[django-allauth 官方文檔](https://django-allauth.readthedocs.io/en/latest/)
[LINE_Developers 平台](https://developers.line.biz/en/)
