# 專案結構

## 檔案組織

```
tetris-kiro/
├── index.html              # 主遊戲檔案（全部整合）
├── .kiro/
│   ├── specs/
│   │   └── browser-tetris-game/
│   │       ├── .config.kiro      # 規格設定
│   │       ├── requirements.md   # 功能需求
│   │       ├── design.md         # 技術設計
│   │       └── tasks.md          # 實作任務
│   └── steering/
│       ├── product.md            # 產品概述
│       ├── tech.md               # 技術堆疊與指令
│       └── structure.md          # 本檔案
├── LICENSE                 # MIT 授權條款
└── README.md              # 專案文件
```

## 程式碼組織（index.html 內部）

單一 HTML 檔案組織成清楚的區段：

### 1. HTML 結構
- 遊戲容器與 canvas 元素
- 側邊面板：分數、等級、下一個方塊預覽
- 控制按鈕與操作說明

### 2. CSS 樣式
- 現代化漸層背景
- 使用 flexbox 的響應式版面配置
- 遊戲結束覆蓋層樣式

### 3. JavaScript 架構

#### 常數與設定
- `SHAPES`：四方塊形狀定義（每種 4 個旋轉狀態）
- `COLORS`：每種四方塊類型的顏色對應
- `FIELD_WIDTH`、`FIELD_HEIGHT`：遊戲場地尺寸（10×20）
- `SCORE_RULES`：計分規則常數
- `KEY_MAPPING`：鍵盤輸入對應

#### 核心類別（依序）
1. **Tetromino**：代表單一四方塊，包含位置與旋轉狀態
2. **GameField**：管理 10×20 遊戲場地
3. **CollisionDetector**：處理碰撞偵測邏輯
4. **TetrominoManager**：管理當前與下一個方塊，處理移動/旋轉
5. **LineClearSystem**：偵測並清除填滿的列
6. **ScoringSystem**：追蹤與計算分數
7. **LevelSystem**：根據消除列數管理等級進度
8. **GravitySystem**：控制方塊自動下落
9. **Renderer**：處理 canvas 繪製
10. **InputHandler**：處理鍵盤輸入
11. **GameStateManager**：協調遊戲狀態與主迴圈

#### 測試區塊
每個類別都包含測試區塊（用 `{}` 包裹），內含 console 日誌供驗證使用。

## 命名慣例

- **類別**：PascalCase（例如：`TetrominoManager`、`GameField`）
- **方法**：camelCase（例如：`moveDown()`、`checkCollision()`）
- **常數**：UPPER_SNAKE_CASE（例如：`FIELD_WIDTH`、`SCORE_RULES`）
- **變數**：camelCase（例如：`currentTetromino`、`lastDropTime`）

## 程式碼風格

- ES6+ 類別語法
- 所有類別與方法都有完整的 JSDoc 註解
- 描述性的變數與方法名稱
- 清楚的關注點分離，單一職責類別
- 大量繁體中文內嵌註解
