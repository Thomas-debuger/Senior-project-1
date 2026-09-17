我重新把 **ICBBB 那 9 篇全文**和 ICPRAM 裡真正能確認為 **Position Paper → Short Paper** 的案例重新看過後，我會選：

# 優先投 ICBBB Full Paper

這次我的理由不是「ICBBB 比較簡單」，而是你的研究本質上 **更像一篇已完成的 ICBBB Full Paper，而不像 ICPRAM Position Paper**。

ICPRAM 官方自己其實把兩種 paper 定義得很清楚：

* **Regular Paper**：completed and validated research
* **Position Paper**：work in progress 或 arguable opinion

Position Paper 的 review 標準也會特別考慮它可能仍屬 speculative / ongoing、尚未完全驗證，而且錄取後一定是 Short Paper，proceedings 上限 8 頁。

你的研究現在反而已經超過典型 Position Paper 的成熟度。

你已經有：

> PSORT-D：82 人，ADA / UST 各 41
>
> PSORT-R：53 人，ADA 26、UST 27
>
> 8 個 prespecified branches
>
> 50×5 repeated CV
>
> fold-contained limma + RFE + scaling + tuning
>
> model freeze
>
> completely independent external validation

而且 PSORT-R 明確沒有參與：

* feature screening
* feature selection
* tuning
* calibration
* threshold optimization
* post-hoc model modification

這已經不是：

> 「我有一個 idea，做了一些 preliminary experiments」

的研究了。

---

## 我重新看 ICPRAM Position Paper 後，差異更明顯

我們這 9 篇 ICPRAM Bioinformatics papers 中，能 **官方確認是 Position submission** 的幾篇很有代表性。

### 2024 Parkinson sEMG

這篇是：

```text
ICPRAM24-PP-154
```

所以確實是 Position Paper。

它不是提出新的 HMM，而是把：

* HMM / GMM
* wavelet descriptors
* segmentation
* classification

整合成一個新 framework，再大量測試：

* HMM states
* Gaussian components
* feature descriptors
* 不同 configuration

官方最終結果報：

```text
Accuracy = 99.37%
CRS = 100%
```

也就是它雖然是 Position Paper，仍然很 **Pattern Recognition-oriented**：

```text
representation
    ↓
descriptor
    ↓
model configuration
    ↓
segmentation
    ↓
classification
```

---

### 2023 Bone Phantom

這篇更典型，是官方：

```text
ICPRAM23-PP-113
```

它是一個 proof-of-concept：

> 用 DFT-derived signal features 和 mathematical decision rules
> 去估 cortical thickness / porosity

實驗設計則是：

> 每個 phantom 輪流當 test，其餘當 training。

---

### 2021 Bio-inspired Models + Machine Learning

這篇甚至在摘要裡直接寫：

> **“This position paper proposes the integration of bioinspired models with machine learning.”**

它真正的主旨是：

> medical human datasets 很小，甚至可能 features > samples，因此應該把 mechanistic / bio-inspired models 和 ML 結合。

它本身不是一篇：

```text
new cohort
    ↓
完整建模
    ↓
external validation
```

的 conventional prediction paper。

---

因此 ICPRAM Position Paper 的樣子其實比較接近：

> **「我提出一個值得 Pattern Recognition 社群討論／驗證的方法觀點或初步 framework，並給一些 supporting experiments。」**

而你現在比較像：

> **「我完成了一個 precision-medicine bioinformatics study，而且有真正 external patient validation。」**

兩者不是單純「Full vs Short」而已，而是 **paper identity 不同**。

---

# 再看 ICBBB 9 篇，我反而更確定你可以投 Full

最關鍵的不是那些很強的新演算法 paper，而是 ICBBB 同時接受了好幾篇 **沒有新 core ML algorithm** 的 Full Paper。

---

## 1. Comparative Evaluation of Drug Response Metrics for Predicting Cancer Sensitivity Using Transcriptomic Profiles

這篇就是：

```text
Transcriptomics
    ↓
Drug Response
    ↓
XGBoost
    ↓
比較三種 Response Definitions
```

資料包含：

```text
636 cancer cell lines
169 drugs
```

但 classifier 基本上就是一個 XGBoost family。

它的 contribution 根本不是：

> 「我們發明新的 classifier。」

而是：

> **AUC、Z-score、IC50 哪一個 response metric 比較適合 transcriptomic drug-response prediction？**

