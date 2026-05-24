# Senior-project

下面是把兩件事合併後的 **BigComp short paper 最高通過率最終時程表**：

1. 原本的高通過率 BigComp short paper 進度
2. 解決 **GSE121212 只有 147 樣本** 的外部資料集補強策略

你們目前簡報已經有主資料集 GSE121212、RNA-seq、AD/PSO、LS/NL/Healthy、STAR、DESeq2、TPM、ssGSEA、免疫相關 pathway heatmap 等基礎，所以這份安排不是從零開始，而是把它推到可以投稿 short paper 的完整程度。

---

# 最終投稿策略

你們不要把目標寫成：

> 用機器學習預測皮膚病。

而要寫成：

> **An Interpretable Machine Learning Framework Integrating Immune Cell Abundance and Transcriptomic Profiles for Lesional-like Risk Stratification in Inflammatory Skin Diseases**

中文意思：

> **整合免疫細胞豐度與轉錄體資料之可解釋機器學習框架：應用於皮膚發炎疾病之病灶化風險分層**

這樣可以同時扣住：

* BigComp 的 machine learning / data analytics
* 生醫資料分析
* immune profiling
* interpretable AI
* biomarker discovery
* external validation

---

# 最終總工時建議

原本 190～220 小時偏緊。
如果要把通過率拉到最高，我建議抓：

> **240～280 小時**

原因是你們要多做：

1. 外部資料集搜尋與整理
2. cross-cohort validation
3. batch effect / platform 差異處理
4. SHAP 與 biomarker 解釋
5. leakage-free repeated CV

這些才是讓 reviewer 比較難攻擊的關鍵。

---

# 最終版每週時間表

## Phase 1：5 月中～6 月底

### 目標：把研究問題、資料、label、baseline 全部固定

這階段的重點不是衝模型，而是避免後面整篇 paper 被 reviewer 說 label 不清楚、資料洩漏、樣本太少。

| 週次     |       時間 |    工時 | 本週目標                  | 必須交出的成果                                                            |
| ------ | -------: | ----: | --------------------- | ------------------------------------------------------------------ |
| Week 1 |     5 月中 |  6 小時 | 收斂投稿故事                | 確定 title、研究問題、主任務、副任務、不可過度宣稱的地方                                    |
| Week 2 |    5 月下旬 |  8 小時 | 整理 GSE121212 metadata | 樣本表：sample ID、AD/PSO/CTRL、LS/NL/Healthy、是否可用                       |
| Week 3 |     5 月底 |  8 小時 | 建立主資料 feature matrix  | ssGSEA immune score matrix、TPM/gene matrix、combined feature matrix |
| Week 4 | 6 月第 1 週 | 10 小時 | 建立 baseline pipeline  | Logistic Regression 跑完 LS vs NL，含 stratified 5-fold CV             |
| Week 5 | 6 月第 2 週 | 10 小時 | 加入基本 ML 模型            | SVM、Random Forest、XGBoost 初版結果                                     |
| Week 6 | 6 月第 3 週 | 12 小時 | 檢查資料洩漏與 overfitting   | 確認標準化、feature selection、PCA 都只在 training fold 內做                   |
| Week 7 | 6 月第 4 週 | 14 小時 | 搜尋外部資料集               | 建立候選資料集表：GSE154200、GSE140227、GSE153007、GSE14905 等                  |

---

## Week 7 必須完成的外部資料集表

這張表非常重要，因為它是解決「147 樣本偏少」的核心。

| Dataset   | 疾病                            | LS | NL | Healthy | Platform   | 用途                                  | 優先度 |
| --------- | ----------------------------- | -: | -: | ------: | ---------- | ----------------------------------- | --: |
| GSE121212 | AD / PSO                      |  有 |  有 |       有 | RNA-seq    | 主資料集 / discovery cohort             |  最高 |
| GSE154200 | AD / PSO / eczema             |  有 |  有 |     需確認 | RNA-seq    | 外部驗證 / 可能 cross-cohort              |  最高 |
| GSE140227 | AD                            |  有 |  有 |     需確認 | RNA-seq    | AD-specific validation              |   高 |
| GSE153007 | AD / PSO / contact dermatitis |  有 |  有 |     可能有 | microarray | cross-platform signature validation |  中高 |
| GSE14905  | PSO                           |  有 |  有 |     可能無 | microarray | PSO-specific validation             |  中高 |

最推薦策略：

> **GSE121212 做主訓練與 discovery，GSE154200 做最重要的外部驗證，GSE140227 / GSE14905 / GSE153007 做 signature replication。**

---

# Phase 2：7 月

## 目標：完成可以投稿的核心實驗與外部資料初步驗證

