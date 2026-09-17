# ICBBB、ICPRAM、IEEE BigComp 投稿適配性分析

## 1. 最終結論

這次重新把前面的名次與機率全部丟掉，重新從三組各 **9 篇已錄取論文** 出發：

* **ICBBB**：使用已取得的全文
* **IEEE BigComp**：使用已取得的全文
* **ICPRAM**：重新核對正式 proceedings 與可取得全文

重新檢視各篇論文的：

* Problem
* Data
* Method
* Novelty
* Comparison
* Validation
* Discussion

並以相同方式重新檢視目前的 Methods 草稿與兩份簡報。

> 這裡的「第幾名」是把目前研究加入該會議的 9 篇已錄取 benchmark 中，形成 **10 篇一起比較**，而且是依照各會議自己的審稿偏好評估，不是三個會議共用同一套標準。

| 會議                     |          相對位置 | 合理波動 |            估計錄取機率 | 最可能結果                                |
| ---------------------- | ------------: | ---: | ----------------: | ------------------------------------ |
| **ICBBB**              |  **第 5 / 10** |  4–6 | **約 75%（65–80%）** | Full Paper 有合理機會                     |
| **ICPRAM**             |  **第 5 / 10** |  4–6 | **約 65%（55–70%）** | Regular 投稿後，**Short acceptance 最合理** |
| **IEEE BigComp Short** | **第 10 / 10** | 9–10 | **約 35%（25–40%）** | 可以投，但三者中風險最高                         |

### 注意

以上百分比：

> **不是官方 Acceptance Rate。**

而是：

> 如果站在看過這批已錄取論文的 reviewer 角度，估計目前研究穿過 review threshold 的可能性。

因為沒有 rejected-paper corpus，所以不能把 75%、65%、35% 當成統計意義上的真實錄取率。

另外，這個評估有一個重要前提：

> 評估的是「目前草稿完成，並把兩份簡報中的 Results 與 biological validation 正式寫進論文」之後的版本。

目前 Word 中：

* Results
* Discussion
* Conclusion / Limitations

仍然只是空標題。

如果直接把目前的五頁半成品原封不動投稿，就不適用以上錄取機率。

---

# 2. 三個會議其實在找三種不同的東西

重新看完 27 篇論文後，最重要的結論是：

> **ICBBB、ICPRAM、BigComp 的 reviewer 所重視的研究價值並不相同。**

---

## 2.1 ICPRAM

ICPRAM reviewer 的第一直覺比較接近：

> **「這篇對 Pattern Recognition / Machine Learning 有什麼值得看的東西？」**

ICPRAM 2027 reviewer guidance 明確評估：

* Relevance
* Originality
* Technical Quality
* Significance
* Presentation

而且 reviewer 會直接考慮：

* Needs more experimental results?
* Needs comparative evaluation?
* Improve critical discussion?

雖然 **Bioinformatics and Systems Biology** 正式被列在 Applications Track，但 ICPRAM 的核心仍然是：

> **Pattern Recognition**

### 從 9 篇 accepted papers 看到的特徵

較強的論文通常具有：

* PoS fused-lasso 新演算法
* Protein GNN + LLM 新 representation framework
* Cortical-column connectivity model
* Method comparison
* Parameter study
* Pattern-recognition experiment

換句話說：

> 沒有新演算法不是一定不能收，但通常必須有足夠完整的 Pattern Recognition 實驗深度。

---

### ICPRAM 對小樣本其實比原先預期更寬容

ICPRAM 曾接受：

* **17 人 Parkinson sEMG**

  * 9 healthy
  * 8 PD
* 極小型 bone phantom experimental dataset
* 討論 medical human datasets 太小，以及 mechanistic models + ML 的 Position Paper

因此：

> **n = 41 並不是 ICPRAM 最主要的問題。**

真正比較可能被 reviewer 攻擊的是：

