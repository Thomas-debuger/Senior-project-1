可以。我這次**只看 4 Results & Discussion，不處理 Methods、Introduction、Conclusion**。

我先從 4.1 一路完整讀到 4.3 結尾，包括 Table 1、Fig. 1、Table 2、Fig. 2 的文字與你對結果的解讀；第一遍只確認你到底做了什麼、哪些是你自己的數據。第二遍才逐句判斷「這句是你自己的 observation，還是需要外部文獻支撐的 biological / novelty claim」。

你的 Results & Discussion 範圍是這裡：

* 4.1 的八個模型與 selected signatures
* 4.2 ADA 的 TMEM120B/ST7
* 4.3 UST 的八條 pathway、GSEA、七個 genes 與 external evidence

## 總結

> **4.1 幾乎完全不用新增 citation。**
>
> **4.2 主要只有最後談「既有 ADA biomarker literature」的段落需要。**
>
> **4.3 才是 citation 最密集的地方，尤其是你宣稱八條 pathway 和 psoriasis biology 有關的那一段。**

而且其中有一句我不建議只「加引用」解決，而是要稍微降強度：

> `The biological processes represented by all eight model-selected pathways have documented relevance to psoriasis biology.`

因為八條 pathway 的文獻證據強度其實不一樣。

* ERBB4、Eph/ephrin、Factor XII–kallikrein 很直接
* cell cycle、ubiquitin、lipid metabolism 主要是 process-level support
* Nectin 則是比較新的初步 psoriasis evidence

把它們全部寫成同等程度的「documented relevance」，會比你的文獻實際證據更強。

以下 citation number 接你的現有 **[1]–[19]**，所以新文獻從 **[20]** 開始。

---

## 第一輪結論：逐段哪些地方要引用

| 位置                                                       | 你現在寫的內容                                          | Citation 判定               | 建議                                                  |
| -------------------------------------------------------- | ------------------------------------------------ | ------------------------- | --------------------------------------------------- |
| **4.1 全段**                                               | ADA/UST 八模型效能、最佳 branch、selected genes/pathways  | **不用**                    | 都是你自己的結果                                            |
| **4.2 Fig. 1 前後**                                        | TMEM120B R/NR separation、ST7 overlap             | **不用**                    | 自己的 PSORT-R observation                             |
| **4.2 single-gene models**                               | AUROC、Recall、Specificity、joint model             | **不用**                    | 自己的 post-hoc results                                |
| **4.2 ST7 complementary information**                    | `raises the possibility…`                        | **不用**                    | 已經用 possibility，且下一句明確說未證明 incremental contribution |
| **4.2 biomarker novelty**                                | TMEM120B/ST7 尚未成為 ADA/PASI75 biomarkers          | **需要 literature context** | 建議重寫並放 **[2,20,30]**                                |
| **4.3 GSEA 數值**                                          | 3 significant + 1 borderline                     | **不用**                    | 自己的 GSEA results                                    |
| **4.3 negative NES 解釋**                                  | negative NES 的方向意義                               | **建議重用 [17]**             | GSEA 方法性解釋                                          |
| **4.3 八條 pathways 生物學解釋**                                | cell cycle、ubiquitin、ERBB4、lipid、Eph、Nectin、FXII | **一定要引用**                 | **[21]–[27]**                                       |
| **4.3 3/8 + borderline synthesis**                       | longitudinal support 統整                          | **不用**                    | 自己的結果                                               |
| **4.3 22 genes → 7 genes**                               | candidate-pool FDR、log2FC                        | **不用**                    | 自己的結果                                               |
| **4.3 leading-edge 解釋**                                  | leading-edge 不要求 pathway overall significant     | **應重用 [17]**              | 這是 GSEA 方法概念                                        |
| **4.3 DisGeNET / Jensen DISEASES**                       | 3/7、6/7 overlap                                  | **一定要引用資料庫**              | **[28,29]**                                         |
| **4.3 `literature review found evidence for all seven`** | 全七基因都有 psoriasis literature                      | **目前不建議原句保留**             | 詳見下面                                                |
| **4.3 尚未成為 UST biomarkers**                              | 七基因 novel to UST response                        | **需要 literature context** | 建議 **[30]**，可搭配既有 **[2]**                           |
| **最後 convergent evidence**                               | pathway + gene-level support                     | **不用再引用**                 | 是你自己的 synthesis                                     |