7 月是整個計畫最關鍵的月份。
這個月結束前要知道：這篇 paper 到底能不能投 BigComp。

| 週次      |       時間 |    工時 | 本週目標                       | 必須交出的成果                                            |
| ------- | -------: | ----: | -------------------------- | -------------------------------------------------- |
| Week 8  | 7 月第 1 週 | 22 小時 | 正式重跑主任務 LS vs NL           | Logistic、SVM、RF、XGBoost、LightGBM 的正式結果             |
| Week 9  | 7 月第 2 週 | 24 小時 | 做 feature set performance and stability comparison   | ssGSEA only、gene only、combined features 的 performance、stability、external validation trend 比較表        |
| Week 10 | 7 月第 3 週 | 24 小時 | 做副任務                       | AD vs PSO、AD-LS vs PSO-LS、AD-NL vs PSO-NL          |
| Week 11 | 7 月第 4 週 | 26 小時 | 做 repeated CV / robustness | repeated 5-fold CV、多 random seed、ROC-AUC、PR-AUC、F1 |
| Week 12 |     7 月底 | 26 小時 | 做外部資料集初步驗證                 | GSE154200 或其他外部 dataset 的初版驗證結果                    |

---

## 7 月底必須鎖定的結果

到 Week 12 結束，你們至少要有：

| 成果                                         | 是否必須   |
| ------------------------------------------ | ------ |
| GSE121212 主任務 LS vs NL 模型比較表               | 必須     |
| ssGSEA / gene / combined feature 的效能、穩定性與外部驗證趨勢比較        | 必須     |
| repeated CV 平均值 ± 標準差                      | 必須     |
| ROC-AUC、PR-AUC、F1、Accuracy                 | 必須     |
| confusion matrix                           | 必須     |
| AD vs PSO 副任務結果                            | 建議必須   |
| GSE154200 外部驗證初版                           | 強烈建議必須 |
| GSE140227 / GSE14905 signature replication | 有時間再補  |

這個時間點要做一次判斷：

| 結果狀況 | 投稿故事 |
|---|---|
| LS vs NL 在 repeated CV 中表現穩定，且外部資料趨勢支持 | 主打 lesional-like immune activation classification，強調可辨識病灶樣本與非病灶樣本的免疫活化差異 |
| AD vs PSO 任務表現穩定 | 加強 disease-specific immune phenotype classification，說明 AD 與 PSO 具有不同免疫表型 |
| ssGSEA features 比 gene-only features 更穩定或更可解釋 | 主打 immune-abundance-based framework，強調免疫豐度特徵比單純基因表現更具解釋性與穩定性 |
| combined features 在 repeated CV 與外部驗證中皆表現較佳 | 主打 multi-level transcriptomic and immune-abundance profiling framework，強調結合 gene expression 與 immune signatures 可提升模型表現與泛化能力 |
| GSE154200 外部驗證成功，且 GSE140227 / GSE14905 有部分 signature replication | 主打 robust cross-cohort immune signature discovery，強調主要免疫特徵可在不同資料集中重現 |
| 外部驗證不穩，但內部 CV 與 SHAP 結果仍有合理生物意義 | 改成 exploratory short paper，誠實寫 limitation，主打初步發現與可解釋框架，不過度宣稱泛化能力 |


但 short paper 不要放太大表格：   

BigComp short paper 頁數很短，所以正式論文裡不要放我剛剛那種很大的完整表格。   
正式 paper 裡建議放簡化版：   
| Feature set | Best model | ROC-AUC | PR-AUC | F1 | Stability | External trend |
| ----------- | ---------- | ------: | -----: | -: | --------- | -------------- |
| Gene only   |            |         |        |    |           |                |
| ssGSEA only |            |         |        |    |           |                |
| Combined    |            |         |        |    |           |                |

其中：

ROC-AUC / PR-AUC / F1：放 repeated CV 的 mean ± std   
Stability：可以寫 High / Medium / Low，或用 std 表示   
External trend：寫 Consistent / Partially consistent / Not consistent   

這樣 4 頁比較塞得下。

---

# Phase 3：8 月

## 目標：把實驗結果變成一篇有說服力的 short paper

8 月的重點不是再狂加模型，而是讓 reviewer 相信：

1. 你們不是 overfitting
2. 你們不是只套模型
3. 你們的特徵有生物意義
4. 外部資料也支持你們的發現

