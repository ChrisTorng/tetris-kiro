# 技術堆疊

## 核心技術

- **HTML5**：結構與 canvas 元素
- **CSS3**：樣式設計，包含漸層與現代化版面配置
- **原生 JavaScript (ES6+)**：所有遊戲邏輯與渲染
- **Canvas API**：遊戲渲染（主遊戲場地與下一個方塊預覽）

## 架構

單一檔案架構，所有程式碼（HTML、CSS、JavaScript）都包含在 `index.html` 中。

## 主要函式庫與框架

無 - 零外部依賴。所有功能都使用原生瀏覽器 API 實作。

## 開發方法

使用 Kiro 規格驅動開發（Spec-Driven Development）方法論建置，包含結構化的需求、設計文件與任務分解，位於 `.kiro/specs/browser-tetris-game/`。

## 常用指令

### 本地執行

```bash
# 選項 1：直接開啟檔案
# 直接在瀏覽器中開啟 index.html

# 選項 2：使用 Python 本地伺服器
python -m http.server 8000

# 選項 3：使用 Node.js 本地伺服器
npx http-server
```

### 測試

無自動化測試套件。遊戲包含大量 console 日誌，供開發期間手動驗證使用。

### 部署

無需建置流程。只需將 `index.html` 複製到任何靜態託管服務（GitHub Pages、Netlify 等）即可部署。

## 瀏覽器相容性

需要支援以下功能的現代瀏覽器：
- ES6+ JavaScript 功能（類別、箭頭函式、模板字串）
- Canvas API
- CSS3（漸層、flexbox、transforms）
