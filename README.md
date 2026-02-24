# 俄羅斯方塊遊戲 (Tetris Game)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Live Demo](https://img.shields.io/badge/demo-online-green.svg)](https://christorng.github.io/tetris-kiro)

一個使用原生 JavaScript 和 CSS 實作的經典俄羅斯方塊遊戲，採用單一 HTML 檔案設計，無需任何外部依賴。

🎮 **[立即遊玩](https://christorng.github.io/tetris-kiro)**

## 特色

- ✨ **單一檔案實作** - 所有程式碼都包含在一個 HTML 檔案中
- 🚀 **零依賴** - 僅使用原生 JavaScript 和 CSS，無需任何外部套件
- 🎨 **繁體中文介面** - 完整的繁體中文使用者介面
- 🎯 **經典玩法** - 包含所有 7 種標準四方塊類型 (I, O, T, S, Z, J, L)
- 📊 **計分系統** - 根據消除行數給予不同分數 (1/2/3/4 行 = 100/300/500/800 分)
- 🔄 **等級系統** - 每消除 10 行提升一個等級，遊戲速度逐漸加快
- ⌨️ **鍵盤操作** - 支援方向鍵移動、旋轉和空白鍵瞬降

## 遊戲操作

| 按鍵 | 功能 |
|------|------|
| ← | 向左移動 |
| → | 向右移動 |
| ↓ | 向下移動（緩降，+1 分） |
| ↑ | 順時針旋轉 |
| 空白鍵 | 瞬降（距離 × 2 分） |

## 遊戲規則

- **場地大小**: 10 欄 × 20 列
- **四方塊類型**: 7 種標準類型 (I, O, T, S, Z, J, L)
- **計分規則**:
  - 消除 1 行: 100 分
  - 消除 2 行: 300 分
  - 消除 3 行: 500 分
  - 消除 4 行: 800 分
  - 緩降: 每格 1 分
  - 瞬降: 每格 2 分
- **等級系統**: 每消除 10 行提升一個等級
- **速度變化**: 下落間隔 = max(100, 1000 - 等級 × 100) 毫秒
- **遊戲結束**: 當新四方塊無法生成時遊戲結束

## 技術實作

本專案使用 **Kiro Spec 功能**進行開發，採用規格驅動開發 (Spec-Driven Development) 方法論：

1. **需求分析** - 定義完整的使用者故事和驗收標準
2. **設計文件** - 制定系統架構和類別設計
3. **任務分解** - 將實作分解為漸進式的開發任務
4. **逐步實作** - 按照任務清單系統化地完成開發

### 專案結構

```
tetris-kiro/
├── index.html              # 主遊戲檔案（包含 HTML、CSS、JavaScript）
├── .kiro/specs/           # Kiro Spec 規格文件
│   └── browser-tetris-game/
│       ├── requirements.md # 需求文件
│       ├── design.md      # 設計文件
│       └── tasks.md       # 任務清單
├── LICENSE                # MIT 授權條款
└── README.md             # 本文件
```

### 核心類別

- **GameField** - 遊戲場地管理
- **Tetromino** - 四方塊資料結構
- **TetrominoManager** - 四方塊生成與操作
- **CollisionDetector** - 碰撞偵測
- **GravitySystem** - 重力系統
- **LineClearSystem** - 消行系統
- **ScoringSystem** - 計分系統
- **LevelSystem** - 等級系統
- **Renderer** - 畫面渲染
- **InputHandler** - 輸入處理
- **GameStateManager** - 遊戲狀態管理

## 本地執行

1. 複製此儲存庫：
```bash
git clone https://github.com/ChrisTorng/tetris-kiro.git
cd tetris-kiro
```

2. 在瀏覽器中開啟 `index.html` 檔案即可開始遊戲

或使用本地伺服器：
```bash
# 使用 Python
python -m http.server 8000

# 使用 Node.js
npx http-server
```

然後在瀏覽器中開啟 `http://localhost:8000`

## 關於 Kiro Spec

[Kiro](https://kiro.dev) 是一個 AI 輔助開發工具，其 Spec 功能提供了結構化的開發流程：

- 📝 **需求文件** - 使用使用者故事和驗收標準定義功能
- 🏗️ **設計文件** - 規劃系統架構和實作細節
- ✅ **任務清單** - 將開發工作分解為可追蹤的任務
- 🤖 **AI 協作** - 與 AI 助手協作完成實作

本專案展示了如何使用 Kiro Spec 功能從零開始建立一個完整的遊戲應用。

## 授權條款

本專案採用 MIT 授權條款 - 詳見 [LICENSE](LICENSE) 檔案

## 致謝

- 使用 [Kiro](https://kiro.dev) 的 Spec 功能進行開發
- 靈感來自經典的俄羅斯方塊遊戲

---

**Made with ❤️ using Kiro Spec**
