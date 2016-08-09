<center><h1>Article Recommendation</h1></center>
----
推薦相關內容一直是我們所持續改良及關注的閱讀體驗之一，此題目為邀請所有參賽者根據個人興趣及近期瀏覽之行為，針對瀏覽者之後的行為進行預測，推薦閱讀相關內容。

訓練資料及測試資料的示意圖如下
<img width="650px" src="https://docs.google.com/drawings/d/1e1epVxq0VRVJmy2DG5TBdUp8u3ZeyK2dwSkSQch2qgc/pub?w=851&amp;h=440" />
<br>
<img width="300px" src="https://docs.google.com/drawings/d/1elJJ538OAcm3gxfyVoSoVU__1D-FQwRty1NrxmRqdR0/pub?w=455&h=100" />

### 訓練資料集
* 瀏覽紀錄
	* 資料說明: 參賽者可以利用此6個月份歷史資料集來設計推薦模型，並且資料是採樣過的。
	* Date : 2015/03 ~ 2015/08
	* [Schema Description](training_data_schema.md)
	* [Sample File](./data/sample_training.json)
	* 完整資料集會再以 Mail 通知

* 全文資料集
	* 資料說明: 此資料集之中提供這些 URL 所包含的本文資料
	* Date : 2015/03 ~ 2015/08
	* [Schema Description](article_data_schema.md)
	* [Sample File](./data/sample_article.json)
	* 完整資料集會再以 Mail 通知

### 待測使用者(Cookie)列表 
* 資料說明: 待預測的Cookie(使用者)列表，參賽者必須根據這些Cookie(使用者)的歷史閱覽紀錄，來預測會再看哪些Author(創作者)
* Date : 2015/03 ~ 2015/08
* [Schema Description](testing_data_schema.md)
* [Download Link](./data/testing.json)

## 評分方式
----
### 演算法推薦結果(70%)
* 採用 Top-N Recommendation Precision and Recall 作為指標，故採用F1 Socre來作為最終的 Score 指標
* 定義如下：
	* P : 根據過去歷史資料(訓練資料集)產生 Author(創作者) 推薦模型，再利用此模型來針對每一個 Cookie 推薦 Top-N Author 集合及為 P，而N 的大小會根據不同的使用者(Cookie) 而不同
	* R : 在測試資料集中(測試資料集) ，每一個Cookie 所瀏覽過的 Author(創作者) 集合即為 R 
	* Precsion 定義 : <img src='https://latex.codecogs.com/gif.latex?%5Cfrac%7B%5Cleft%20%7C%20P%5Ccap%20R%20%5Cright%20%7C%7D%7B%5Cleft%20%7C%20P%20%5Cright%20%7C%7D'>

	* Recall 定義 :<img src='https://latex.codecogs.com/gif.latex?%5Cfrac%7B%5Cleft%20%7C%20P%5Ccap%20R%20%5Cright%20%7C%7D%7B%5Cleft%20%7C%20R%20%5Cright%20%7C%7D'>

	* F1 Measure 定義 :<img src='https://latex.codecogs.com/gif.latex?F_1%20%3D%202000*%20%5Ccdot%20%5Cfrac%7B%5Cmathrm%7Bprecision%7D%20%5Ccdot%20%5Cmathrm%7Brecall%7D%7D%7B%5Cmathrm%7Bprecision%7D%20&plus;%20%5Cmathrm%7Brecall%7D%7D'>
	
	* 演算法推薦分數 : 採用 Min-max 標準化將 F1 Measure 進行轉換
		* H : 所有隊伍中最高分的 F1 Measure 即代表 H 
		* L : 所有隊伍中最低分的 F1 Measure 即代表 L
		* X : 某隊中所上傳中的最高 F1 Measure 即代表 X
		* <img src='https://latex.codecogs.com/gif.latex?score%20%3D%20100%5Ctimes%20%5Cfrac%7BX-L%7D%7BH-L%7D' />

* 上傳預測結果取得 F1 Score
	* [上傳格式範例檔](./data/sample_submit.json)
	* 上傳網址將於賽前公布
	* 前三名隊伍的分數將會顯示在 網站的 Leader Board 之中

### 簡報分數(30%)
* 簡報內容
* 演算法設計
* 資料解釋及分析

### 總分計算 : Final Score = (0.7 x 演算法推薦分數) + (0.3 x 簡報分數)

### 備註:
* 由於本站資料非常龐大，故抽樣部份資抖
* 為確保比賽順暢，詳細規則主辦單位保留細節微調之權利

----
### 相關參考資料
* [Large-scale Parallel Collaborative Filtering for
the Netflix Prize](http://www.grappa.univ-lille3.fr/~mary/cours/stats/centrale/reco/paper/MatrixFactorizationALS.pdf)
* [Spark Tutorial](http://spark.apache.org/docs/latest/mllib-collaborative-filtering.html#examples)
* [範例程式碼](https://github.com/pixnet/2016-pixnet-hackathon-recommendation/blob/master/Article_Recommendation_Sample_Code.ipynb)

### 說明影片
- [影片鏈結](https://youtu.be/mQz6lIZHwkA?t=15m14s)

### 小工具
* [方程式 Gif 產生器](https://www.codecogs.com/latex/eqneditor.php)
    * smaple code :`\frac{\left | P\cap R \right |}{\left | P  \right |}`
    * sample code : `F_1 = 2 \cdot \frac{\mathrm{precision} \cdot \mathrm{recall}}{\mathrm{precision} + \mathrm{recall}}`
    * sample code : `score70 = 70\times \frac{X-L}{H-L}`