而且 Discussion 花很多力氣解釋 clinical / biological meaning。

這跟你的 contribution 型態其實很像：

```text
Gene vs Pathway 哪種 representation？
                ↓
Baseline vs Early Longitudinal Information？
                ↓
ADA vs UST 是否有不同 predictive signal？
                ↓
能不能 external generalize？
```

---

## 2. A Comprehensive Preprocessing Pipeline for TCGA-BRCA Multi-Omics Data Integration

作者自己明寫：

> **“Rather than developing novel normalization algorithms...”**

也就是他們直接承認：

> 沒有新的 preprocessing algorithm。

它的 contribution 是：

```text
Established Methods
        ↓
Systematic Pipeline
        ↓
Rigorous QC
        ↓
Reproducibility
        ↓
Biological Validation
```

Results 則大量做 biological validation，包括：

* methylation-expression relationship
* CNV-expression relationship
* PAM50
* survival
* known genes

這種 reviewer taste 和你的：

```text
Prediction
    ↓
External Validation
    ↓
Pathway / GSEA Biological Interrogation
```

非常合。

---

## 3. scRNA Embedding Stability Paper

這篇也不是發明新的 dimensionality reduction algorithm。

它直接使用：

* t-SNE
* UMAP
* PCA
* Monocle 3

然後去問一個新的 scientific question：

> input shuffling 會不會改變 embedding stability？

它用了六個 scRNA datasets，再從 biological relationships 的角度解釋 embedding instability。

也就是說，ICBBB Full Paper 的 novelty 可以是：

> **New biological / computational question**

而不是一定要：

> **New algorithm**

---

## 4. StackFeat

當然 ICBBB 裡也有 StackFeat。

這篇對你特別有參考價值，因為它直接就是：

> **d ≫ n genomic problem**

資料規模：

```text
122 patients
332 miRNAs
```

它比你強的地方是自己發明 StackFeat，而且做了：

* selection stability
* 10×10 CV
* different classifier verification
* 1.5 年後重新執行仍得到相同 signature

你的：

```text
n = 41
```

明顯比它弱。

但是你有 StackFeat 沒有的一張牌：

> **真正另一批患者的 independent external validation。**

所以你不是 ICBBB 頂級稿，但完全有 **Full Paper 的形狀**。

---

# 真正決定我的其實是這張表

| 比較項目                                       | ICBBB Full                                | ICPRAM Position                        |
| ------------------------------------------ | ----------------------------------------- | -------------------------------------- |
| 你的研究已經完成？                                  | **非常適合**                                  | 反而有點超出典型定位                             |
| n = 41                                     | 弱點，但可用 external cohort 防守                 | 小樣本本身不是大問題                             |
| 沒有新 algorithm                              | **可接受**                                   | Position 降低壓力，但仍是 PR conference        |
| 只有 Elastic Net                             | 中等弱點                                      | **仍會被 PR reviewer 注意**                 |
| Independent external validation            | **非常有價值**                                 | 有價值，但 Position 本來甚至不要求 fully validated |
| Drug-specific transcriptomics              | **非常對口**                                  | Application fit 可以，但不是 conference 核心   |
| Pathway / GSEA biology                     | **重要 contribution**                       | Supporting contribution                |
| 8 branches / Gene vs Pathway / W0 vs W0+W1 | 很適合 Full story                            | 8 頁開始有點擠                               |
| 最自然的 novelty                               | **Precision bioinformatics study design** | 必須重新包成一個「position」                     |
| 論文篇幅                                       | 8–10 single-column pages                  | Accepted Position = 8 pages            |
| 我對 fit 的判斷                                 | **高**                                     | 中等                                     |

ICBBB 2027 官方也明確把以下主題列在 CFP：

* **Machine Learning Applications in Bioinformatics**
* **AI in Precision Medicine and Genomic Prediction**
* **Data Mining and Pattern Recognition in Genomics**

而且 Full Paper 就是：

```text
Presentation + Publication
```

---

# 一個很容易產生的誤會：Position Paper 不等於「Regular Paper 的簡單模式」

這一點現在我會特別提醒。

你可能會想：

```text
ICPRAM Regular 對 novelty 要求高
            ↓
那我改投 Position
            ↓
Reviewer 就不太要求 novelty
            ↓
因此比 ICBBB Full 更安全
```

只有前半對。

Position 的確會使用稍微不同的 review criteria，因為官方承認它可以是：