---

# 4.1 External Predictive Performance

這整節其實寫得很乾淨。

你的：

> ADA Week 0-Gene：AUROC 81.70%、AUPRC 89.20%、Accuracy 84.62%
>
> UST Week 0+Week 1-Pathway：AUROC 85.80%、AUPRC 89.55%、Accuracy 77.78%

以及 TMEM120B/ST7、八條 UST pathways 都是**這篇研究直接產生的結果**。

**全部不要引用別人的 paper。**

甚至不要在這裡突然加 Correa 2017 來比較 accuracy。那比較適合 Discussion deeper comparison 或 Related Work，不應污染 Results 的純結果陳述。

---

# 4.2 ADA：真正需要改的是最後一段

前面的 expression、single-gene model、joint model 全是你自己的 data。

現在真正 literature-dependent 的是：

> Neither TMEM120B nor ST7 has been established as a biomarker of ADA treatment response or Week-12 PASI75.

這是**negative novelty claim**。

一篇 paper 永遠無法「證明全世界沒有人做過」，所以我強烈建議從絕對句改成：

> **To our knowledge, neither TMEM120B nor ST7 has previously been established as a biomarker of ADA treatment response or Week-12 PASI75 in psoriasis.**

然後下一句補真正的 prior literature：

> **Previous studies have instead reported other candidate molecular predictors of ADA response, including early lesional-skin transcriptomic signatures [2] and baseline cDC2 NF-κB activity [20], while broader biomarker reviews have emphasized that proposed systemic-treatment response biomarkers still require further validation [30].**

這三個 citation 是有清楚分工的。

你現有的 **[2] Correa da Rosa 2017** 的確有 ADA-specific early lesional gene-expression prediction，不是硬拉過來。原文研究的確針對 ADA 等四種藥物建立 treatment-specific predictors。

新 **[20] Andres-Ejarque et al. 2021, Nature Communications** 更直接：它的題目就是 baseline cDC2 NF-κB signaling predicts **adalimumab non-response in psoriasis**，而且明確分析 Week-12 response，還有額外 15 人 independent validation cohort。

**[30] Corbett et al. 2022, BJD** 系統整理 psoriasis systemic-treatment response biomarkers，最後指出 ADA prioritized cellular biomarker 是 cDC2 NF-κB，而候選 biomarker 整體仍沒有足夠 evidence 直接投入臨床。

所以你的整段我會變成：

> Neither TMEM120B nor ST7 has, **to our knowledge**, previously been established as a biomarker of ADA treatment response or Week-12 PASI75 in psoriasis. Previous studies have instead reported other candidate molecular predictors of ADA response, including early lesional-skin transcriptomic signatures [2] and baseline cDC2 NF-κB activity [20], while broader biomarker reviews indicate that proposed systemic-treatment response biomarkers still require further validation [30]. TMEM120B and ST7 are therefore more appropriately interpreted as candidate response-associated genes identified in this study rather than validated pharmacological-response biomarkers.

我覺得這比你現在一句「沒有被 established」更能 defend。

---

# 4.3：前面的 GSEA Results 基本不用 Citation

這段：

> Three of the eight pathways showed significant enrichment...
>
> Regulation of FXIIa... borderline...
>
> remaining four did not reach FDR < 0.05.

全部是你自己的 GSEA 結果。

**不用引用。**

但這句：

> negative NES values indicate enrichment toward genes showing relatively lower Week 0-to-Week 1 changes in responders than in non-responders.

我會在句尾重用：

> **[17]**

因為這是在解釋 GSEA enrichment-score direction，而不是單純報自己的數值。Subramanian 2005 就是 GSEA 原始方法論文。

---