| 週次      |       時間 |    工時 | 本週目標               | 必須交出的成果                                                    |
| ------- | -------: | ----: | ------------------ | ---------------------------------------------------------- |
| Week 13 | 8 月第 1 週 | 22 小時 | feature importance | RF / XGBoost importance、permutation importance             |
| Week 14 | 8 月第 2 週 | 24 小時 | SHAP 分析            | SHAP summary plot、top immune signatures / top genes        |
| Week 15 | 8 月第 3 週 | 24 小時 | biomarker 與免疫解釋    | top 5～10 features 的生物意義表格                                  |
| Week 16 | 8 月第 4 週 | 26 小時 | 完成外部驗證             | GSE154200 validation；GSE140227 / GSE14905 replication 視情況補 |
| Week 17 |     8 月底 | 22 小時 | 寫 paper v1         | IEEE 4 頁 short paper v1，圖表全部放入                             |

---

## 8 月底 paper v1 必須包含的圖表

4 頁 short paper 很短，所以建議最多 3 圖 + 2 表。

| 圖表       | 內容                                                       | 目的                      |
| -------- | -------------------------------------------------------- | ----------------------- |
| Figure 1 | RNA-seq → TPM → ssGSEA → ML → SHAP → biomarker framework | 讓 reviewer 一眼看懂方法       |
| Figure 2 | PCA / heatmap / immune score pattern                     | 展示 LS/NL 或 AD/PSO 的免疫差異 |
| Figure 3 | ROC curve 或 SHAP summary plot                            | 展示模型效果或可解釋性             |
| Table 1  | Dataset statistics + model performance                   | 同時處理資料與結果               |
| Table 2  | Top immune signatures / biomarkers                       | 展示生物意義                  |

如果真的塞不下，優先保留：

1. Figure 1 framework
2. Table 1 performance
3. Figure 3 SHAP 或 ROC
4. Table 2 biomarkers

---

# Phase 4：9 月

## 目標：把 paper 修到像正式 conference paper

9 月不要再做大型新實驗。
只允許小補圖、小補表、小修數字。

| 週次      |       時間 |    工時 | 本週目標                          | 必須交出的成果                                                 |
| ------- | -------: | ----: | ----------------------------- | ------------------------------------------------------- |
| Week 18 | 9 月第 1 週 | 10 小時 | 老師 / 學長姐 review               | 收到 comments，整理 revision checklist                       |
| Week 19 | 9 月第 2 週 | 12 小時 | 修 Introduction / Related Work | 20 篇左右文獻，明確寫出研究 gap                                     |
| Week 20 | 9 月第 3 週 | 12 小時 | 修 Method / Experiment         | 寫清楚 CV、feature selection、external validation、避免 leakage |
| Week 21 | 9 月第 4 週 | 12 小時 | 修 Results / Discussion        | 避免過度宣稱，補 limitation                                     |
| Week 22 |     9 月底 | 10 小時 | 壓縮成正式 4 頁                     | IEEE format v0.9，不超頁、圖表清楚、引用完整                          |

---

## 9 月最重要的寫法修正

你們一定要避免寫：

> We predict the future progression from non-lesional to lesional skin.

因為如果資料不是 longitudinal，就不能這樣說。

改成：

> We identify lesional-like immune activation patterns in non-lesional skin.

或：

> We develop an immune-abundance-based risk stratification framework for characterizing lesional-like signatures in non-lesional skin.

中文意思：

> 我們不是直接預測未來惡化，而是評估非病灶皮膚是否呈現接近病灶皮膚的免疫活化特徵。

這個修正會大幅降低被 reviewer 攻擊的風險。

---

# Phase 5：10 月上旬～10 月中

## 目標：投稿前最終檢查

| 週次      |        時間 |     工時 | 本週目標       | 必須交出的成果                                    |
| ------- | --------: | -----: | ---------- | ------------------------------------------ |
| Week 23 | 10 月第 1 週 |  10 小時 | 技術一致性檢查    | code、表格、圖、paper 數字一致                       |
| Week 24 | 10 月第 2 週 |  10 小時 | 英文、格式、匿名檢查 | double-blind、references、keywords、PDF final |
| Week 25 |     10 月中 | 6～8 小時 | 預留緊急修正與投稿  | final PDF、abstract、投稿系統資料、最後送出             |

---

# 最終研究任務優先順序

你們不要平均用力，優先順序要很清楚。

## 第一優先：LS vs NL

這是主線。
因為你們題目的核心是病灶與非病灶皮膚的免疫差異。

## 第二優先：ssGSEA immune feature 是否有用

這是你們和普通 ML 皮膚病分類最大的差異。
一定要比較：

| Feature set | 意義                  |
| ----------- | ------------------- |
| gene only   | 傳統基因表現特徵            |
| ssGSEA only | 免疫細胞 / pathway 豐度特徵 |
| combined    | 基因 + 免疫特徵           |

