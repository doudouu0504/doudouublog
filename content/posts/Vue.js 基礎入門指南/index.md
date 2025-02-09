---
date: "2024-12-02T10:44:40+08:00"
draft: false
title: "Vue.js 基礎入門指南"
tags: ["Vue.js"]
categories: ["軟體教學"]
---

## 前言

本篇文章適合 Vue.js 初學者，將帶你快速了解 **Vue.js 的基礎指令、事件處理、迴圈應用**，並示範如何搭建專案環境。透過本篇教學，你將能夠寫出 Vue.js 的基礎應用，並進一步理解 Vue 的核心概念。

<!--more-->

---

## 一、Vue.js 基本概念

### 1.1 Vue.js 指令與響應式資料

- **Vue 指令 (`v-` 開頭)**：Vue 使用 `v-` 作為指令前綴，例如 `v-model`、`v-bind` 等。
- **響應式變數 (`ref`)**：使用 `ref` 定義變數，Vue 會自動追蹤其變更，並即時更新畫面。
- **不需直接操作 DOM**：Vue 自動處理 UI 更新，開發者無需使用 `document.querySelector` 來手動抓取 DOM 元素。

### 1.2 Vue.js 基本範例

以下是 Vue.js 的 Hello World 範例，使用 `ref` 定義響應式變數 `msg`，並讓輸入框綁定到變數。
[點擊練習網址](https://play.vuejs.org/#eNp9kctOwzAQRX9l8CYgVakQrEpa8VClwgIQILHxJkqnqYtjW36ESlH+nbFDUxaoiyiZudeTcz0duzMmbwOyGStcZYXx4NAHs+BKNEZbDx1Y3EAPG6sbyMiaccVVpZXz0Lga5lE/z1YopYZPbeX6LLu4OXqEMsGvSrWWaMmMLSoP8wV0XEEckLelDHhQcl/aGv3QpCk9PcV0ICMmKjw2RpYeqQIotpeLrkscfV9MqUrd9E+4Ta85Z38ROINpMsW54yw2Yd4R70bU+c5pRdeR+DirdGMEnXsxXlAezmYDedRKivz9lHreBpwc+tUWq69/+ju3jz3OXi06tC1yNmpD7kFevj/jnr5HsdHrIMl9QnxDp2WIjIPtPvzGHX2J9jEtVaj6wy33HpU7hIqg0dknP2e06IcT0Y+4V/l1Oke7Yv0PGrvFqQ==)

```html
<script setup>
  import { ref } from "vue";
  const msg = ref("Hello World!");
</script>

<template>
  <h1>{{ msg }}</h1>
  <input v-model="msg" />
</template>
```

## 二、事件處理

### 2.1 v-model (表單綁定)

`v-model` 用於雙向綁定輸入框與變數，適用於表單元素，例如 `input`、`textarea`。

```html
<input v-model="msg" />
```

### 2.2 v-on 事件綁定 (縮寫 `@`)

Vue 事件處理可使用 `v-on` 綁定，縮寫為 `@`。

```html
<script setup>
  import { ref } from "vue";
  const msg = ref("Hello Vue!");
  const updateMessage = (event) => {
    msg.value = event.target.value;
  };
</script>

<template>
  <input @input="updateMessage" />
</template>
```

### 2.3 設定條件樣式

可透過 `v-bind:class` 動態設定 CSS，以下範例當字數超過 15 時，文字變紅色。

```html
<template>
  <h1 :class="{ red: msg.length > 15 }">{{ msg }}</h1>
</template>

<style>
  .red {
    color: red;
  }
</style>
```

## 三、迴圈渲染

### 3.1 v-for 迴圈渲染

`v-for` 可用於渲染陣列內容，以下範例遍歷 `products` 陣列。
[點題練習網址](https://play.vuejs.org/#eNq1lNtqE0EYx19lmJve1N3YVmhiGlDphV6oeLpxvIibSTJ1d2aYmY2BsCC0VVoNBgRTq1IrESO24AlPtPgy3d3kLZw95ACm3pTszRy+/zf7+w4zDXiOc6PmYpiDeWkJwhWQWLm8gChxOBMKNIDAZeCBsmAOmNHSGUQRtRiVCnDBSq6lJFgCtxEF+mskAwAIKqJsjGBOT/0n7WC/1X/bDT/tht/W+p1W0FlHcHYk5oJYsfj0XDYztk+cYiU9pKoUlznT5MSSrmPwKlNMmguZjDmfySCY+Hip72SOcG03/LHdazfDjRe9B1+DDzuTIeYWpggRbLZv3upvfQle7vmd5/679mSGxcXpIfidbX9zp7d6GO4/7HW3gld7xxQjm50aw9HPZv/pYf/xwdGf18Hvj+Gz75MZzpysFIjeOYto3kyaW7e1XijscLuosF7lS6QGaqfKTCzpw7UBEDpsawS1AoBIU/BbzbD7OQcaDRDJjDgS4Hl5M7KOZKu/gjcHI1kcxr+ycP19uPEI5IlT0X+/S2gpJ4WVIhhpkIWB02CMZmPscBYqqS9imVSMFcmovsNxqhG0mMOJjcUVroi+qFG+0iIgWLRtdv9SvKeEi9Pcap8qtu5N2F+R9STfVwWWWNQ02NCmiqKCVWJevn4Z1/V8aHR0EgfFPsZ4DUtmuxFjIjvv0pLGHtPFtBfjl4jQyg25XFeYykFQEWikTDoNQf06XfhP6CPceWMh9kPUg95fqfmz/A==)

```html
<script setup>
  const products = [
    { title: "北歐風簡約餐椅", price: 1290 },
    { title: "無線藍牙耳機", price: 2490 },
  ];
</script>

<template>
  <div v-for="item in products" :key="item.title">
    <div>名稱: {{ item.title }}</div>
    <div>價格: {{ item.price }}</div>
  </div>
</template>
```

## 四、Vue.js 開發環境搭建

### 4.1 建立 Vue.js 專案

在終端機執行以下指令來初始化 Vue.js 專案。

```sh
npm init vue@latest my-vue-app
cd my-vue-app
npm install
```

### 4.2 啟動開發伺服器

```sh
npm run dev
```

成功執行後，終端機將顯示開發伺服器的網址，例如 `http://localhost:5173/`。

## 五、Vue.js 主應用程式 (main.js)

Vue 應用程式的入口檔案為 `main.js`，`createApp` 負責初始化應用。

```js
import { createApp } from "vue";
import App from "./App.vue";
createApp(App).mount("#app");
```

## 六、結論

透過本篇教學，你已經學會了 Vue.js 的 **指令、事件處理、迴圈渲染**，並成功搭建 Vue.js 專案環境。Vue.js 讓開發者能夠更專注於應用邏輯，而不必直接操作 DOM，讓開發更直觀且高效。

如果你對 Vue.js 有興趣，建議繼續學習 **元件化開發、Vue Router、Vuex (Pinia)** 等進階主題，進一步提升你的開發能力！🚀