# 最需要處理的是「八條 Pathway 都跟 Psoriasis 有關」這段

你現在一口氣說八條 pathway 全都有 documented relevance。

我不建議直接保留原句，然後後面塞七篇文獻。

原因是：

> **「exact Reactome pathway 已被 psoriasis 文獻證實」**

和

> **「這個 pathway 所代表的 biological process 已有 psoriasis evidence」**

是不一樣的。

例如我們確實有很好的 evidence 說 psoriasis keratinocytes 有 abnormal cell-cycle control，但這不等於有 paper 已經直接驗證你的 exact Reactome **`Polo-like kinase mediated events`** 是 psoriasis biomarker。

所以我會把第一句改成：

> **The eight model-selected pathways map onto biological processes with varying degrees of prior relevance to psoriasis.**

這句精準很多。

接著我建議整段直接改成這樣：

> **The eight model-selected pathways map onto biological processes with varying degrees of prior relevance to psoriasis. The Polo-like kinase- and Cyclin D-related pathways represent cell-cycle processes, and dysregulated cell-cycle control is closely associated with keratinocyte hyperproliferation in psoriasis [21]. Synthesis of active ubiquitin is biologically consistent with reported involvement of the ubiquitin–proteasome system in psoriatic keratinocyte proliferation and inflammatory signaling [22]. ERBB4 has been directly linked to keratinocyte proliferation and inflammatory-mediator production in psoriasis [23]. Fatty acyl-CoA biosynthesis is consistent with disease-associated alterations in epidermal lipid metabolism and ELOVL-family regulation in psoriatic skin [24]. Eph/ephrin signaling has been shown to be dysregulated in psoriatic epidermis [25]. Nectin/Necl trans heterodimerization represents cell–cell adhesion biology; notably, increased Nectin-4 expression has recently been reported in psoriatic lesional keratinocytes [26]. Finally, the Factor XII–prekallikrein system has been experimentally implicated in psoriatic inflammation [27].**

這版我敢讓 reviewer 一篇一篇點進去查。

---

## [21] Cell Cycle

**Pellarin et al. 2025, Signal Transduction and Targeted Therapy** 有專門的 psoriasis subsection，直接寫到 dysregulated CDK activity 會加速 cell-cycle progression 與 keratinocyte hyperproliferation，而且引用 human psoriatic epidermis 中 CDK2–cyclin E activity 上升的資料。

所以它可以支撐：

> cell-cycle dysregulation ↔ keratinocyte hyperproliferation

但我**不會**把它寫成：

> Polo-like kinase mediated events has previously been validated in psoriasis.

因為它沒有證明這件事。

---

## [22] Ubiquitin

**Zhou et al. 2022, Cell Death & Disease** 是 psoriasis keratinocyte pathogenesis review，而且直接有一節說 ubiquitin–proteasome system 在 psoriasis pathogenesis 中具重要作用，包括 POMP、TRIM21、NEDD4L 等與 keratinocyte proliferation / STAT3 相關機制。

所以它能合理支撐：

> `Synthesis of active ubiquitin` 與已知 psoriasis ubiquitin biology **biologically consistent**

但同樣不是宣稱 exact Reactome pathway 已被驗證。

---

## [23] ERBB4

這篇非常直接。

**Huang et al. 2021, Cell Death & Disease** 題目本身就是：

> *MiR-193b-3p–ERBB4 axis regulates psoriasis pathogenesis via modulating cellular proliferation and inflammatory-mediator production of keratinocytes.*

不是擦邊引用。

所以你現在：

> Nuclear signaling by ERBB4 has been linked to keratinocyte proliferation and inflammatory-mediator production in psoriasis.

這句可以非常放心地放 **[23]**。

---

## [24] Fatty Acyl-CoA / ELOVL

這篇也非常適合。

**Merleev et al. 2022, JCI Insight** 做 epidermal lipidomics + transcriptomics，直接描述 psoriasis-specific epidermal lipid alterations；更重要的是，他們特別研究了 **ELOVL4**，而且 ELOVL4 expression cluster 中甚至包括 **ELOVL7**。

