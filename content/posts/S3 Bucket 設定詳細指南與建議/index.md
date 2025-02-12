---
date: "2025-01-25T13:32:50+08:00"
draft: false
title: "S3 Bucket 設定詳細指南與建議"
tags: ["Django", "AWS"]
categories: ["軟體教學"]
slug: "S3Bucket-set"
---

## 前言

本文將逐步解析 **AWS S3 Bucket** 的設定選項，並針對常見情境提供最佳化建議，幫助你更快上手並避免常見錯誤。
並且分享一部完整介紹專案如何連接 AWS S3 設置的影片。

<!--more-->

---

{{< youtubeLite id="y12KO8XM6jw" label="Blowfish-tools demo" >}}
{{< alert >}}以上是完整的設置 AWS S3 影片，文章內容是介紹 Bucket 的詳細設定。{{< /alert >}}

---

## **一、General Configuration**

### 1.1 選擇 Bucket 類型

- **建議選擇 General Purpose（預設）**：
  - 適用於大多數應用情境，支援各類型檔案儲存（圖片、影片、文件等）。
  - **Directory** 適用於大數據管理，對一般應用不必要。

### 1.2 設定 Bucket 名稱

- **Bucket 名稱需全球唯一**，建議使用簡單且有意義的名稱，例如：
  - `my-app-user-avatars`
  - `project-name-profile-images`
- **命名規則**：
  - 只能使用 **小寫字母、數字、破折號（-）**。
  - 不能以破折號開頭或結尾。

### 1.3 是否複製現有 Bucket 設定？

- **建議略過**，除非有相似專案需要沿用相同的設定。

---

## **二、Object Ownership**

### 2.1 ACLs Disabled（推薦）

- **建議選擇 ACLs Disabled**（預設值）：
  - 物件的所有權由 Bucket 擁有者（你）完全控制。
  - 提高安全性，避免不必要的權限複雜度。

### 2.2 ACLs Enabled（不建議）

- **僅適用於需要細粒度權限控管的特殊情境**。
- 對於大部分應用而言，ACLs 會增加不必要的管理負擔。

---

## **三、Block Public Access**

### 3.1 是否應該封鎖公開訪問？

- **建議選擇 `Block all public access`（預設）**：
  - 避免意外公開敏感數據，提高安全性。
  - 若有特定檔案需公開，可於**上傳時單獨設定公開權限**。

---

## **四、Bucket Versioning**

### 4.1 是否啟用版本控制？

- **建議選擇 Disable（預設）**：
  - 只保留最新版本，節省儲存空間與管理成本。
- **啟用 Versioning 適用場景**：
  - 頻繁變更的重要檔案（如系統日誌、合約文件）才建議開啟。

---

## **五、Tags（可選）**

- 可新增標籤來分類與管理資源，例如：
  - `Key: Environment, Value: Production`
  - `Key: Project, Value: MyApp`
- **建議：若無特定需求可省略**。

---

## **六、Default Encryption**

AWS 提供多種加密方式，可保護儲存於 S3 的資料。

### 6.1 SSE-S3（推薦）

- **建議選擇 SSE-S3**（預設值）：
  - S3 內建金鑰管理，適用於大多數應用。

### 6.2 SSE-KMS

- 適用於高安全性需求（如金融、醫療數據）。
- **需額外設定 AWS Key Management Service（KMS）**，並可能產生額外成本。

### 6.3 DSSE-KMS

- 提供更高級的雙層加密，適用於合規性要求高的情境（如 GDPR、HIPAA）。

---

## **七、最佳設定建議總覽**

| 設定項目                | 建議選擇                | 原因           |
| ----------------------- | ----------------------- | -------------- |
| **Bucket 類型**         | General Purpose（預設） | 適用於一般用途 |
| **Bucket 名稱**         | 自訂名稱                | 必須全球唯一   |
| **複製現有設定**        | 略過                    | 非必要         |
| **Object Ownership**    | ACLs Disabled（推薦）   | 簡單且安全     |
| **Block Public Access** | Block all public access | 避免數據外洩   |
| **Bucket Versioning**   | Disable                 | 節省空間       |
| **Tags**                | 可略過                  | 非必要         |
| **Default Encryption**  | SSE-S3（預設）          | 內建加密管理   |

---

## **結論**

透過本指南，你已經了解 AWS S3 Bucket 的核心設定，並掌握了不同選項的適用情境。

### **回顧學習重點**

1. **選擇 General Purpose** 作為 Bucket 類型。
2. **Bucket 名稱需全球唯一**，且符合命名規則。
3. **建議啟用 `Block all public access`** 來提高安全性。
4. **ACLs 建議關閉**，讓擁有者全權管理存取權限。
5. **預設加密選擇 SSE-S3**，確保數據安全。

透過這些最佳化建議，你可以更有效率地管理 S3 Bucket，確保數據安全與存取靈活性！🚀
