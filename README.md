# Senior-project-1

下面是把兩件事合併後的 BigComp short paper 最高通過率最終時程表：
原本的高通過率 BigComp short paper 進度
解決 GSE121212 只有 147 樣本 的外部資料集補強策略
你們目前簡報已經有主資料集 GSE121212、RNA-seq、AD/PSO、LS/NL/Healthy、STAR、DESeq2、TPM、ssGSEA、免疫相關 pathway heatmap 等基礎，所以這份安排不是從零開始，而是把它推到可以投稿 short paper 的完整程度。
最終投稿策略
你們不要把目標寫成：
用機器學習預測皮膚病。
而要寫成：
An Interpretable Immune-Abundance-Based Machine Learning Framework for Lesional-like Risk Stratification in Atopic Dermatitis and Psoriasis
中文意思：
基於免疫細胞豐度的可解釋機器學習框架，用於異位性皮膚炎與乾癬之病灶化免疫風險分層。
這樣可以同時扣住：
BigComp 的 machine learning / data analytics
生醫資料分析
immune profiling
interpretable AI
biomarker discovery
external validation
最終總工時建議
原本 190～220 小時偏緊。
如果要把通過率拉到最高，我建議抓：
240～280 小時
原因是你們要多做：
外部資料集搜尋與整理
cross-cohort validation
batch effect / platform 差異處理
SHAP 與 biomarker 解釋
leakage-free repeated CV
這些才是讓 reviewer 比較難攻擊的關鍵。
最終版每週時間表
Phase 1：5 月中～6 月底
目標：把研究問題、資料、label、baseline 全部固定
這階段的重點不是衝模型，而是避免後面整篇 paper 被 reviewer 說 label 不清楚、資料洩漏、樣本太少。
週次時間工時本週目標必須交出的成果Week 15 月中6 小時收斂投稿故事確定 title、研究問題、主任務、副任務、不可過度宣稱的地方Week 25 月下旬8 小時整理 GSE121212 metadata樣本表：sample ID、AD/PSO/CTRL、LS/NL/Healthy、是否可用Week 35 月底8 小時建立主資料 feature matrixssGSEA immune score matrix、TPM/gene matrix、combined feature matrixWeek 46 月第 1 週10 小時建立 baseline pipelineLogistic Regression 跑完 LS vs NL，含 stratified 5-fold CVWeek 56 月第 2 週10 小時加入基本 ML 模型SVM、Random Forest、XGBoost 初版結果Week 66 月第 3 週12 小時檢查資料洩漏與 overfitting確認標準化、feature selection、PCA 都只在 training fold 內做Week 76 月第 4 週14 小時搜尋外部資料集建立候選資料集表：GSE154200、GSE140227、GSE153007、GSE14905 等Week 7 必須完成的外部資料集表
這張表非常重要，因為它是解決「147 樣本偏少」的核心。
Dataset疾病LSNLHealthyPlatform用途優先度GSE121212AD / PSO有有有RNA-seq主資料集 / discovery cohort最高GSE154200AD / PSO / eczema有有需確認RNA-seq外部驗證 / 可能 cross-cohort最高GSE140227AD有有需確認RNA-seqAD-specific validation高GSE153007AD / PSO / contact dermatitis有有可能有microarraycross-platform signature validation中高GSE14905PSO有有可能無microarrayPSO-specific validation中高
最推薦策略：
GSE121212 做主訓練與 discovery，GSE154200 做最重要的外部驗證，GSE140227 / GSE14905 / GSE153007 做 signature replication。
Phase 2：7 月
目標：完成可以投稿的核心實驗與外部資料初步驗證
7 月是整個計畫最關鍵的月份。
這個月結束前要知道：這篇 paper 到底能不能投 BigComp。
週次時間工時本週目標必須交出的成果Week 87 月第 1 週22 小時正式重跑主任務 LS vs NLLogistic、SVM、RF、XGBoost、LightGBM 的正式結果Week 97 月第 2 週24 小時做 feature set comparisonssGSEA only、gene only、combined features 比較表Week 107 月第 3 週24 小時做副任務AD vs PSO、AD-LS vs PSO-LS、AD-NL vs PSO-NLWeek 117 月第 4 週26 小時做 repeated CV / robustnessrepeated 5-fold CV、多 random seed、ROC-AUC、PR-AUC、F1Week 127 月底26 小時做外部資料集初步驗證GSE154200 或其他外部 dataset 的初版驗證結果7 月底必須鎖定的結果
到 Week 12 結束，你們至少要有：
成果是否必須GSE121212 主任務 LS vs NL 模型比較表必須ssGSEA / gene / combined feature 比較必須repeated CV 平均值 ± 標準差必須ROC-AUC、PR-AUC、F1、Accuracy必須confusion matrix必須AD vs PSO 副任務結果建議必須GSE154200 外部驗證初版強烈建議必須GSE140227 / GSE14905 signature replication有時間再補
這個時間點要做一次判斷：
結果狀況投稿故事LS vs NL 很好主打 lesional-like immune activation classificationAD vs PSO 很好加強 disease-specific immune phenotype classificationssGSEA 比 gene only 更穩主打 immune-abundance frameworkcombined features 最好主打 multi-level transcriptomic + immune profiling外部驗證成功主打 robust cross-cohort immune signature外部驗證不穩改成 exploratory short paper，誠實寫 limitationPhase 3：8 月
目標：把實驗結果變成一篇有說服力的 short paper
8 月的重點不是再狂加模型，而是讓 reviewer 相信：
你們不是 overfitting
你們不是只套模型
你們的特徵有生物意義
外部資料也支持你們的發現
週次時間工時本週目標必須交出的成果Week 138 月第 1 週22 小時feature importanceRF / XGBoost importance、permutation importanceWeek 148 月第 2 週24 小時SHAP 分析SHAP summary plot、top immune signatures / top genesWeek 158 月第 3 週24 小時biomarker 與免疫解釋top 5～10 features 的生物意義表格Week 168 月第 4 週26 小時完成外部驗證GSE154200 validation；GSE140227 / GSE14905 replication 視情況補Week 178 月底22 小時寫 paper v1IEEE 4 頁 short paper v1，圖表全部放入8 月底 paper v1 必須包含的圖表
4 頁 short paper 很短，所以建議最多 3 圖 + 2 表。
圖表內容目的Figure 1RNA-seq → TPM → ssGSEA → ML → SHAP → biomarker framework讓 reviewer 一眼看懂方法Figure 2PCA / heatmap / immune score pattern展示 LS/NL 或 AD/PSO 的免疫差異Figure 3ROC curve 或 SHAP summary plot展示模型效果或可解釋性Table 1Dataset statistics + model performance同時處理資料與結果Table 2Top immune signatures / biomarkers展示生物意義
如果真的塞不下，優先保留：
Figure 1 framework
Table 1 performance
Figure 3 SHAP 或 ROC
Table 2 biomarkers
Phase 4：9 月
目標：把 paper 修到像正式 conference paper
9 月不要再做大型新實驗。
只允許小補圖、小補表、小修數字。
週次時間工時本週目標必須交出的成果Week 189 月第 1 週10 小時老師 / 學長姐 review收到 comments，整理 revision checklistWeek 199 月第 2 週12 小時修 Introduction / Related Work20 篇左右文獻，明確寫出研究 gapWeek 209 月第 3 週12 小時修 Method / Experiment寫清楚 CV、feature selection、external validation、避免 leakageWeek 219 月第 4 週12 小時修 Results / Discussion避免過度宣稱，補 limitationWeek 229 月底10 小時壓縮成正式 4 頁IEEE format v0.9，不超頁、圖表清楚、引用完整9 月最重要的寫法修正
你們一定要避免寫：
We predict the future progression from non-lesional to lesional skin.
因為如果資料不是 longitudinal，就不能這樣說。
改成：
We identify lesional-like immune activation patterns in non-lesional skin.
或：
We develop an immune-abundance-based risk stratification framework for characterizing lesional-like signatures in non-lesional skin.
中文意思：
我們不是直接預測未來惡化，而是評估非病灶皮膚是否呈現接近病灶皮膚的免疫活化特徵。
這個修正會大幅降低被 reviewer 攻擊的風險。
Phase 5：10 月上旬～10 月中
目標：投稿前最終檢查
週次時間工時本週目標必須交出的成果Week 2310 月第 1 週10 小時技術一致性檢查code、表格、圖、paper 數字一致Week 2410 月第 2 週10 小時英文、格式、匿名檢查double-blind、references、keywords、PDF finalWeek 2510 月中6～8 小時預留緊急修正與投稿final PDF、abstract、投稿系統資料、最後送出最終研究任務優先順序
你們不要平均用力，優先順序要很清楚。
第一優先：LS vs NL
這是主線。
因為你們題目的核心是病灶與非病灶皮膚的免疫差異。
第二優先：ssGSEA immune feature 是否有用
這是你們和普通 ML 皮膚病分類最大的差異。
一定要比較：
Feature set意義gene only傳統基因表現特徵ssGSEA only免疫細胞 / pathway 豐度特徵combined基因 + 免疫特徵
如果 ssGSEA only 或 combined 表現好，故事會非常漂亮。
第三優先：外部驗證
這是解決 147 樣本偏少的核心。
最推薦：
資料集用途GSE154200最主要外部驗證GSE140227AD-specific LS/NL validationGSE14905PSO-specific LS/NL validationGSE153007cross-platform microarray validation
第四優先：SHAP / biomarker interpretation
這可以讓你們的 paper 不只是模型準確率，而是有生物意義。
最終版 4 頁 paper 架構
Page 1
Abstract
Introduction
Problem Definition
Contributions
貢獻建議寫成 3 點：
提出一個基於 immune-abundance 的可解釋 ML framework
比較 gene expression、ssGSEA immune signatures、combined features 對 LS/NL 與 AD/PSO 分類的效果
透過 SHAP 與外部資料集驗證，找出具生物意義的 immune signatures / biomarkers
Page 2
Dataset
External cohorts
Preprocessing
ssGSEA immune profiling
ML models
Evaluation protocol
這頁一定要寫：
stratified repeated 5-fold CV
feature selection inside training folds
no data leakage
external validation
metrics：ROC-AUC、PR-AUC、F1、Accuracy
Page 3
Model comparison
Feature set comparison
External validation
ROC / PR curve
核心表格：
TaskFeature setModelROC-AUCPR-AUCF1AccuracyPage 4
SHAP summary
Top immune signatures / biomarkers
Biological interpretation
Limitation
Conclusion
limitation 建議誠實寫：
sample size is limited
retrospective public datasets
cohort heterogeneity / batch effect
not a longitudinal progression prediction
clinical validation is still needed
這樣不會扣分，反而會讓 paper 比較可信。
解決 147 樣本偏少的最終方法
你們不要單純說「我們資料少」。
要改成這樣設計：
主設計
GSE121212 as discovery cohort
GSE154200 as external validation cohort
GSE140227 and GSE14905 as disease-specific signature replication cohorts
GSE153007 as cross-platform validation cohort if usable
也就是：
問題解法GSE121212 只有 147 samples加外部 cohort validationRNA-seq feature 太多，樣本少用 ssGSEA 降維成 immune signaturesoverfitting 風險repeated CV + leakage-free pipeline只在單一 dataset 成立cross-cohort validation生物意義不足SHAP + biomarker / pathway interpretation平台差異RNA-seq 用 model validation；microarray 用 signature replication
這樣 reviewer 看到的就不是：
你們只有 147 samples。
而是：
你們有一個 discovery cohort，並且用多個 public cohorts 驗證主要 immune signatures。
這個說服力差很多。
最終通過率評估
如果你們照這份最終版完整做完，我會這樣評分：
完成程度BigComp short paper 通過率評分只完成 GSE121212 + 基本 ML6.5～7/10完成 GSE121212 + repeated CV + SHAP7.5～8/10加上 GSE154200 外部驗證8～8.3/10再加 GSE140227 / GSE14905 signature replication8.3～8.5/10圖表漂亮、story 清楚、limitation 嚴謹8.5/10 左右
我不會說 100% 穩過，因為 conference review 本來就有不確定性，而且 BigComp 不是純醫療 AI 會議。
但如果你們真的照這份做完，你們會從：
可以挑戰 BigComp short paper
提升到：
有明顯競爭力，而且被接受不意外。
最終一句話版本
你們最高通過率的做法是：
用 GSE121212 做主實驗，不硬說預測未來惡化；改成 lesional-like immune activation risk stratification。7 月完成 ML + repeated CV，8 月完成 SHAP + GSE154200 外部驗證，9 月只修 paper，並用 GSE140227 / GSE14905 補強 AD/PSO signature replication。
這樣是目前你們這個題目衝 BigComp short paper 最穩、最合理、最能防 reviewer 攻擊的安排。