作者又在 psoriasis lesional RNA-seq 中檢驗 ELOVL4-related expression，並把它連到 lipid synthesis、skin barrier 與 inflammatory genes。

這和你後面剛好選到：

> **ELOVL4 + ELOVL7**

非常有價值。

所以 [24] 不只是替 pathway biology 背書，之後 Discussion 談七個 candidate genes 時也可以再次引用。

---

## [25] Eph/Ephrin

我真的有嘗試找更新的，但我最後還是選 **2013 JID**。

原因不是找不到新 paper 就隨便拿舊的，而是這篇太直接：

> *Alteration of the EphA2/Ephrin-A Signaling Axis in Psoriatic Epidermis.*

它真的拿 psoriasis patient skin biopsy 做 microarray、qPCR、IHC、ELISA，發現 EphA family expression 改變，EphA2 上升、ephrin-A ligand 降低，並進一步做 keratinocyte differentiation/proliferation experiments。

所以雖然是 2013 年，**它比一篇 2025 generic Eph review 更適合你的句子**。

這就是你之前要求我的原則：

> **準確 > 年份**

---

## [26] Nectin

這一條原本是我最不放心的。

後來找到 **Nakajima et al. 2024, International Journal of Dermatology**：

> *Increased Nectin-4 expression in atopic dermatitis and psoriasis: a preliminary study.*

它的確直接研究 psoriasis lesional skin/sera，而且 Nectin-4 本身就是 immunoglobulin-like **cell-adhesion molecule**。

但 paper 自己就叫：

> **preliminary study**

所以你的 wording 千萬不要寫成：

> Nectin/Necl pathway is well established in psoriasis.

我上面替你改成：

> **Nectin/Necl trans heterodimerization represents cell–cell adhesion biology; notably, increased Nectin-4 expression has recently been reported...**

這樣證據強度才對。

---

## [27] FXII / Prekallikrein

這個非常漂亮，而且很新。

**Zhang et al. 2024, British Journal of Pharmacology** 直接發現 Factor XII / prekallikrein activation 促進 psoriasis-like inflammation，FXII 或 prekallikrein deficiency 會減輕 lesion，而且 bradykinin pathway 有機制性證據。

所以：

> Regulation of FXIIa and plasma kallikrein activity is consistent with evidence implicating the Factor XII–kallikrein system in psoriatic inflammation **[27]**.

可以留。

---

# 3/8 Significant + Fourth Borderline 不需要引用

這段：

> three of eight received clear pathway-level support...
>
> fourth near-significant...

完全是你自己的結果。

**不要引用別人。**

同樣，22 genes → 7 genes、正負 interaction effects、Table 2 也全部不用外部文獻。

---

# Leading-Edge 那一句應該補 [17]

你寫：

> Leading-edge membership itself does not require the overall pathway to reach GSEA significance; rather, it identifies the subset of genes contributing most strongly to the observed enrichment signal.

這是**方法學事實**，不是你自己的結果。

所以：

> ...contributing most strongly to the observed enrichment signal **[17]**.

就好。

不需要新增 paper，因為 [17] 已經是 GSEA 原始文獻。

---

# DisGeNET / Jensen DISEASES 這句一定要引用資料庫

你現在：

> Three of the seven genes overlapped the DisGeNET psoriasis gene-disease association set, and six of seven were represented in the Jensen DISEASES psoriasis text-mining gene set.

建議直接：

> Three of the seven genes overlapped the DisGeNET psoriasis gene–disease association set **[28]**, and six of seven were represented in the Jensen DISEASES psoriasis text-mining gene set **[29]**.

[28] 是 DisGeNET 官方 resource paper。

[29] 就是 DISEASES 2.0 的正式 database paper，明確整合 text mining、curated data 與其他 disease–gene associations。

這裡不要引用一篇「某研究用了 DisGeNET」；引用資料庫本身最好。

---

# 我最建議你刪／改的是「Literature Review Found Evidence for All Seven」

你目前寫：

