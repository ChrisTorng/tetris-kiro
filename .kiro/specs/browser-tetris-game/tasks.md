# 實作計畫：瀏覽器俄羅斯方塊遊戲

## 概述

本實作計畫將瀏覽器俄羅斯方塊遊戲分解為漸進式的開發任務。遊戲使用單一 HTML 檔案實作，包含原生 JavaScript 與 CSS，不依賴任何外部套件。實作順序從核心資料結構開始，逐步建立遊戲邏輯、輸入處理、渲染系統，最後整合所有元件。

## 任務清單

- [x] 1. 建立 HTML 檔案結構與基礎樣式
  - 建立 `tetris.html` 檔案，包含 HTML 結構、CSS 樣式區塊和 JavaScript 區塊
  - 定義 Canvas 元素用於遊戲場地渲染
  - 定義下一個方塊預覽的 Canvas 元素
  - 建立分數、等級顯示區域（使用繁體中文標籤）
  - 建立「開始遊戲」和「重新開始」按鈕（繁體中文）
  - 建立遊戲結束訊息顯示區域
  - 加入基礎 CSS 樣式：版面配置、按鈕樣式、Canvas 邊框
  - _需求：1.1, 1.2, 12.1, 14.1, 14.2, 16.1, 16.2, 16.4, 17.4_

- [x] 2. 實作四方塊資料結構與常數定義
  - [x] 2.1 定義四方塊形狀常數
    - 定義 `SHAPES` 物件，包含 7 種四方塊類型（I, O, T, S, Z, J, L）
    - 每種類型包含 4 個旋轉狀態的二維陣列
    - _需求：2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 2.7_

  - [x] 2.2 定義四方塊顏色常數
    - 定義 `COLORS` 物件，為每種四方塊類型指定顏色
    - _需求：17.1_

  - [x] 2.3 定義遊戲常數
    - 定義場地寬度（10）和高度（20）
    - 定義計分規則常數（消行分數、緩降、瞬降）
    - 定義按鍵映射常數
    - _需求：1.1, 1.2, 10.1, 10.2, 10.3, 10.4, 6.2, 7.3_

- [x] 3. 實作 Tetromino 類別
  - [x] 3.1 實作 Tetromino 建構子與基本方法
    - 實作 `constructor(type, x, y)` 初始化四方塊類型、位置、旋轉狀態
    - 實作 `getType()`, `getColor()`, `getPosition()`, `setPosition(x, y)` 方法
    - 實作 `getShape()` 方法返回當前旋轉狀態的形狀
    - _需求：2.1-2.7, 3.1_

  - [x] 3.2 實作 Tetromino 旋轉邏輯
    - 實作 `rotate()` 方法，順時針旋轉 90 度（更新旋轉狀態索引）
    - 確保 O 型四方塊旋轉後保持相同形狀
    - _需求：5.1, 5.4_

  - [x] 3.3 實作 Tetromino 方塊座標計算
    - 實作 `getBlocks()` 方法，返回所有方塊的絕對座標陣列
    - 根據形狀二維陣列和位置計算每個方塊的 (x, y) 座標
    - _需求：3.1, 4.1, 4.2_

- [x] 4. 實作 GameField 類別
  - [x] 4.1 實作 GameField 建構子與初始化
    - 實作 `constructor(width, height)` 建立二維陣列
    - 實作 `clear()` 方法清空場地（所有格子設為 null）
    - _需求：1.1, 1.2, 1.3, 14.7_

  - [x] 4.2 實作 GameField 查詢與更新方法
    - 實作 `isOccupied(x, y)` 檢查位置是否被佔據
    - 實作 `setCell(x, y, color)` 設定格子顏色
    - 實作 `getCell(x, y)` 取得格子顏色
    - 實作 `getWidth()`, `getHeight()` 取得場地尺寸
    - _需求：1.1, 1.2, 9.1_

  - [x] 4.3 實作 GameField 列操作方法
    - 實作 `isRowFull(row)` 檢查列是否完全填滿
    - 實作 `clearRow(row)` 清除列（設為 null）
    - 實作 `moveRowDown(row)` 將指定列向下移動一格
    - _需求：9.1, 9.2, 9.3_

- [x] 5. 實作 CollisionDetector 類別
  - 實作 `constructor(gameField)` 儲存場地參考
  - 實作 `checkCollision(tetromino)` 檢查四方塊是否與邊界或已固定方塊碰撞
  - 實作 `canMove(tetromino, dx, dy)` 檢查移動後是否會碰撞
  - 實作 `canRotate(tetromino, newShape)` 檢查旋轉後是否會碰撞
  - 碰撞檢查邏輯：遍歷四方塊所有方塊座標，檢查是否超出邊界或與已佔據格子重疊
  - _需求：4.3, 4.4, 5.2, 5.3, 6.3_