如果 ssGSEA only 或 combined 表現好，故事會非常漂亮。

## 第三優先：外部驗證

這是解決 147 樣本偏少的核心。
最推薦：

| 資料集       | 用途                                   |
| --------- | ------------------------------------ |
| GSE154200 | 最主要外部驗證                              |
| GSE140227 | AD-specific LS/NL validation         |
| GSE14905  | PSO-specific LS/NL validation        |
| GSE153007 | cross-platform microarray validation |

## 第四優先：SHAP / biomarker interpretation

這可以讓你們的 paper 不只是模型準確率，而是有生物意義。

---

# 最終版 4 頁 paper 架構

## Page 1

* Abstract
* Introduction
* Problem Definition
* Contributions

貢獻建議寫成 3 點：

1. 提出一個基於 immune-abundance 的可解釋 ML framework
2. 比較 gene expression、ssGSEA immune signatures、combined features 對 LS/NL 與 AD/PSO 分類的效果
3. 透過 SHAP 與外部資料集驗證，找出具生物意義的 immune signatures / biomarkers

---

## Page 2

* Dataset
* External cohorts
* Preprocessing
* ssGSEA immune profiling
* ML models
* Evaluation protocol

這頁一定要寫：

* stratified repeated 5-fold CV
* feature selection inside training folds
* no data leakage
* external validation
* metrics：ROC-AUC、PR-AUC、F1、Accuracy

---

## Page 3

* Model comparison
* Feature set comparison
* External validation
* ROC / PR curve

核心表格：

| Task | Feature set | Model | ROC-AUC | PR-AUC | F1 | Accuracy |
| ---- | ----------- | ----- | ------: | -----: | -: | -------: |

---

## Page 4

* SHAP summary
* Top immune signatures / biomarkers
* Biological interpretation
* Limitation
* Conclusion

limitation 建議誠實寫：

* sample size is limited
* retrospective public datasets
* cohort heterogeneity / batch effect
* not a longitudinal progression prediction
* clinical validation is still needed

這樣不會扣分，反而會讓 paper 比較可信。

---

# 解決 147 樣本偏少的最終方法

你們不要單純說「我們資料少」。
要改成這樣設計：

## 主設計

> GSE121212 as discovery cohort
> GSE154200 as external validation cohort
> GSE140227 and GSE14905 as disease-specific signature replication cohorts
> GSE153007 as cross-platform validation cohort if usable

也就是：

| 問題                       | 解法                                                            |
| ------------------------ | ------------------------------------------------------------- |
| GSE121212 只有 147 samples | 加外部 cohort validation                                         |
| RNA-seq feature 太多，樣本少   | 用 ssGSEA 降維成 immune signatures                                |
| overfitting 風險           | repeated CV + leakage-free pipeline                           |
| 只在單一 dataset 成立          | cross-cohort validation                                       |
| 生物意義不足                   | SHAP + biomarker / pathway interpretation                     |
| 平台差異                     | RNA-seq 用 model validation；microarray 用 signature replication |

這樣 reviewer 看到的就不是：

> 你們只有 147 samples。

而是：

> 你們有一個 discovery cohort，並且用多個 public cohorts 驗證主要 immune signatures。

這個說服力差很多。

---

# 最終通過率評估

如果你們照這份最終版完整做完，我會這樣評分：

| 完成程度                                          | BigComp short paper 通過率評分 |
| --------------------------------------------- | ------------------------: |
| 只完成 GSE121212 + 基本 ML                         |                  6.5～7/10 |
| 完成 GSE121212 + repeated CV + SHAP             |                  7.5～8/10 |
| 加上 GSE154200 外部驗證                             |                  8～8.3/10 |
| 再加 GSE140227 / GSE14905 signature replication |                8.3～8.5/10 |
| 圖表漂亮、story 清楚、limitation 嚴謹                   |             **8.5/10 左右** |

我不會說 100% 穩過，因為 conference review 本來就有不確定性，而且 BigComp 不是純醫療 AI 會議。
但如果你們真的照這份做完，你們會從：

> 可以挑戰 BigComp short paper

提升到：

> **有明顯競爭力，而且被接受不意外。**

---

# 最終一句話版本

你們最高通過率的做法是：

> **用 GSE121212 做主實驗，不硬說預測未來惡化；改成 lesional-like immune activation risk stratification。7 月完成 ML + repeated CV，8 月完成 SHAP + GSE154200 外部驗證，9 月只修 paper，並用 GSE140227 / GSE14905 補強 AD/PSO signature replication。**

這樣是目前你們這個題目衝 BigComp short paper 最穩、最合理、最能防 reviewer 攻擊的安排。