> In addition, the literature review identified psoriasis-related evidence for all seven genes to varying degrees.

這句不是一定錯。

但它會產生一個很大的 reference burden：

* PGR 一篇
* A2M 一篇
* SPARC 一篇
* S100B 一篇
* APOE 一篇
* ELOVL4 一篇
* ELOVL7 一篇

而且我真的逐個去查後，**七個 gene 的 literature strength 差很多**。

例如：

* ELOVL4/ELOVL7 有相當直接的 JCI Insight evidence
* SPARC 可以在 2024 *Nature Communications* longitudinal psoriasis scRNA-seq 裡找到
* APOE 甚至有非常新的 2026 *Immunity* longitudinal psoriasis atlas，指出 IL34+/APOE+ fibroblasts 具有 inflammatory properties
* S100B 的直接 human psoriasis paper 就比較舊、期刊層級也沒那麼高
* PGR、A2M、ELOVL7 的證據又各自屬於不同類型

所以如果目標是 ICBBB Full Paper，我反而會**刪掉這一句**。

留下：

> External psoriasis-related evidence further supported the biological relevance of these candidates. Three of the seven genes overlapped the DisGeNET psoriasis gene-disease association set [28], and six of seven were represented in the Jensen DISEASES psoriasis text-mining gene set [29].

這已經夠漂亮。

如果之後你有 Supplementary Materials，我才會做一張：

| Gene   | Psoriasis Evidence | Paper | Evidence Type |
| ------ | ------------------ | ----- | ------------- |
| PGR    |                    |       |               |
| A2M    |                    |       |               |
| SPARC  |                    |       |               |
| S100B  |                    |       |               |
| APOE   |                    |       |               |
| ELOVL4 |                    |       |               |
| ELOVL7 |                    |       |               |

逐一列七個。

這比主文一句「全部都有文獻」然後塞七、八個 citation 乾淨很多。

---

# UST Biomarker Novelty 那句也要改成「To Our Knowledge」

你現在：

> In contrast, these genes have not been established as biomarkers of UST treatment response.

這跟 ADA 一樣，是 negative literature claim。

我會改：

> **To our knowledge, none of these seven genes has previously been established as a biomarker of UST treatment response. Previous biomarker studies have instead highlighted other candidates, most notably HLA-C*06:02 and IL1B-related variation [30].**

這句很有文獻基礎。

**Corbett et al. 2022 BJD** 系統性 scoping review 納入 71 studies；它整理 UST response biomarker literature 後，優先 candidate 就是 **HLA-C*06:02** 與 **IL1B locus variation**，而且作者明確強調還沒有足以直接臨床使用的 response biomarker。

甚至它整理的既有 UST studies 包括 Week-12 / PASI75 的 HLA-C*06:02 evidence，所以和你的 endpoint 也不是很遠。

2025/2026 確實也有更新的 psoriasis stratification review，仍主要討論 HLA-C*06:02、clinical variables、drug concentration 等已知 predictors，而不是你這七個 genes。

不過因為 narrative/mini-review 的 evidence rigor 不如 BJD scoping review，我**沒有為了年份新而把 [30] 換掉**。

---

# 所以最後 4.3 的最後一段我建議變成

> External psoriasis-related evidence further supported the biological relevance of these candidates. Three of the seven genes overlapped the DisGeNET psoriasis gene–disease association set [28], and six of seven were represented in the Jensen DISEASES psoriasis text-mining gene set [29]. **To our knowledge, none of these seven genes has previously been established as a biomarker of UST treatment response; prior biomarker studies have instead highlighted other candidates, including HLA-C*06:02 and IL1B-related variation [30].** Their potential novelty therefore lies not in representing entirely new psoriasis-associated genes, but in linking their early Week 0-to-Week 1 expression changes to differential UST response within an externally predictive pathway signature.
>
> Taken together, the significant enrichment of three model-selected pathways, borderline enrichment of a fourth, and complete leading-edge overlap of all seven response-associated candidate genes provide convergent pathway- and gene-level support for the biological relevance of the UST predictive signature. These findings therefore identify a biologically plausible set of early treatment-response signals that warrants further independent validation as candidate biomarkers of UST response.