- [x] 6. 實作 TetrominoManager 類別
  - [x] 6.1 實作 TetrominoManager 建構子與四方塊生成
    - 實作 `constructor(gameField)` 儲存場地參考和碰撞偵測器
    - 實作 `generateNext()` 隨機生成下一個四方塊類型
    - 實作 `spawnNew()` 在場地頂端中央生成新四方塊
    - 檢查生成位置是否被佔據，若是則返回失敗狀態
    - _需求：2.8, 3.1, 3.2, 3.3_

  - [x] 6.2 實作 TetrominoManager 移動方法
    - 實作 `moveLeft()` 向左移動（使用碰撞偵測）
    - 實作 `moveRight()` 向右移動（使用碰撞偵測）
    - 實作 `moveDown()` 向下移動（使用碰撞偵測），返回是否成功
    - _需求：4.1, 4.2, 4.3, 4.4, 6.1, 6.3_

  - [x] 6.3 實作 TetrominoManager 旋轉與瞬降
    - 實作 `rotate()` 順時針旋轉（使用碰撞偵測）
    - 實作 `hardDrop()` 瞬降到最低位置，返回下降格數
    - _需求：5.1, 5.2, 5.3, 7.1, 7.2_

  - [x] 6.4 實作 TetrominoManager 固定方法
    - 實作 `lock()` 將當前四方塊固定到場地
    - 遍歷四方塊所有方塊，將顏色寫入場地對應位置
    - _需求：6.3, 8.3_

  - [x] 6.5 實作 TetrominoManager 查詢方法
    - 實作 `getCurrent()` 取得當前四方塊
    - 實作 `getNext()` 取得下一個四方塊
    - _需求：3.2, 12.2_

- [x] 7. 實作 LineClearSystem 類別
  - 實作 `constructor(gameField)` 儲存場地參考
  - 實作 `checkAndClear()` 檢查並清除所有填滿的列
  - 從底部向上掃描，找出所有填滿的列
  - 清除填滿的列，將上方列向下移動
  - 實作 `getLastClearedCount()` 返回上次清除的列數
  - _需求：9.1, 9.2, 9.3, 9.4_

- [x] 8. 實作 ScoringSystem 類別
  - 實作 `constructor()` 初始化分數為 0
  - 實作 `reset()` 重置分數為 0
  - 實作 `addSoftDrop()` 緩降加 1 分
  - 實作 `addHardDrop(distance)` 瞬降加分（距離 × 2）
  - 實作 `addLineClear(lines)` 根據消除列數加分（1/2/3/4 列對應 100/300/500/800 分）
  - 實作 `getScore()` 取得當前分數
  - _需求：6.2, 7.3, 10.1, 10.2, 10.3, 10.4, 14.5_

- [x] 9. 實作 LevelSystem 類別
  - 實作 `constructor()` 初始化等級為 1，累計消除列數為 0
  - 實作 `reset()` 重置等級為 1，累計消除列數為 0
  - 實作 `addClearedLines(count)` 增加累計消除列數，並計算新等級
  - 等級計算：`Math.floor(totalLines / 10) + 1`
  - 實作 `getLevel()` 取得當前等級
  - 實作 `getTotalLines()` 取得累計消除列數
  - _需求：11.1, 11.2, 14.6_

- [x] 10. 實作 GravitySystem 類別
  - 實作 `constructor(tetrominoManager, levelSystem)` 儲存參考
  - 實作 `start()` 啟動重力計時器
  - 實作 `stop()` 停止重力計時器
  - 實作 `update()` 由遊戲循環呼叫，檢查是否該執行下落
  - 實作 `getInterval()` 根據等級計算下落間隔：`Math.max(100, 1000 - level * 100)`
  - 定期呼叫 `tetrominoManager.moveDown()`，若失敗則觸發固定
  - _需求：8.1, 8.2, 8.3, 11.3_