> **只有 Elastic Net，缺少 classifier baseline comparison，而且沒有新的 Pattern Recognition algorithm。**

目前 Methods 中，八個 branch 都固定使用同一個：

> **Elastic Net classifier**

---

## 2.2 ICBBB

ICBBB reviewer 的第一直覺比較接近：

> **「這個 computational work 對 biology / medicine 到底有什麼意義？分析可信嗎？」**

ICBBB 2027 CFP 直接包含：

* Machine Learning Applications in Bioinformatics
* AI in Precision Medicine and Genomic Prediction
* Multi-Omics
* Biomedical Informatics
* Clinical Decision Support

ICBBB 官方只公開：

* Double-blind review
* 由相符領域專家審稿

不像 ICPRAM 有完整 numerical review rubric，因此主要從 9 篇 accepted papers 反推其偏好。

---

### ICBBB 的特徵

9 篇 accepted papers 顯示：

> **新演算法是很大的加分，但不是必要條件。**

例如：

#### TCGA-BRCA preprocessing paper

並沒有提出新的 normalization algorithm，而是建立：

* 完整 preprocessing pipeline
* Reproducible pipeline
* Biological validation

#### Cancer drug-response paper

核心方法甚至就是：

* XGBoost
* 搭配三種 response definition

因此 ICBBB 並不要求一定要有全新 ML algorithm。

---

### ICBBB 特別常見的研究邏輯

```text
Computational result
        ↓
Biological interpretation
        ↓
Known biology / pathway / marker consistency
```

其中 **StackFeat** 特別值得參考：

* 122 patients
* 332 miRNAs
* 屬於典型 **d ≫ n genomic feature-selection problem**
* 強調 repeated stability
* classifier validation
* biomarker biology

它很接近目前研究可能遇到的 ICBBB reviewer 思維。

因此：

> **41 人非常小，是明確弱點；但「沒有新 classifier」並不是致命傷。**

---

## 2.3 IEEE BigComp

BigComp 的核心定位是：

> **Big Data and Smart Computing**

Topics 雖然包含 Bioinformatics，但同時包含：

* Machine Learning and AI for Big Data
* Techniques / Models / Algorithms for Big Data
* Infrastructure / Platforms
* Multimodal Data
* Scalable Computing

從 9 篇 BigComp Short Paper 可以看到非常穩定的 pattern：

> **要嘛有 computational novelty，要嘛有 big-data scale + 完整 model comparison。**

最好甚至兩者都有。

---

### 例子 1：COVID Protein Paper

其中一個 dataset 只有：

> **90 sequences**

資料並不大。

但是它：

* 提出 **SDCPSF**
* 使用 **Apache Spark**
* 做 scalable feature extraction

因此它的 BigComp identity 來自：

> **Algorithmic + scalable computing contribution**

而不是 observation 數量。

---

### 例子 2：PROTAC

真正 validation 只有：

> **52 PDB structures**

其實跟目前研究的 41 人沒有差非常多。

但它：

* 提出新的 exposure-based algorithm
* 量化 search-space reduction
* Search-space reduction = **87.4%**

---

### 例子 3：Cancer Readmission

沒有新 algorithm，但資料規模是：

> **15,877 patients × 4,437 features**

而且比較：

* Logistic Regression
* Decision Tree
* Random Forest
* XGBoost

---

### 例子 4：Heart Failure

最終約：

> **2,000 patients**

實驗包含：

> **4 models × 3 missing-value strategies + feature-selection experiment**

---

### BigComp 的問題

這就是為什麼目前研究在 BigComp benchmark 中會被排到最後。

不是研究本身不嚴謹，而是：

> **目前研究擁有的 contribution 與 BigComp 最重視的 contribution 不完全重疊。**

---

# 3. 目前研究真正的強項

目前研究設計其實不弱，而且有幾個很明確的優勢。

---

## 3.1 真正獨立的 External Validation

### Development Cohort：PSORT-D