最後一段不用再 citation。

那是**你的 inference from your own results**，而且你已經用了：

* `biologically plausible`
* `warrants further independent validation`
* `candidate biomarkers`

語氣很安全。

---

# 最終建議的 References

下面引用數我盡量統一成 **OpenAlex 截至 2026-09-19 的 snapshot**。

Citation count 本身會持續變動；[26] 因 OpenAlex 沒有可靠 surfaced count，我寧可明確標示另一來源，不替它亂造數字。

Q 統一以 **2025 JCR/JIF quartile** 為主。

| Ref      | 文獻                                                                                                                                                                     | 年份 / 期刊                                          |                          引用數 | 2025 JCR | 為什麼用                                                                                                         |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ | ---------------------------: | :------: | ------------------------------------------------------------------------------------------------------------ |
| **[2]**  | **Correa da Rosa et al. — Shrinking the Psoriasis Assessment Gap: Early Gene-Expression Profiling Accurately Predicts Response to Long-Term Treatment**                | 2017, *Journal of Investigative Dermatology*     |              **94** OpenAlex |  **Q1**  | 最接近你的早期 lesional transcriptomic ADA/UST treatment-response 前作；4.2 ADA context 可重用。                           |
| **[17]** | **Subramanian et al. — Gene set enrichment analysis: A knowledge-based approach for interpreting genome-wide expression profiles**                                     | 2005, *PNAS*                                     |          **56,658** OpenAlex |  **Q1**  | 支撐 NES direction 與 leading-edge interpretation；已經在你 bibliography，不新增。                                        |
| **[20]** | **Andres-Ejarque et al. — Enhanced NF-κB signaling in type-2 dendritic cells at baseline predicts non-response to adalimumab in psoriasis**                            | 2021, *Nature Communications*                    |              **51** OpenAlex |  **Q1**  | 非常直接的 ADA response biomarker paper；Week-12 response + independent cohort。                                    |
| **[21]** | **Pellarin et al. — Cyclin-dependent protein kinases and cell cycle regulation in biology and disease**                                                                | 2025, *Signal Transduction and Targeted Therapy* |             **225** OpenAlex |  **Q1**  | 有專門 psoriasis section，直接支撐 dysregulated cell-cycle/CDK activity → keratinocyte hyperproliferation。           |
| **[22]** | **Zhou et al. — Advances in the pathogenesis of psoriasis: from keratinocyte perspective**                                                                             | 2022, *Cell Death & Disease*                     |             **611** OpenAlex |  **Q1**  | psoriasis-specific review，直接討論 ubiquitin–proteasome system 與 keratinocyte proliferation/inflammation。        |
| **[23]** | **Huang et al. — MiR-193b-3p–ERBB4 axis regulates psoriasis pathogenesis via modulating cellular proliferation and inflammatory-mediator production of keratinocytes** | 2021, *Cell Death & Disease*                     |              **38** OpenAlex |  **Q1**  | 幾乎逐字支撐你 ERBB4 那句；非常直接。                                                                                       |
| **[24]** | **Merleev et al. — Biogeographic and disease-specific alterations in epidermal lipid composition and single-cell analysis of acral keratinocytes**                     | 2022, *JCI Insight*                              |              **27** OpenAlex |  **Q1**  | psoriasis epidermal lipidomics；特別分析 ELOVL4，而且 ELOVL4 cluster 包含 ELOVL7，和你結果高度相關。                             |
| **[25]** | **Gordon et al. — Alteration of the EphA2/Ephrin-A Signaling Axis in Psoriatic Epidermis**                                                                             | 2013, *Journal of Investigative Dermatology*     |              **61** OpenAlex |  **Q1**  | 雖舊，但直接以 psoriasis skin 證明 Eph/ephrin dysregulation，比新的 generic Eph 文獻更精確。                                    |
| **[26]** | **Nakajima et al. — Increased Nectin-4 expression in atopic dermatitis and psoriasis: a preliminary study**                                                            | 2024, *International Journal of Dermatology*     | **0*** ResearchGate snapshot |  **Q1**  | 目前找到最直接的 psoriasis–Nectin evidence；但 paper 本身是 preliminary letter，因此 wording 必須保守。                           |
| **[27]** | **Zhang et al. — Factor XII and prekallikrein promote microvascular inflammation and psoriasis in mice**                                                               | 2024, *British Journal of Pharmacology*          |              **60** OpenAlex |  **Q1**  | 直接的 FXII/prekallikrein psoriasis mechanistic evidence，和你的 pathway 非常契合。                                      |
| **[28]** | **Piñero et al. — The DisGeNET knowledge platform for disease genomics: 2019 update**                                                                                  | 2020 issue, *Nucleic Acids Research*             |           **2,753** OpenAlex |  **Q1**  | 你直接用了 DisGeNET gene–disease set，所以應引用 database source。                                                       |
| **[29]** | **Grissa et al. — DISEASES 2.0: a weekly updated database of disease–gene associations from text mining and data integration**                                         | 2022, *Database*                                 |             **136** OpenAlex |  **Q2**  | Jensen DISEASES 的直接方法/資料庫來源。雖 Q2，但這是 authoritative source，不應為了 Q1 換成別人使用它的 paper。                            |
| **[30]** | **Corbett et al. — Biomarkers of systemic treatment response in people with psoriasis: a scoping review**                                                              | 2022, *British Journal of Dermatology*           |              **42** OpenAlex |  **Q1**  | 直接整理 ADA/UST treatment-response biomarkers；UST prioritized candidates 包括 HLA-C*06:02、IL1B，而且強調仍需 validation。 |

