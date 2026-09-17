# PSORT 在 ICBBB 尺度下的雙面向 Contribution 評估

如果完全把 PSORT 和這 **9 篇 ICBBB accepted papers 放在同一把 ICBBB 尺上**，並且把：

* 資訊工程 Contribution
* 生物／醫學 Contribution

真正拆開評估，目前最適合的結論是：

> **資訊工程 Contribution：中**
>
> **生物／醫學 Contribution：強**

這是目前最適合定稿的兩個等級。

但資訊工程有一個很重要的特殊性：

> **Computational Novelty：中低**
>
> **Computational Rigor / Validation Design：強**

兩者合起來，整體資訊工程 Contribution 才評為：

> **中**

而不是單純說資訊工程端很弱。

---

# 1. 與 9 篇 ICBBB Accepted Papers 的直接比較

| Paper                     | 資訊工程 Contribution | 生物／醫學 Contribution |
| ------------------------- | ----------------: | -----------------: |
| **DICE-ZIKV**             |            **極強** |             **極強** |
| **DL-FSG**                |            **極強** |             **中高** |
| **StackFeat**             |            **極強** |              **強** |
| **TCGA-BRCA Pipeline**    |          **中高～強** |              **強** |
| **Single-cell Stability** |             **強** |             **中高** |
| **TooT-SS**               |            **中高** |             **中高** |
| **K-mer CNN**             |            **中高** |             **中高** |
| **Drug-response XGBoost** |          **中低～中** |           **中高～強** |
| **Cancer GCN + SHAP/IG**  |             **中** |              **中** |
| **PSORT**                 |             **中** |              **強** |

這張表就是目前最接近整個問題核心的答案。

---

# 2. 為什麼 PSORT 的資訊工程只有「中」？

如果 Contribution 的意思是：

> **你對 Computer Science / Machine Learning 方法本身新增了什麼？**

那麼不能把很多「做得非常嚴謹」的設計，直接視為：

> **Methodological Novelty**

目前 PSORT 使用：

* limma
* RFE
* Elastic Net
* Repeated Cross-validation
* Platt Calibration

這些全部都是：

> **Established Methods**

而且正式使用的 classifier family 只有：

> **Elastic Net**

因此，如果純粹看：

> **Computational Novelty**

目前只能給：

> **中低**

---

# 3. StackFeat 為什麼屬於強甚至極強？

StackFeat 和 PSORT 都面對：

> **d ≫ n 的 High-dimensional Genomic Problem**

但 StackFeat 並不只是套用既有 Feature Selection。

它直接針對：

> **Feature-selection Instability**

設計新的方法。

核心概念包含：

* Signed Coefficient Consistency
* Selection Frequency
* 雙條件 Feature Selection
* Convergence Logic

最後建立出的 5-marker signature 中：

> **4 個 marker 在至少 77% iterations 中被重複選中**

而且又透過：

> **10 × 10 CV + Multiple Classifiers**

進行驗證。

這種研究屬於：

> **直接針對一個 ML / Computational Problem 提出新的方法解法**

因此資訊工程 Contribution 可以到：

> **強甚至極強**

---

# 4. DL-FSG 為什麼也是極強？

DL-FSG 的 Computational Contribution 非常清楚。

它自己提出新的：

> **Representation / Fusion Architecture**

並且與：

> **7 個 Contemporary Methods**

直接進行 benchmark。

另外還包含：

* Attention Ablation
* Representation Ablation
* Protein-input Ablation
* Runtime Comparison
* FLOPs Comparison

因此不只是：

> 「模型預測得很好」

而是有完整的：

```text
New Architecture
      ↓
Strong Baselines
      ↓
Ablation
      ↓
Efficiency Evaluation
```

這就是典型的：

> **極強 Computational Contribution**

---

# 5. Single-cell Stability 為什麼可以到「強」？

Single-cell Stability 並沒有重新發明：

* t-SNE
* UMAP