* ADA：**41**
* UST：**41**

### External Cohort：PSORT-R

* ADA：**26**
* UST：**27**

而且：

> **Patient 才是 analysis unit。**

沒有把：

* W0
* W1

當成額外獨立 observations 來灌大樣本數。

這一點非常重要。

---

## 3.2 Leakage-Controlled Development

50 × 5 repeated CV 中：

```text
limma
  ↓
RFE
  ↓
Standardization
  ↓
Hyperparameter tuning
```

全部限制在：

> **Training fold only**

也就是：

* limma 不看 validation fold
* RFE 不看 validation fold
* standardization 不看 validation fold
* tuning 不看 validation fold

最終確定：

* K
* α
* λ

之後，才使用完整 PSORT-D refit。

接著 freeze：

* Classifier
* Calibration
* Decision procedure

再進入 PSORT-R。

PSORT-R 完全沒有參與：

* Feature selection
* Hyperparameter tuning
* Calibration fitting
* Threshold optimization

因此：

> **Generalization design 是整個研究最強、最值得強調的部分之一。**

---

## 3.3 External Cohort 的價值

27 篇 accepted papers 中，很多研究雖然 dataset 大得多，但 validation 仍然只是：

* Random split
* Cross-validation
* Internal holdout

目前研究則真的有：

> **另一個 independent cohort**

因此即使 development n 很小，independent external validation 仍然是一個實質優勢。

---

## 3.4 Transparent Reporting

目前共有：

> **8 個 biological branches**

這些 branch 在 external testing 前就全部 freeze。

外測後：

> **全部照實報告，不因為結果不好就換模型。**

結果並不是全部漂亮。

例如較好的：

* ADA W0 Gene AUROC：**81.70%**
* UST W0+W1 Pathway AUROC：**85.80%**

但其他 6 個 branches 中：

* 很多 AUROC 約 **0.33–0.60**
* 部分模型甚至出現 **Specificity = 0**

這些結果本身是 weakness。

但是：

> **全部如實呈現，可以降低 reviewer 對 cherry-picking 的懷疑。**

---

# 4. Reviewer 最可能攻擊的地方

## 4.1 Effective Sample Size

最嚴重的問題仍然是：

> **Effective sample size 就是 41。**

不是因為做了：

> 50 × 5 CV

就變成幾千個 observations。

Repeated CV 的作用是：

> **降低 partition dependence**

而不是：

> **創造新的獨立資訊。**

External validation 可以大幅緩解這個問題，但不能完全消除 small-n limitation。

---

## 4.2 Algorithmic Novelty 很低

目前使用的：

* limma
* RFE
* Elastic Net
* Platt calibration

全部都是：

> **Established methods**

因此 novelty 不能寫成：

> 「我們提出新的 ML algorithm。」

真正合理的 novelty 應該放在：

```text
Drug-specific treatment-response prediction
        +
Gene vs Pathway representation
        +
Baseline vs Early longitudinal information
        +
Leakage-controlled development
        +
Independent external validation
```

也就是：

> **研究設計與 clinical/bioinformatics application 的 novelty，而不是 ML algorithm novelty。**

---

## 4.3 缺少 Multi-Model Comparison

這個問題的重要程度依 venue 而不同：

| Venue       | 影響程度  |
| ----------- | ----- |
| **ICBBB**   | 中度弱點  |
| **ICPRAM**  | 明顯弱點  |
| **BigComp** | 很大的弱點 |

BigComp biomedical short papers 中甚至有 SNP paper：

### Feature Space

> **167,768 SNP positions**

### Feature-selection methods

* RRF
* XGBoost
* MIFS
* Random FS

### Classifiers

* Random Forest
* XGBoost
* MLP
* CNN
* Bi-LSTM
* Transformer

最後才建立 multimodal model。

---

目前研究的 comparison 主要是：

```text
4 biological representations
        ×
K
        ×
α
        ×
λ
```

