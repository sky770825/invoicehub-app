# 一人發票歸戶系統 — 產品規格書

## 1. 產品定位

**名稱**：InvoiceHub 發票歸戶  
**口報**：「發票拍一拍，中獎不漏接」  
**目標客群**：個人用戶、小店老闆（有營業稅需求）  
**核心價值**：用相機鏡頭 scan 歸戶，登打發票不再費時，統一管理不漏兌

---

## 2. MVP 功能

### 2.1 發票掃描（手機相機）
- 開啟相機，掃描發票 QR Code（或手動輸入）
- 支援財政部 QR Code 格式（10位數發票號碼 + 隨機碼）
- 自動解析：發票號碼、日期、金額
- 儲存至個人發票列表

### 2.2 手動輸入
- 發票號碼（10位）
- 開立日期
- 消費金額
- 載具類型（手機條碼/自然人憑證/愛心碼）

### 2.3 發票列表
- 按月份分類顯示所有歸戶發票
- 狀態標記：未兌/已兌/已凍
- 自動對獎（每期統一發票開獎日自動計算）
- 顯示獎金估算

### 2.4 自動對獎
- 支援每期（單月/雙月）開獎號碼對獎
- 特別獎/特獎/頭獎/增開六獎
- 顯示「中了多少！」提示

### 2.5 載具管理
- 綁定手機條碼（可用字母+數字）
- 顯示載具條碼（視覺化）

---

## 3. 資料模型

### Invoice
| 欄位 | 類型 |
|------|------|
| id | UUID |
| invoice_number | string（10位） |
| date | YYYY-MM |
| amount | number |
| carrier_type | enum（mobile_barcode/natural_id/love_code） |
| carrier_number | string |
| status | enum（active/claimed/frozen） |
| period | string（10801/10802...） |
| created_at | datetime |

### Settings
| 欄位 | 類型 |
|------|------|
| carrier_barcode | string |
| admin_password | bcrypt hash |

**儲存**：localStorage

---

## 4. 視覺方向
- 主色：#0891B2（青色，代表統一發票的發票色）
- 中獎提示：#FFD700（金色）
- 狀態色彩：綠（未兌）/ 灰（已兌）/ 冰藍（已凍）
- 字體：Noto Sans TC
- 全響應式（手機 scan 優先）

---

## 5. 交付產出
- `/tmp/invoice-collector/invoicehub.html`
- 部署至 GitHub Pages

---

## 6. 已知限制
- 不串接財政部 API（MVP 純本地計算對獎）
- QR Code 解析為簡化版（基本格式即可）
- 載具條碼顯示為文字序列，非真正條碼圖
