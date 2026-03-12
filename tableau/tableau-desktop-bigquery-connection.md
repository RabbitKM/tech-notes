# Tableau Desktop 新增 BigQuery 連線 & 資料來源取代
## 新增BigQuery連線

#### Step1. 在連線窗格中選取 Google BigQuery

<img src="tableau-desktop-bigquery-connection_images/image-1734579870341.png" width="80%" height="80%">

#### Step2. 選擇驗證的方式 (共2種)

<img src="tableau-desktop-bigquery-connection_images/image-1734579999407.png" width="50%" height="50%">

##### 1. 使用 OAuth 登入 (WebUI)

依照Web頁面指示，登入帳號及同意授權權限給Tableau。  
<img src="tableau-desktop-bigquery-connection_images/image-1734660205298.png" style="border: 1px solid black; vertical-align: top;" width="45%" height="45%"> 
<img src="tableau-desktop-bigquery-connection_images/image-1734660131574.png" style="border: 1px solid black; vertical-align: top;" width="50%" height="50%"> 

##### 2. 使用服務帳戶登入(JSON檔案)
> Tableau Server 2020.4.4 不支援此方法

選擇驗證用的JSON檔案登入  
<img src="tableau-desktop-bigquery-connection_images/image-1734581904242.png" width="50%" height="50%">

#### Step3. 選擇欲使用的BigQuery專案

選擇專案後即可讀取數據庫及資料表，用於後續報表設計。  
<img src="tableau-desktop-bigquery-connection_images/image-1734581150656.png" width="80%" height="80%">

<br>  

---
## 將既有資料來源取代成BigQuery

> 目前測試出兩種取代方式:
> 
> A. 在既有資料來源中 **逐一取代 table** (<span style="background-color: rgb(251, 238, 184);">如果主表為<span style="color: rgb(224, 62, 45);">自訂SQL查詢</span>則無法採用此方法</span>)  
> B. 另外新增資料來源後，使用內建工具取代 **整個資料來源**

### A. 在既有資料來源中逐一取代 table

#### step1. 開啟欲替換的資料來源頁面，點兩下邏輯資料表進入實體層頁面
邏輯層頁面  
<img src="tableau-desktop-bigquery-connection_images/image-1734660499705.png" width="80%" height="80%">  

實體層頁面  
<img src="tableau-desktop-bigquery-connection_images/image-1734661100182.png" width="80%" height="80%">

#### step2. 在左側窗格中新增BigQuery連線
<img src="tableau-desktop-bigquery-connection_images/image-1734661342234.png" width="80%" height="80%">

#### step3. 搜尋BigQuery中對應的table
<img src="tableau-desktop-bigquery-connection_images/image-1734661559640.png" width="80%" height="80%">

#### step4. 逐一替換table

##### 1. 非自訂SQL查詢 (直接 table 替換 table)
選取左側窗格 BigQuery 中 table，拖曳到右側要替換的 table 後放開，即完成取代。  

<img src="tableau-desktop-bigquery-connection_images/image-1734661949827.png" width="80%" height="80%">

##### 2. 自訂SQL查詢 (移除舊SQL查詢，重新建立SQL查詢)

* **複製既有 SQL 語法**  
  點選 table 右側小箭頭，選擇"編輯自訂SQL查詢"。  
  <img src="tableau-desktop-bigquery-connection_images/image-1734663581964.png" width="60%" height="60%">

  跳出窗格後複製 SQL 語法  
  <img src="tableau-desktop-bigquery-connection_images/image-1734663150445.png" width="60%" height="60%">

<br>

* **移除舊有table**  
  <img src="tableau-desktop-bigquery-connection_images/image-1734665703606.png" width="60%" height="60%"> 

<br>

* **重新建立 SQL 查詢**  
  左側窗格中點選"新自訂SQL"  
  <img src="tableau-desktop-bigquery-connection_images/image-1734676476518.png" width="80%" height="80%">
  <br> 
  貼上 SQL 語法並修改來源字段 (FROM ...)，加入 BigQuery 專案名稱。
  <img src="tableau-desktop-bigquery-connection_images/image-1734664165932.png" width="60%" height="60%">
  <br>  
  點選確認後即產生新的實體資料表  
  <img src="tableau-desktop-bigquery-connection_images/image-1734666185068.png" width="60%" height="60%"> 
  <br>  
  依相同條件建立資料關聯 (可另開原 tableau 檔在旁做比對)  
  <img src="tableau-desktop-bigquery-connection_images/image-1734666890627.png" width="60%" height="60%"> 