> * **[26]** 我特別不把 `0` 當成像 OpenAlex 那樣完整的 citation count。ResearchGate 目前顯示 0，並寫明尚未 resolve citations；所以如果之後要正式做 citation count table，這篇應標成 **`0 (ResearchGate snapshot; database coverage uncertain)`**，而不是裝成非常精確的 0。

---

## 有沒有哪個地方「真的選不出唯一一篇」？

這次其實**幾乎沒有**，因為我刻意替每一句找最直接的 evidence，而不是看到三篇差不多就全部塞。

唯一比較特殊的是 **ADA biomarker context 的 [2] + [20] + [30]**，但它們並不是三選一，而是功能不同：

* **[2]**：和你最像的 lesional transcriptomic prediction 前作
* **[20]**：很直接的 Week-12 ADA molecular biomarker + independent validation
* **[30]**：broader biomarker landscape 的 scoping review

三篇是在回答不同問題，所以我才認為 4.2 那兩句同時保留有價值。

其他地方我都選得出來。例如：

* lipid → **[24]**
* cell cycle → **[21]**
* ERBB4 → **[23]**
* Eph → **[25]**
* Factor XII → **[27]**

---

# 最後，我最建議你真的改的只有兩種句型

第一種是：

> **“all eight pathways have documented relevance”**

改成：

> **“The eight model-selected pathways map onto biological processes with varying degrees of prior relevance to psoriasis.”**

因為你的 literature support 確實是**強弱不一**，這樣最學術誠實。

第二種是：

> **“these genes have not been established…”**

全部改成：

> **“To our knowledge, ... has/have not previously been established…”**

因為沒有任何 citation 能數學上證明「全世界完全沒有人做過」。

你能做的是完整搜尋後合理陳述 `to our knowledge`，再用 [20]/[30] 這種專門 treatment-response literature 告訴 reviewer **目前 established/candidate landscape 主要是哪些東西**。

---

如果按這個版本改，我認為你的 **Results & Discussion citation chain 已經會比單純亂塞一堆 2025 paper 扎實很多**：

* 自己的數據保持乾淨
* biological interpretation 才引用外部研究
* database evidence 引用原始資料庫
* novelty claims 使用 `to our knowledge`
* exact pathway evidence 與 process-level evidence 明確區分
