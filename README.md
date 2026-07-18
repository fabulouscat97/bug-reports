# Bug Reports / CPOchat — Matrix View

**🌐 語言 / Language：中文（目前） · [English](README.en.md)**

一個**離線、單檔** HTML bug 追蹤工具。開啟 [`bug-tracker-v4.html`](bug-tracker-v4.html) 就能直接使用，不需要安裝、不需要後端、不需要網路連線。所有資料都留在你自己的瀏覽器裡。

核心概念：每一個 bug 都橫跨 **Test → Dev → Production** 三個環境，用矩陣（表格）方式一覽每個環境各自的修復進度與驗證狀態。

---

## ✨ 主要功能

### 🧩 三環境矩陣視圖
- 每個 bug 一列，橫向分成 **Test / Dev / Production** 三欄。
- 每個環境各自有：
  - **Bug Fix ETA**（預計修復時間，可自由填文字，例如 `2026-05-30 · Next deployment`）
  - **Pass 勾選**（標記該環境已通過驗證）
  - **截圖**：分為 *Bug Evidence*（bug 證據）與 *Validation / Pass Evidence*（驗證證據）兩類
- 左側「Bug」欄可**拖曳分隔線調整寬度**，雙擊還原成預設寬度。

### 💾 IndexedDB 儲存
- 資料存在瀏覽器的 **IndexedDB**（比 localStorage 的 ~5MB 上限大很多，可容納數百 MB 含截圖）。
- 首次開啟時會自動把舊版 localStorage 的資料**一次性遷移**過來。
- 資料量接近 ~50MB 時會出現提醒，建議定期 Export 備份。

### 📸 截圖處理
- **上傳**檔案，或直接在輸入框內 **Ctrl+V 貼上**剪貼簿截圖。
- 圖片自動**壓縮**（最長邊縮到 1600px、轉 JPEG），大幅縮小體積同時保持可讀性。
- 點縮圖開啟**燈箱（Lightbox）**：支援放大縮小、滾輪縮放、拖曳平移；快捷鍵 `+` / `-` / `0`，`Esc` 關閉。

### ✏️ 就地編輯（Inline Editing）
- 直接點卡片上的 **Description / Solution / ETA / Notes** 就能就地修改。
- `Enter` 儲存、`Esc` 取消（多行欄位用 `Shift+Enter` 換行）。
- **Notes** 為多項目條列，可逐條新增、編輯、刪除。

### 🔍 篩選與排序
- 關鍵字搜尋（涵蓋 ID、標題、描述、解法、備註、Jira、負責人、ETA）。
- **Bug ID** 多選篩選、**Owner（負責人）** 多選篩選，皆附面板內即時搜尋。
- 狀態篩選：**Not Started**（0 環境通過）／**In Progress**（部分通過）／**Ready to Archive ✓**（三環境全通過）。
- 依 Bug ID 排序（A–Z / Z–A，自然數字排序）。

### 📦 Archive（封存）
- bug 三環境全部通過後標記為 **Ready to Archive**，可封存收納。
- 可單獨封存、查看封存區、移回作用中、或一次刪除所有封存項目。

### 📝 變更歷史
- 每個 bug 自動記錄**帶時間戳的變更歷史**（建立、狀態變更、ETA 修改、截圖增減、封存等）。

### 🎫 其他
- **Jira Ticket / URL** 欄位（填網址會變成可點連結）。
- **負責人（Owner）** 欄位，附既有名單自動建議。
- **亮／暗主題**切換（預設亮色，記憶你的選擇）。
- 頂部標題列、工具列、統計列皆為 **sticky**，捲動時保持可見。

### 📤 匯出／匯入
- **Export**：把全部資料匯出成 JSON 檔備份。
- **Import**：載入 JSON；若已有資料則詢問是否合併（重複 ID 會自動配發新 ID）。

---

## 🚀 使用方式

直接用瀏覽器開啟即可：

```
open bug-tracker-v4.html      # macOS
```

或把 `bug-tracker-v4.html` 拖進任何瀏覽器分頁。

> ⚠️ **資料儲存在「開啟這個檔案的那個瀏覽器」的 IndexedDB 裡。**
> 換瀏覽器、換電腦、或清除瀏覽器資料，資料不會自動同步。
> 要搬移或備份資料，請用右上角的 **⬆ Export / ⬇ Import**。

---

## 🔒 隱私

完全在本機運作，沒有任何伺服器、追蹤或外部請求。你的 bug 資料與截圖從不離開你的瀏覽器。

---

## 🛠 技術

- 單一 `.html` 檔，原生 HTML / CSS / JavaScript，**零相依套件**。
- 儲存：IndexedDB（資料）＋ localStorage（少量 UI 偏好，如主題、排序、欄寬、展開狀態）。