而不是：

```text
Elastic Net
vs
SVM
vs
Random Forest
vs
XGBoost
```

這兩種 experimental depth：

> **在 CS reviewer 眼中並不完全等價。**

---

# 5. Feature Stability 問題

這是一個需要特別注意的地方。

## ADA 正式 K = 2

### TMEM120B

CV selection frequency：

> **19.6%**

### ST7

CV selection frequency：

> **4.8%**

---

## UST 8 Pathways

部分 pathway selection frequency 甚至只有：

* **1.6%**
* **6.8%**
* **7.2%**

這對 prediction model 本身：

> 不一定致命。

但是如果進一步宣稱：

> 「這些是 robust biomarkers」

reviewer 很可能會質疑。

因此 biological interpretation 必須區分三件事情：

```text
Predictive signature
≠
Stable individual biomarker
≠
Causal mechanism
```

不能因為某 feature 被最終模型選中，就直接稱它為：

* 穩定 biomarker
* causal pathway
* drug mechanism

---

# 6. UST Biological Validation 的內部矛盾

目前 UST biological slides 有一個必須修掉的問題。

其中一頁寫：

> **3 / 8 pathways：GSEA FDR < 0.05**

另外：

> **1 pathway borderline**

但是下一頁又寫：

> 7 個 high-effect genes 所屬的三條 pathways「皆未達 GSEA FDR < 0.05」

接著下一行又說這 7 genes 同時滿足：

> **Significant GSEA Pathway + Leading-edge gene**

最後流程圖又變成：

> **9 genes**

這看起來比較可能是：

> **簡報不同版本整合時產生的文字或數字錯誤**

不一定代表實際分析錯誤。

但是：

> **論文中絕對不能留下這種 contradiction。**

否則 reviewer 很可能會開始懷疑整套 biological validation 的 reproducibility。

---

# 7. 為什麼 ICPRAM 是第 5 / 10？

目前研究的：

* Technical rigor
* Leakage control
* Independent validation

其實比 ICPRAM 9 篇 accepted papers 中不少 application papers 更完整。

而：

> **n = 41 不足以直接把研究打到後段。**

因為 ICPRAM 本身已接受過：

* 17-subject Parkinson sEMG
* 極小型 bone phantom study
* Small medical-data Position Paper

---

## 明顯較強的 ICPRAM papers

真正會明顯排在目前研究前面的，主要是具有：

* New algorithm
* New representation
* New Pattern Recognition mechanism

的研究。

目前研究比較接近與：

* GAN comparative study
* Parkinson HMM application

這類 application paper 競爭中段。

---

## 雙方優勢

### 目前研究

> **Independent external validation 勝**

### 部分 ICPRAM accepted papers

> **Pattern Recognition experimental depth / model comparison 勝**

綜合後：

> **ICPRAM：第 5 / 10**

合理位置：

> **第 4–6**

---

## ICPRAM Acceptance Estimate

Regular Paper 投稿後：

> **Full 或 Short 任一形式接受：約 65%**

合理區間：

> **55–70%**

其中：

> **Short acceptance 明顯比 Full acceptance 更可能。**

如果只問：

> **Full Paper acceptance**

則估計約：

> **25–35%**

---

# 8. 為什麼 ICBBB 也是第 5 / 10？

ICBBB 是三個 venue 中：

> **研究 identity 最自然的一個。**

因為目前 clinical question 很直接：

> **Can lesional-skin transcriptomics predict PASI75 response to ADA and UST in psoriasis?**

研究具有：

* Precision Medicine application
* Drug-specific prediction
* Transcriptomics
* Independent patient cohort
* Biological interpretation

---

## UST 不只是 Prediction

UST 並不是 prediction 跑完就結束。

目前流程還包含：

1. 模型選出 8 pathways
2. 使用完整約 15,395 genes
3. 做 interaction ranking
4. Pre-ranked GSEA
5. Biological interpretation