但是它提出了一個非常明確的新 Computational Research Question：

> **Input Shuffling 到底會不會破壞 Embedding Stability？**

接著使用：

* 6 datasets
* Jaccard Index
* kNN Preservation
* Calinski-Harabasz Index
* Davies-Bouldin Index
* Xie-Beni Index
* RF-hierarchical Analysis

進行系統性驗證。

因此它雖然沒有新 algorithm，但：

> **Computational Question 本身很明確，而且整篇研究就是圍繞這個 methodological problem 展開。**

所以可以到：

> **強**

---

# 6. PSORT 缺少這種程度的 Computational Novelty

目前 PSORT 沒有：

* 新 Algorithm
* 新 Representation Architecture
* 新 Learning Framework
* 新 Feature-selection Algorithm
* 一個全新的 ML Methodological Problem

因此：

## Computational Novelty

> **中低**

這一點必須和：

> **Validation Rigor**

分開看。

---

# 7. 但 PSORT 的 Computational Rigor 很強

這完全是另外一回事。

PSORT 並不是：

```text
Full Dataset Feature Selection
        ↓
Cross-validation
        ↓
Report Good Performance
```

而是在每個 Training Fold 內重新執行：

```text
limma
  ↓
RFE
  ↓
Scaling
  ↓
α / λ Tuning
```

也就是：

> **Feature Screening、Feature Selection、Standardization、Hyperparameter Tuning 全部限制在 Training Fold。**

Validation Fold 完全沒有參與。

---

# 8. Repeated CV + Independent External Validation

接著使用：

> **50 × 5-fold Repeated Cross-validation**

完成 Development。

最終再：

1. Freeze Feature Set
2. Freeze K
3. Freeze α / λ
4. Freeze Classifier
5. Freeze Calibration
6. Freeze Threshold

最後才進入：

> **PSORT-R Independent External Cohort**

而 PSORT-R 完全沒有參與：

* Feature Selection
* Hyperparameter Tuning
* Calibration
* Threshold Optimization

因此如果單獨評估：

> **Computational / Methodological Rigor**

可以給：

> **強**

甚至可以視為這 9 篇 ICBBB Accepted Papers 中的：

> **前段**

---

# 9. PSORT 資訊工程細項拆解

| 細項                                 |       等級 |
| ---------------------------------- | -------: |
| **Algorithm Novelty**              |   **中低** |
| **Representation Novelty**         |    **中** |
| **Experimental Design**            |    **強** |
| **Leakage Control**                |    **強** |
| **Validation Rigor**               |    **強** |
| **Multi-model Comparison**         |   **中低** |
| **Feature-stability Evidence**     | **中低～中** |
| **Reproducibility / Transparency** |    **強** |
| **資訊工程總 Contribution**             |    **中** |

---

# 10. 為什麼最後不是「中高」？

核心原因是：

> **Rigorous Evaluation ≠ New Computational Contribution**

Rigorous evaluation 可以讓 reviewer 更相信：

> **你的結果是真的，而不是 Data Leakage 或 Overfitting 製造出來的。**

但它不等於：

> **你解決了一個新的 ML Methodological Problem。**

這個區別非常重要。

因此：

> **Computational Rigor = 強**

並不代表：

> **Computational Contribution = 強**

最終資訊工程 Contribution 評為：

> **中**

是比較合理的。

---

# 11. PSORT 的生物／醫學 Contribution 為什麼是「強」？

這部分完全不同。

PSORT 的問題不是一般的：

> **Psoriasis vs Healthy Classification**

而是：

> **接受 ADA 或 UST 的 psoriasis patient，能不能從 lesional-skin transcriptomics 預測 Week-12 PASI75？**

這是一個直接的：

> **Treatment-response / Precision-medicine Problem**

---

# 12. Drug-specific Prediction

PSORT 並沒有把：

> ADA + UST

混在一起建立一個 generic model。

而是分別建立：

> **ADA-specific Model**