- [ ] 11. 實作 Renderer 類別
  - [x] 11.1 實作 Renderer 建構子與基礎設定
    - 實作 `constructor(canvas, nextCanvas, gameField, tetrominoManager, scoringSystem, levelSystem)`
    - 取得 Canvas 2D 繪圖上下文
    - 定義格子大小、顏色常數
    - _需求：17.1, 17.2, 17.4_

  - [x] 11.2 實作場地與四方塊渲染
    - 實作 `renderField()` 繪製遊戲場地網格線和已固定方塊
    - 實作 `renderTetromino()` 繪製當前下落的四方塊
    - 使用不同視覺效果區分當前四方塊與已固定方塊
    - _需求：17.1, 17.2, 17.3_

  - [x] 11.3 實作資訊顯示渲染
    - 實作 `renderNextPreview()` 在預覽 Canvas 繪製下一個四方塊
    - 實作 `renderScore()` 更新分數顯示元素（繁體中文標籤）
    - 實作 `renderLevel()` 更新等級顯示元素（繁體中文標籤）
    - _需求：10.5, 11.4, 12.1, 12.2, 12.3, 16.4_

  - [x] 11.4 實作遊戲狀態渲染
    - 實作 `renderGameOver()` 顯示遊戲結束訊息和最終分數（繁體中文）
    - 實作 `renderLineClearEffect()` 顯示消行視覺回饋效果
    - 實作 `render()` 主渲染方法，協調所有渲染子方法
    - _需求：13.4, 16.3, 17.5_

- [x] 12. 實作 InputHandler 類別
  - 實作 `constructor(tetrominoManager, gameStateManager)` 儲存參考
  - 實作 `enable()` 啟用鍵盤事件監聽
  - 實作 `disable()` 停用鍵盤事件監聽
  - 實作 `handleKeyDown(event)` 處理按鍵事件
  - 按鍵映射：左鍵→moveLeft, 右鍵→moveRight, 下鍵→moveDown+addSoftDrop, 上鍵→rotate, 空白鍵→hardDrop+addHardDrop
  - _需求：4.1, 4.2, 5.1, 6.1, 7.1, 13.3_

- [ ] 13. 實作 GameStateManager 類別
  - [x] 13.1 實作 GameStateManager 建構子與初始化
    - 實作 `constructor()` 建立所有子系統實例
    - 建立 GameField, TetrominoManager, CollisionDetector, GravitySystem, LineClearSystem, ScoringSystem, LevelSystem, Renderer, InputHandler
    - 初始化遊戲狀態為 'idle'
    - _需求：1.3, 11.1, 14.3_

  - [x] 13.2 實作遊戲控制方法
    - 實作 `init()` 初始化遊戲（清空場地、重置分數等級、生成第一個四方塊）
    - 實作 `start()` 開始遊戲（設定狀態為 'playing'、啟動重力、啟用輸入）
    - 實作 `restart()` 重新開始（呼叫 init 和 start）
    - 實作 `gameOver()` 觸發遊戲結束（設定狀態為 'gameover'、停止重力、停用輸入）
    - 實作 `getState()` 取得當前狀態
    - _需求：13.1, 13.2, 13.3, 14.3, 14.4, 14.5, 14.6, 14.7_

  - [x] 13.3 實作遊戲循環
    - 實作 `update()` 遊戲循環主方法
    - 更新重力系統
    - 檢查四方塊是否需要固定
    - 固定後執行消行檢查、更新分數等級、生成新四方塊
    - 檢查新四方塊是否能生成，若否則觸發遊戲結束
    - 呼叫渲染器更新畫面
    - 使用 `requestAnimationFrame` 持續呼叫 update
    - _需求：3.3, 6.3, 8.3, 9.1, 9.2, 9.3, 11.2_

- [x] 14. 整合與事件綁定
  - 在 HTML 載入完成後（DOMContentLoaded）建立 GameStateManager 實例
  - 綁定「開始遊戲」按鈕點擊事件到 `gameStateManager.start()`
  - 綁定「重新開始」按鈕點擊事件到 `gameStateManager.restart()`
  - 啟動遊戲循環（呼叫 `gameStateManager.update()`）
  - _需求：14.1, 14.2, 14.3, 14.4, 15.1, 15.2, 15.3, 15.6_

- [x] 15. 最終檢查點 - 確保所有功能正常運作
  - 在現代瀏覽器中開啟 `tetris.html` 檔案
  - 驗證所有需求功能：場地初始化、四方塊生成、鍵盤操作、重力系統、消行計分、等級提升、遊戲結束、介面語言
  - 確認單一檔案實作（無外部依賴）
  - 確認所有文字使用繁體中文
  - 如有問題請詢問使用者

## 注意事項

- 所有任務專注於編寫、修改或測試程式碼
- 每個任務都參照特定需求以確保可追溯性
- 實作順序從核心資料結構到遊戲邏輯，最後整合所有元件
- 使用原生 JavaScript 和 CSS，不依賴任何外部套件
- 所有使用者介面文字使用繁體中文