#### step5. 檢查篩選器條件是否與原本的一致
<img src="tableau-desktop-bigquery-connection_images/image-1734668093842.png" width="80%" height="80%"> 

#### step6. 移除舊連線 
<img src="tableau-desktop-bigquery-connection_images/image-1734668500932.png" width="80%" height="80%">  

<br>  
<br>  

---

### B. 另外新增資料來源後，使用內建工具取代整個資料來源

#### step1. 點選工具列中"資料"，選擇"新增資料來源"
<img src="tableau-desktop-bigquery-connection_images/image-1734676960864.png" width="60%" height="60%">  

#### step2. 新增BigQuery連線
<img src="tableau-desktop-bigquery-connection_images/image-1734677124360.png" width="80%" height="80%">  

#### step3. 依照原本串接關係，在新資料來源中創建相同的表及關聯
參考原資料來源(這裡是Hadoop)  
<img src="tableau-desktop-bigquery-connection_images/image-1734680876250.png" width="80%" height="80%">  

在新資料來源(BigQuery)中建立相同關聯  
<img src="tableau-desktop-bigquery-connection_images/image-1734681059899.png" width="80%" height="80%">  

#### step4. 新增篩選器與原有的一致
點選右上的篩選器新增  
<img src="tableau-desktop-bigquery-connection_images/image-1734681192047.png" width="80%" height="80%">  

參考原有的篩選器做配置  
<img src="tableau-desktop-bigquery-connection_images/image-1734681329675.png" width="60%" height="60%">  

#### step5. 使用內建工具取代整個資料來源
**先切換至任一工作表頁籤**，點選工具列中"資料"，選擇"取代資料來源"。  
<img src="tableau-desktop-bigquery-connection_images/image-1734681613372.png" width="60%" height="60%">  

選取欲替換的資料來源後確定  
<img src="tableau-desktop-bigquery-connection_images/image-1734681911549.png" width="60%" height="60%">  

#### step6. 移除舊資料來源
<img src="tableau-desktop-bigquery-connection_images/image-1734685053000.png" width="80%" height="80%">  

### 補充
> **重設自訂SQL查詢**，或是**替換整個資料來源**時，欄位可能會有一些細微差異 (例如: Tableau會自動產生欄位別名)，依照狀況可參考下列方法做調整嘗試。

#### 欄位名稱重設
切換至資料來源頁面，點選欲重設名稱的邏輯資料表。  
點選下方第一個欄位後按住Shift，然後滑動到最底部，滑鼠點一下最後一個欄位，即可全選欄位。(或依需要的範圍選取)  
<img src="tableau-desktop-bigquery-connection_images/image-1734683177383.png" width="50%" height="50%">  

滑鼠右鍵點選任一欄位，選擇"重設名稱"，即可將選取的欄位名稱還原成原始欄位名稱。  
<img src="tableau-desktop-bigquery-connection_images/image-1734683278165.png" width="50%" height="50%">  

#### 欄位型別更換
部分**數字**欄位在原資料來源中，維度被更換成**字串**欄位，但是透過替換整個資料來源後，可能沒有跟著變動，此時透過手動拖曳來重現。  
<img src="tableau-desktop-bigquery-connection_images/image-1734683666028.png" width="50%" height="50%">   

#### 欄位/公式異常處理
由於Tableau自動產生欄位別名，造成欄位名稱的不同，公式可能會找不到相同的欄位名稱因此報錯(顯示驚嘆號)。  
可透過右鍵欄位選擇"取代引用"，手動替換成新的正確欄位名稱。(使用相同欄位的公式會自動跟著調整)  
<img src="tableau-desktop-bigquery-connection_images/image-1734685132977.png" width="40%" height="40%"> 

## 參考資料 
* Google BigQuery - Tableau  
[https://help.tableau.com/current/pro/desktop/zh-tw/examples_googlebigquery.htm](https://help.tableau.com/current/pro/desktop/zh-tw/examples_googlebigquery.htm)  

* 取代資料來源 - Tableau  
[https://help.tableau.com/current/pro/desktop/zh-tw/connect_basic_replace.htm](https://help.tableau.com/current/pro/desktop/zh-tw/connect_basic_replace.htm)