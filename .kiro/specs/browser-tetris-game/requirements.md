# 需求文件

## 簡介

瀏覽器俄羅斯方塊遊戲是一個使用單一 HTML 檔案實作的經典俄羅斯方塊遊戲，僅使用原生 JavaScript 與 CSS，不依賴任何外部套件。玩家透過鍵盤操作控制下落的四方塊，目標是消除填滿的列以獲得分數，隨著遊戲進行難度會逐漸提升。

## 範圍外

以下功能明確不在此規格書範圍內：

- **持有棋子（Hold piece）**: 不支援暫存當前四方塊以供稍後使用的功能
- **幽靈棋子（Ghost piece）**: 不顯示四方塊落地位置的半透明預覽
- **多人遊戲**: 不支援多人對戰或協作模式
- **手機觸控操作**: 僅支援鍵盤操作，不提供觸控螢幕控制介面

## 術語表

- **遊戲場地（Game_Field）**: 10 欄 × 20 列的遊戲區域
- **四方塊（Tetromino）**: 由 4 個方格組成的遊戲方塊
- **重力系統（Gravity_System）**: 控制四方塊自動下落的機制
- **消行系統（Line_Clear_System）**: 偵測並移除已填滿列的機制
- **計分系統（Scoring_System）**: 計算玩家分數的機制
- **等級系統（Level_System）**: 根據消除行數調整遊戲速度的機制
- **碰撞偵測器（Collision_Detector）**: 偵測四方塊是否與場地邊界或其他方塊碰撞的機制
- **輸入處理器（Input_Handler）**: 處理鍵盤輸入的機制
- **遊戲狀態管理器（Game_State_Manager）**: 管理遊戲狀態（進行中、暫停、結束）的機制
- **渲染器（Renderer）**: 將遊戲狀態繪製到畫面的機制

## 需求

### 需求 1：遊戲場地初始化

**使用者故事：** 作為玩家，我希望遊戲有標準的遊戲場地，以便進行俄羅斯方塊遊戲。

#### 驗收標準

1. THE Game_Field SHALL 包含 10 欄
2. THE Game_Field SHALL 包含 20 列
3. WHEN 遊戲開始時，THE Game_Field SHALL 為空白狀態

### 需求 2：四方塊類型

**使用者故事：** 作為玩家，我希望遊戲包含所有標準四方塊類型，以便體驗完整的俄羅斯方塊遊戲。

#### 驗收標準

1. THE 遊戲 SHALL 支援 I 型四方塊（4 格直線）
2. THE 遊戲 SHALL 支援 O 型四方塊（2×2 正方形）
3. THE 遊戲 SHALL 支援 T 型四方塊（T 字形）
4. THE 遊戲 SHALL 支援 S 型四方塊（S 字形）
5. THE 遊戲 SHALL 支援 Z 型四方塊（Z 字形）
6. THE 遊戲 SHALL 支援 J 型四方塊（J 字形）
7. THE 遊戲 SHALL 支援 L 型四方塊（L 字形）
8. WHEN 新四方塊生成時，THE 遊戲 SHALL 從 7 種類型中隨機選擇一種

### 需求 3：四方塊生成

**使用者故事：** 作為玩家，我希望四方塊能正確生成在場地頂端，以便開始操作。

#### 驗收標準

1. WHEN 遊戲開始或前一個四方塊固定後，THE 遊戲 SHALL 在場地頂端中央生成新四方塊
2. WHEN 新四方塊生成時，THE 遊戲 SHALL 顯示下一個四方塊的預覽
3. IF 新四方塊生成位置已被佔據，THEN THE Game_State_Manager SHALL 觸發遊戲結束

### 需求 4：鍵盤操作 - 左右移動

**使用者故事：** 作為玩家，我希望能用左右鍵移動四方塊，以便調整其水平位置。

#### 驗收標準