而不是重新使用 external data 選 pathway。

目前結果：

> **3 / 8 pathways FDR significant**

另外：

> **1 pathway borderline**

這種 story 非常符合 ICBBB accepted papers 常見的：

```text
ML / Computational Signal
        ↓
Biological Interpretation
        ↓
Biological Plausibility
```

---

## ICBBB 並不要求一定有 New Algorithm

已錄取研究已經證明：

> **沒有新的 ML algorithm 仍然可以被接受。**

因此目前研究真正落後前段 paper 的原因主要是：

### 1. Small sample size

> **n = 41**

### 2. Algorithmic novelty 低

> 主要使用 established methods

### 3. ADA biological evidence 相對較弱

目前對 ADA 的 biological interpretation 其實相對克制：

* TMEM120B：目前較偏 indirect metabolic / lipid background
* ST7：沒有可靠直接 TNF-α link
* UST pathways：也明確承認不一定是 UST direct targets

這種克制其實是優點。

---

## ICBBB Ranking

不太會放到：

> **第 1–3**

因為：

* DICE-ZIKV
* DL-FSG
* StackFeat

這類 paper 的 computational contribution 更明確。

但也不至於落到後半。

因此：

> **ICBBB：第 5 / 10**

合理位置：

> **第 4–6**

---

## ICBBB Acceptance Estimate

完成版 Full Paper：

> **約 75%**

合理區間：

> **65–80%**

在三個 venue 中：

> **ICBBB 是目前最自然、最值得優先考慮的 venue。**

---

# 9. 為什麼 BigComp 是第 10 / 10？

這是重新檢查 9 篇 BigComp Short Papers 後最大的修正。

這並不是代表：

> 「目前研究的科學品質比 9 篇都差。」

真正的原因是：

> **BigComp reviewer 最重視的 contribution，目前研究擁有得最少。**

---

## 目前缺少的 BigComp 元素

### 沒有 New Algorithm

目前主要使用 established methods。

### 沒有 Distributed / Scalable Computing

例如：

* Spark
* Distributed processing
* Large-scale system

目前都不是研究 contribution。

### 沒有大量 Observations

真正的 independent patients：

> **n = 41**

### 沒有 Multi-Model / Strong Baseline Suite

主要 classifier：

> **Elastic Net**

---

# 10. 目前研究的「Big」是什麼？

最大的 computational characteristic 是：

> **p ≫ n**

例如：

```text
約 15,000 genes
vs
41 patients
```

這確實是一個：

> **High-dimensional computational problem**

而且 BigComp CFP 確實包含：

> **Bioinformatics**

所以並不是沒有投稿資格。

但從 9 篇 accepted papers 看，BigComp 對小型 biomedical dataset 通常需要其他東西補回來。

---

## Small Data + New Algorithm

### PROTAC

```text
52 PDB structures
+
New algorithm
```

### COVID Protein Subset

```text
90 sequences
+
New scalable distributed feature extraction
+
Apache Spark
```

---

## No New Algorithm + Large Data / Rich Comparison

### Cancer Readmission

```text
15,877 patients
+
4 classifiers
```

### Heart Failure Mortality

```text
~2,000 patients
+
4 models
×
3 imputation methods
```

### Neutropenia

```text
10,717 patients
+
Bi-LSTM
+
RETAIN
+
LR / RF baselines
```

### Biome

```text
Six classifier families
+
Multiple large climate datasets
+
Feature ablation
```

---

# 11. BigComp 最大的反擊點：External Validation

目前研究最大的防守點仍然是：

> **真正存在 independent external cohort。**

這表示研究不是沒有投稿 BigComp 的資格。

而且 external-validation quality 很可能比 9 篇 benchmark 中不少研究更加嚴格。

但是 BigComp reviewer 很可能仍然給出類似意見：

> **The study is carefully validated, but the computational novelty and big-data contribution are limited.**