以及：

> **UST-specific Model**

因此研究問題不是：

> 「乾癬患者能不能被分類？」

而是：

> **不同 biologic treatment 的 response 是否能由不同 molecular signals 預測？**

這個問題在 biology / medicine 上有明確意義。

---

# 13. 同時比較 Time 與 Molecular Representation

PSORT 系統性比較：

## Temporal Representation

* W0
* W0+W1

## Molecular Representation

* Gene
* Pathway

因此完整架構是：

```text
ADA / UST
    ×
W0 / W0+W1
    ×
Gene / Pathway
```

實際在問的是：

> **不同 biologic 的 predictive molecular information，是否存在於不同時間點、不同 biological representation？**

這是一個有實際生物與 Precision Medicine 意義的問題。

不是單純：

> **ML Exercise**

---

# 14. External Validation 本身也是 Biological / Clinical Contribution 的一部分

External Validation 不只是資訊工程上的 validation。

它同時代表：

> 不只是證明「模型在 Development Cohort 的 CV 很準」。

而是進一步檢查：

> **在另一批真正的 psoriasis patients 中，這個 treatment-specific molecular signal 是否仍具有 generalizability。**

因此：

> **Independent Patient Cohort**

讓 clinical interpretation 明顯比單一 cohort study 更強。

---

# 15. UST 把 Biological Contribution 再往上推一層

UST 並不是做到：

> **Pathway Predictor AUROC ≈ 0.85**

就結束。

而是把模型已選定的 pathways 進一步拿去問：

> **Responder 與 Non-responder 從 W0 → W1 的 transcriptional response，是否真的在這些 pathway 呈現 coordinated gene-level signal？**

流程概念為：

```text
Predictive Pathways
        ↓
Gene-level Interaction
        ↓
Pre-ranked GSEA
        ↓
Leading-edge Interpretation
```

因此形成：

> **Prediction → Independent Biological Interrogation**

這種設計非常符合 ICBBB。

---

# 16. 與 TCGA-BRCA 的邏輯類似

TCGA-BRCA accepted paper 沒有發明新的 normalization algorithm。

它的價值在於：

> 使用 biological evidence 證明 preprocessing pipeline 沒有把真正的 biology 洗掉。

例如檢查：

* Subtype Accuracy
* Cross-omics Relationship
* Known Driver Genes
* Survival Association

因此：

> **Established Computational Methods + Strong Biological Validation**

在 ICBBB 是可以成立的。

---

# 17. Drug-response XGBoost 也是重要參考

Drug-response paper 的核心 classifier 其實只有：

> **XGBoost**

真正的 Contribution 是研究：

> **哪一種 response metric 最適合 transcriptomic pharmacogenomic prediction？**

所以 PSORT 在 ICBBB：

> **不需要依賴 Elastic Net 本身的新穎性來成立。**

真正需要強調的是：

* Treatment-specific Question
* Independent Validation
* Gene vs Pathway
* W0 vs W0+W1
* Biological Interpretation

---

# 18. 為什麼 Biological Contribution 不是「極強」？

「極強」比較適合像：

> **DICE-ZIKV**

這種從：

```text
Sequence
   ↓
Causal Mutation
   ↓
Molecular Interaction
   ↓
Cellular Pathway
   ↓
Evolutionary Forecasting
```

把 Computational Model 和 Mechanism 串得非常完整的研究。

DICE-ZIKV 甚至跨越：

* Molecular Scale
* Cellular Scale
* Evolutionary Scale

---

# 19. PSORT 目前缺少的 Biological Evidence

PSORT 目前沒有：

* Wet-lab Functional Validation
* Direct Mechanistic Experiment
* Prospective Treatment Cohort
* Causal Inference
* Functional Perturbation Experiment

而且：

> **ADA Biology 相對薄弱。**

UST 目前也應該描述成：

> **Predictive Pathways with Transcriptomic Coherence**

而不能直接升級成：

> **UST Mechanism**