1. WHEN 玩家按下左方向鍵，THE Input_Handler SHALL 將當前四方塊向左移動一格
2. WHEN 玩家按下右方向鍵，THE Input_Handler SHALL 將當前四方塊向右移動一格
3. IF 移動後會與場地邊界碰撞，THEN THE Collision_Detector SHALL 阻止移動
4. IF 移動後會與已固定方塊碰撞，THEN THE Collision_Detector SHALL 阻止移動

### 需求 5：鍵盤操作 - 旋轉

**使用者故事：** 作為玩家，我希望能用上鍵旋轉四方塊，以便調整其方向。

#### 驗收標準

1. WHEN 玩家按下上方向鍵，THE Input_Handler SHALL 將當前四方塊順時針旋轉 90 度
2. IF 旋轉後會與場地邊界碰撞，THEN THE Collision_Detector SHALL 阻止旋轉
3. IF 旋轉後會與已固定方塊碰撞，THEN THE Collision_Detector SHALL 阻止旋轉
4. THE O 型四方塊 SHALL 在旋轉時保持相同形狀

### 需求 6：鍵盤操作 - 緩降

**使用者故事：** 作為玩家，我希望能用下鍵加速四方塊下落，以便更快地放置方塊。

#### 驗收標準

1. WHEN 玩家按下下方向鍵，THE Input_Handler SHALL 將當前四方塊向下移動一格
2. WHEN 玩家按下下方向鍵使四方塊下移，THE Scoring_System SHALL 增加 1 分
3. IF 向下移動會導致碰撞，THEN THE 遊戲 SHALL 固定當前四方塊

### 需求 7：鍵盤操作 - 瞬降

**使用者故事：** 作為玩家，我希望能用空白鍵瞬間將四方塊降到底部，以便快速放置方塊。

#### 驗收標準

1. WHEN 玩家按下空白鍵，THE Input_Handler SHALL 將當前四方塊移動到最低可能位置
2. WHEN 瞬降完成後，THE 遊戲 SHALL 立即固定該四方塊
3. WHEN 瞬降完成後，THE Scoring_System SHALL 增加分數，分數等於下降的格數乘以 2

### 需求 8：重力系統

**使用者故事：** 作為玩家，我希望四方塊能自動下落，以便遊戲持續進行。

#### 驗收標準

1. WHILE 遊戲進行中，THE Gravity_System SHALL 定期將當前四方塊向下移動一格
2. WHEN 等級為 N，THE Gravity_System SHALL 每 (1000 - N × 100) 毫秒執行一次下落，最小間隔為 100 毫秒
3. IF 四方塊無法繼續下落，THEN THE 遊戲 SHALL 固定該四方塊並生成新四方塊

### 需求 9：消行系統

**使用者故事：** 作為玩家，我希望填滿的列能被消除，以便騰出空間繼續遊戲。

#### 驗收標準

1. WHEN 四方塊固定後，THE Line_Clear_System SHALL 檢查是否有完全填滿的列
2. WHEN 偵測到填滿的列，THE Line_Clear_System SHALL 移除該列
3. WHEN 列被移除後，THE Line_Clear_System SHALL 將該列上方的所有列向下移動一格
4. THE Line_Clear_System SHALL 在單次固定中同時處理多個填滿的列

### 需求 10：計分系統

**使用者故事：** 作為玩家，我希望消除列時能獲得分數，以便追蹤我的遊戲表現。

#### 驗收標準

1. WHEN 玩家同時消除 1 列，THE Scoring_System SHALL 增加 100 分
2. WHEN 玩家同時消除 2 列，THE Scoring_System SHALL 增加 300 分
3. WHEN 玩家同時消除 3 列，THE Scoring_System SHALL 增加 500 分
4. WHEN 玩家同時消除 4 列，THE Scoring_System SHALL 增加 800 分
5. THE Scoring_System SHALL 在畫面上即時顯示當前分數

### 需求 11：等級系統

**使用者故事：** 作為玩家，我希望遊戲難度隨著進度提升，以便保持挑戰性。

#### 驗收標準