* speculative
* ongoing work
* 尚未完全驗證

但它不是：

> **「任何完整研究都可以降級來增加錄取率。」**

它其實是在換問題。

Regular reviewer 問的是：

> 研究是否完整、新穎、驗證充分？

Position reviewer 會更接受：

> 這個 idea / methodological position 是否值得提出？
> 即使還沒完全驗證，它是否有 scientific value？

所以如果你把現在這篇完整 PSORT 直接砍成 8 頁丟 Position，我反而擔心它會變成：

> 「一篇正常的 biomedical prediction paper，但作者自己把它標成 Position。」

不是不能收，但沒有充分利用 Position track 的特色。

---

# 如果真的要投 ICPRAM Position，我會要求重新定義整篇 Paper

不能只是把 ICBBB 版本砍短。

我會把 ICPRAM Position Paper 的核心變成：

> **Can rigorous leakage-controlled modeling and independent validation make extreme p≫n transcriptomic prediction scientifically useful despite very small clinical cohorts?**

然後 PSORT 變成一個 **case study**。

整個故事會變成：

```text
Small clinical transcriptomic cohorts are unavoidable
                        ↓
p ≫ n makes feature/model instability severe
                        ↓
Aggressive complexity is not necessarily desirable
                        ↓
Fold-contained FS
+ Sparse Regularization
+ Model Freeze
                        ↓
Independent Cohort Validation
                        ↓
ADA / UST PSORT Case Study
```

這樣才像真正的：

> **ICPRAM Position Paper**

而不是：

> 「我們預測 psoriasis drug response。」

後者明顯更像 ICBBB。

---

# 所以我會怎麼選？

如果你的目標是：

> **讓這項 PSORT 研究以最自然、最好防守的形式正式發表**

我選：

# ICBBB Full Paper

而且不是五五波。

我的投稿選擇權重大概是：

```text
ICBBB Full      70%
ICPRAM Position 30%
```

注意：

> 這不是 acceptance probability，而是 **投稿選擇權重**。

---

## 成功率粗略估計

### ICBBB Full

完成版我大致維持：

```text
約 65–80%
中心估計約 75%
```

### ICPRAM Position

我反而不會直接因為「Position」就給比 Regular 高很多。

如果有 **真的重新寫成 Position-paper framing**：

```text
約 55–70%
```

如果只是把現在完整 empirical study 直接縮短：

```text
約 50–60%
```

這些仍然只是從 accepted-paper profile 推估，**不是官方 acceptance rate**。

---

# 唯一會讓我改選 ICPRAM Position 的現實因素：時間

目前兩個 deadline：

```text
ICBBB 2027 Full Paper
2026/10/05
```

```text
ICPRAM Position / Regular Second Stage
2026/10/22
```

你現在 Methods 已經寫得相當完整，但 Word 裡目前：

```text
4 RESULT

5 DISCUSSION

6 CONCLUSION & LIMITATION
```

還是空的。

而且 UST biological validation 還有我們剛抓出的：

```text
3/8
7 genes
9 genes
```

版本矛盾需要先 resolve。

---

# 最終決策

所以我的決策其實非常清楚。

如果你能在 **2026/10/05 前**把以下內容全部整理好：

* Results
* Discussion
* Limitations
* References
* UST biological consistency

那就：

> **投 ICBBB Full Paper。**

如果 10/05 前做不到，而且硬趕會讓論文品質明顯下降：

> **改投 2026/10/22 的 ICPRAM Position Paper。**

但這時不能只是把 ICBBB Full Paper 砍短，而應重新包裝成：

> **Small-n / p≫n clinical pattern recognition 的 methodological position + PSORT case study**

---

# Conclusion

純粹從 **研究內容適配性** 來看，我現在會選：

> # **ICBBB Full Paper**

從這次重新閱讀 accepted papers 的結果來看，你的研究其實沒有必要因為：

> 「沒有新的 ML 演算法」

就主動把自己降成 Position Paper。

你的主要 contribution 並不是新 classifier，而是：

```text
Rigorous leakage-controlled modeling
                +
Small-n high-dimensional transcriptomics
                +
Gene vs Pathway representation
                +
Baseline vs Early longitudinal information
                +
Drug-specific modeling
                +
Independent external patient validation
                +
Biological interpretation
```

這整體更像一篇：

> **完整的 precision bioinformatics Full Paper。**