這可能是最容易導致 rejection 的 comment。

---

## BigComp Ranking

因此：

> **IEEE BigComp Short：第 10 / 10**

合理區間：

> **第 9–10**

但中心判斷仍然是：

> **第 10**

---

## BigComp Acceptance Estimate

估計：

> **約 35%**

合理區間：

> **25–40%**

不是只有 10% 的原因是：

* Short Paper 本來即可容納較精簡研究
* 可以包含 work-in-progress 類型 contribution
* Independent external validation 是實質優勢
* Bioinformatics 正式在 CFP scope 中

但是：

> **BigComp 的適配度明顯低於 ICBBB 與 ICPRAM。**

---

# 12. 三個 Venue 最終比較

| 面向                        | ICBBB      | ICPRAM     | IEEE BigComp Short      |
| ------------------------- | ---------- | ---------- | ----------------------- |
| Small n 容忍度               | 中等         | **相對較高**   | 中等，但需其他 contribution 補償 |
| Bioinformatics fit        | **非常高**    | 中等         | 有，但不是核心                 |
| Clinical relevance        | **重要**     | 次要         | 次要                      |
| Biological interpretation | **重要**     | 加分         | 次要                      |
| New algorithm 要求          | 中低         | **中高**     | **高**                   |
| Model comparison 要求       | 中等         | **高**      | **很高**                  |
| External validation 價值    | **很高**     | 很高         | 很高                      |
| Big-data scale 要求         | 低          | 低          | **高**                   |
| 目前研究相對排名                  | **5 / 10** | **5 / 10** | **10 / 10**             |
| 估計接受機率                    | **約 75%**  | **約 65%**  | **約 35%**               |
| 整體適配性                     | **最自然**    | 可防守        | 風險最高                    |

---

# 13. 一句話總結三個 Venue

## ICBBB

> **弱點是 sample size，但 clinical / bioinformatics question、independent external validation 與 UST biological interpretation 正好符合 venue 重視的內容，因此約第 5 / 10，估計約 75%。**

---

## ICPRAM

> **Small n 不是最大問題，真正的問題是 classifier comparison 與 methodological novelty 不足；rigorous validation 把研究拉回中段，因此約第 5 / 10，估計約 65%。**

---

## IEEE BigComp Short

> **External validation 很好，但 small n + 無 new algorithm + 無 multi-model comparison 同時撞上 BigComp 重視的幾個方向，因此在 9 篇 accepted benchmark 中排第 10 / 10，估計約 35%。**

---

# 14. 最適合目前研究的 Positioning

目前最值得維持的方向：

> **不要為了投稿硬創造一個假的 methodological novelty。**

研究的真正 identity 應該寫成：

> **Treatment-specific transcriptomic response prediction under an extreme p ≫ n setting, using leakage-controlled model development, independent cohort validation, and biological interrogation of the UST predictive signature.**

換成比較完整的概念就是：

```text
Treatment-specific prediction
        +
Extreme high-dimensional transcriptomics (p ≫ n)
        +
Gene vs Pathway representations
        +
Baseline vs Early longitudinal information
        +
Leakage-controlled feature selection and tuning
        +
Independent external cohort validation
        +
Biological interrogation of the UST signature
```

而不是：

```text
We propose a novel machine-learning algorithm.
```

因為實際上並沒有提出新的 ML algorithm。

---

# 15. 最後結論

目前研究的定位：

* **ICBBB：非常合理**
* **ICPRAM：可以防守**
* **IEEE BigComp：相對吃虧**

其中最重要的研究價值並不是：

> 「使用了 Elastic Net、RFE 或 limma。」

而是：

> **在極端 p ≫ n 的 treatment-response transcriptomic prediction 問題中，採用 leakage-controlled development，並使用完全獨立 cohort 驗證泛化能力，再進一步針對 UST predictive signature 進行 biological interrogation。**