1. WHEN 遊戲開始時，THE Level_System SHALL 將等級設為 1
2. WHEN 玩家累計消除 10 列，THE Level_System SHALL 將等級提升 1
3. WHEN 等級提升時，THE Gravity_System SHALL 增加四方塊下落速度
4. THE Level_System SHALL 在畫面上即時顯示當前等級

### 需求 12：下一個方塊預覽

**使用者故事：** 作為玩家，我希望能預覽下一個四方塊，以便規劃策略。

#### 驗收標準

1. THE Renderer SHALL 在遊戲場地旁顯示下一個四方塊的預覽區域
2. WHEN 新四方塊生成時，THE 遊戲 SHALL 更新預覽區域顯示下一個四方塊
3. THE 預覽區域 SHALL 顯示四方塊的形狀和顏色

### 需求 13：遊戲結束條件

**使用者故事：** 作為玩家，我希望當無法繼續遊戲時能明確知道遊戲已結束，以便決定是否重新開始。

#### 驗收標準

1. WHEN 新四方塊無法在生成位置放置時，THE Game_State_Manager SHALL 將遊戲狀態設為結束
2. WHEN 遊戲結束時，THE Gravity_System SHALL 停止四方塊下落
3. WHEN 遊戲結束時，THE Input_Handler SHALL 停止接受移動和旋轉輸入
4. WHEN 遊戲結束時，THE Renderer SHALL 顯示「遊戲結束」訊息和最終分數

### 需求 14：遊戲控制按鈕

**使用者故事：** 作為玩家，我希望能透過按鈕開始和重新開始遊戲，以便控制遊戲流程。

#### 驗收標準

1. THE 遊戲介面 SHALL 提供「開始遊戲」按鈕
2. THE 遊戲介面 SHALL 提供「重新開始」按鈕
3. WHEN 玩家點擊「開始遊戲」按鈕，THE Game_State_Manager SHALL 初始化遊戲並開始
4. WHEN 玩家點擊「重新開始」按鈕，THE Game_State_Manager SHALL 重置遊戲狀態並重新開始
5. WHEN 重新開始時，THE Scoring_System SHALL 將分數重置為 0
6. WHEN 重新開始時，THE Level_System SHALL 將等級重置為 1
7. WHEN 重新開始時，THE Game_Field SHALL 清空所有已固定方塊

### 需求 15：單一檔案實作

**使用者故事：** 作為使用者，我希望遊戲能在單一 HTML 檔案中執行，以便輕鬆分享和部署。

#### 驗收標準

1. THE 遊戲 SHALL 包含在單一 HTML 檔案中
2. THE 遊戲 SHALL 僅使用原生 JavaScript
3. THE 遊戲 SHALL 僅使用原生 CSS
4. THE 遊戲 SHALL NOT 依賴任何外部 JavaScript 函式庫或框架
5. THE 遊戲 SHALL NOT 依賴任何外部 CSS 框架
6. WHEN 在現代瀏覽器中開啟 HTML 檔案時，THE 遊戲 SHALL 能正常執行

### 需求 16：使用者介面語言

**使用者故事：** 作為台灣玩家，我希望遊戲介面使用繁體中文，以便更容易理解。

#### 驗收標準

1. THE 遊戲介面 SHALL 使用繁體中文顯示所有文字
2. THE 按鈕標籤 SHALL 使用繁體中文
3. THE 遊戲狀態訊息 SHALL 使用繁體中文
4. THE 分數和等級標籤 SHALL 使用繁體中文

### 需求 17：視覺呈現

**使用者故事：** 作為玩家，我希望遊戲有清晰的視覺呈現，以便輕鬆辨識遊戲元素。

#### 驗收標準

1. THE Renderer SHALL 為每種四方塊類型使用不同顏色
2. THE Renderer SHALL 在遊戲場地中繪製網格線
3. THE Renderer SHALL 清楚區分當前下落的四方塊與已固定的方塊
4. THE Renderer SHALL 在畫面上顯示分數、等級和下一個方塊預覽
5. WHEN 列被消除時，THE Renderer SHALL 提供視覺回饋效果