因此 Biological Contribution 最合理停在：

> **強**

而不是：

> **極強**

---

# 20. PSORT 的雙面向 Contribution Profile

整體 profile 非常明顯：

```text
資訊工程 Contribution
        中
         +
生物／醫學 Contribution
        強
```

而不是：

```text
資訊工程 Contribution
        強
         +
生物／醫學 Contribution
        中
```

這也是：

> **為什麼 PSORT 對 ICBBB 的適配性高於 ICPRAM / BigComp。**

---

# 21. 為什麼這種 Profile 很適合 ICBBB？

從這 9 篇 Accepted Papers 可以看出：

> ICBBB 並不要求每一篇論文的資訊工程 Contribution 都必須極強。

只要：

* Computational Work 可信
* Experimental Design 嚴謹
* Research Question 清楚
* Biological Contribution 足夠強

一樣可以形成完整的 ICBBB Paper。

Drug-response XGBoost 就接近這條路線。

---

# 22. 如果把 10 篇按資訊工程 Contribution 分組

## 極強

* DICE-ZIKV
* DL-FSG
* StackFeat

## 強

* Single-cell Stability

## 中高

* TCGA-BRCA
* TooT-SS
* K-mer CNN

## 中

* **PSORT**
* GCN + SHAP/IG

## 中低～中

* Drug-response XGBoost

因此 PSORT 大約是：

> **第 7 左右 / 10**

但這裡要特別注意：

> **如果只把 Validation Rigor 單獨拿出來評，PSORT 可能是前 2–4 名。**

---

# 23. 如果按生物／醫學 Contribution 分組

## 極強

* DICE-ZIKV

## 強

* StackFeat
* TCGA-BRCA
* **PSORT**

## 中高～強

* Drug-response XGBoost

## 中高

* Single-cell Stability
* TooT-SS
* DL-FSG
* K-mer CNN

## 中

* GCN + SHAP/IG

因此 PSORT 的 Biological / Medical Contribution 大約是：

> **第 3–4 / 10 等級**

這也與先前：

> **第 3–5**

的判斷一致。

---

# 24. 最乾淨的兩個答案

如果最後只需要記住兩件事：

## 資訊工程 Contribution

> ### **中**

但內部其實是：

> **Novelty = 中低**
>
> **Validation Rigor = 強**

也就是：

```text
Low-to-Moderate Novelty
        +
Strong Methodological Rigor
        ↓
Overall Computational Contribution
        =
中
```

---

## 生物／醫學 Contribution

> ### **強**

約落在這批 10 篇的：

> **前 3–5**

但因為缺少：

* Functional Validation
* Wet-lab Validation
* Causal Validation
* Mechanistic Experiment

所以仍然不到：

> **極強**

---

# 25. 最終結論

PSORT 最適合的 Contribution Profile 是：

| 面向                                   |   最終評價 |
| ------------------------------------ | -----: |
| **資訊工程 Contribution**                |  **中** |
| **Computational Novelty**            | **中低** |
| **Computational / Validation Rigor** |  **強** |
| **生物／醫學 Contribution**               |  **強** |

最精簡的說法就是：

> **資訊工程 Contribution：中**
>
> **其中 Novelty = 中低，但 Validation Rigor = 強。**

以及：

> **生物／醫學 Contribution：強**
>
> **約位於這批 ICBBB Papers 的前 3–5，但由於缺乏 functional / wet-lab / causal validation，因此不到極強。**

---

# 26. 一句話理解 PSORT 為什麼適合 ICBBB

> **PSORT 並不是靠 Computational Novelty 取勝，而是靠嚴謹的 Computational Validation Design，加上強而清楚的 Treatment-response / Precision-medicine Biological Contribution。**

這也剛好解釋：

> **為什麼它很適合 ICBBB，但到了 ICPRAM 或 IEEE BigComp，Methodological Novelty 與 Computational Contribution 的不足就會變得更明顯。**
