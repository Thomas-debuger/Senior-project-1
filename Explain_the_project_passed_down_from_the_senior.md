# Q1：這是我們交接到的專題，我現在只有一點基礎，詳細告訴我這5頁在做甚麼，教會我讓我直接無縫銜接

可以，這 5 頁其實是在交代一個完整的 RNA-seq 生醫資訊專題流程。你可以把它理解成：

> **用 RNA-seq 資料比較異位性皮膚炎 AD 和乾癬 PSO 的病灶皮膚 LS、非病灶皮膚 NL，找出差異表現基因 DEGs，再做路徑分析與免疫特徵分析，最後希望建立一個能判斷 NL 是否有轉成 LS 風險的模型。**

而你們現在選到的 **GSE121212** 很符合這個專題，因為它的 GEO 標題就是 **Atopic Dermatitis, Psoriasis and healthy control RNA-seq cohort**，資料型態是 **Expression profiling by high throughput sequencing**，也就是 RNA-seq。GEO 摘要也提到這個資料集包含 AD 與 psoriasis 樣本，用來研究兩者共同與不同的分子特徵。([美國國立生物技術資訊中心][1])

---

# 先把關鍵名詞搞懂

你只要先記住這幾個詞，後面就能接上。

| 名詞               | 意思                                         | 在你們專題中的角色              |
| ---------------- | ------------------------------------------ | ---------------------- |
| AD               | Atopic Dermatitis，異位性皮膚炎                   | 研究疾病之一                 |
| PSO              | Psoriasis，乾癬                               | 研究疾病之一                 |
| LS               | Lesional skin，病灶皮膚                         | 已經發炎、有明顯病灶的皮膚          |
| NL               | Non-lesional skin，非病灶皮膚                    | 外觀看似正常，但可能已有免疫異常       |
| DEG              | Differentially Expressed Gene，差異表現基因       | 兩組樣本之間表現量顯著不同的基因       |
| RNA-seq          | RNA 定序                                     | 用來量測基因表現量              |
| DESeq2           | RNA-seq 差異表現分析工具                           | 用 raw counts 找 DEGs    |
| TPM              | Transcripts Per Million                    | 標準化後的基因表現量，適合 ssGSEA   |
| ssGSEA           | Single-sample Gene Set Enrichment Analysis | 把基因表現轉成免疫路徑或細胞特徵分數     |
| Pathway analysis | 路徑富集分析                                     | 看 DEGs 主要落在哪些生物功能或免疫路徑 |

---

# 第 1 頁：研究背景與動機 — 為什麼要研究 AD 和 PSO？

這頁在說：

## 1. AD 和 PSO 都是常見慢性發炎皮膚病

投影片寫：

> 常見的慢性炎症皮膚病：異位性皮膚炎 AD 與乾癬 PSO

這代表你們研究的主角是兩種皮膚發炎疾病。

AD 和 PSO 都會造成皮膚發炎、紅腫、免疫活化，但它們背後的免疫機制不完全一樣。你們不是只要分類疾病名稱，而是要理解：

> 為什麼 AD 和 PSO 都會發炎，但基因與免疫路徑會不同？

---

## 2. AD 與 PSO 的免疫機制不同

投影片寫：

> AD 由 Th2/Th22 主導；PSO 由 Th1/Th17 主導。

你可以這樣理解：

### AD：偏 Th2 / Th22

AD 常和皮膚屏障異常、過敏反應、IL-13、IL-4 等免疫路徑有關。

### PSO：偏 Th1 / Th17

PSO 常和 IL-17、IL-23、TNF 等發炎路徑有關。

GSE121212 對應的研究論文也指出，AD 和 psoriasis 雖然有共享的發炎成分，但兩者有不同的 cytokine signature，而且 AD 顯示 IL-13 dominant 的特徵。([ScienceDirect][2])

所以這頁的意思是：

> AD 和 PSO 臨床上都是皮膚發炎，但背後免疫機制不同，因此可以用 RNA-seq 找出它們在基因表現上的差異。

---

## 3. 兩者也有共同性

投影片寫：

> 兩者臨床表現雖不同，但皆涉及免疫交互作用，並共享部分發炎途徑。

也就是說：

AD 和 PSO 不完全一樣，但也不是完全無關。

你們的研究價值就在這裡：

> 找出哪些基因或免疫路徑是 AD/PSO 共同發炎特徵，哪些是 AD 特有，哪些是 PSO 特有。

---

## 4. NL 非病灶皮膚的「隱藏危機」

這是這頁最重要的地方。

投影片寫：

> 病灶皮膚 LS：具明顯的炎症與免疫活化。
> 非病灶皮膚 NL：外觀看似正常，但已隱含「皮膚屏障異常」與「輕度免疫活性」，隨時有惡化成病灶 LS 的風險。

這個概念很重要。

一般人會以為：

```text
LS = 生病
NL = 正常
```

但你們專題想說的是：

```text
LS = 已經明顯病變
NL = 表面正常，但可能已經有早期分子異常
```

所以你們不是只看「病灶 vs 正常」，而是特別關注：

> NL 是否已經有一些接近 LS 的基因或免疫特徵？

這就會連到後面的「NL 惡化風險模型」。

---

# 第 2 頁：研究缺口與研究目的

這頁是在說：

> 以前的研究還不夠，所以我們要做這個專題。

---

## 1. 目前研究缺口

投影片寫：

> 對 AD 與 PSO 中，NL 與 LS 之間的免疫差異理解仍有限。

也就是說，很多研究可能已經知道：

```text
AD LS 跟健康皮膚不同
PSO LS 跟健康皮膚不同
```

但比較少深入問：

```text
AD 的 NL 和 LS 差在哪？
PSO 的 NL 和 LS 差在哪？
AD 的 NL 是否比 PSO 的 NL 更接近 LS？
哪些 NL 樣本其實已經有病灶化風險？
```

---

## 2. 臨床上缺乏可靠模型

投影片寫：

> 臨床上缺乏可靠的模型，無法有效預測 NL 向 LS 轉變的風險。

這句話就是你們專題後半段的核心。

意思是：

目前醫生看病時，通常可以看出哪裡已經是病灶 LS，但對於「看起來還正常的皮膚 NL」，很難判斷它未來會不會惡化。

所以你們希望用 RNA-seq 和機器學習補上這個缺口。

---

## 3. 本研究目的

投影片列了三點：

### 第一：特徵比較

> 深入比較 AD 與 PSO 中，NL 與 LS 的免疫特徵差異。

也就是做這些比較：

```text
AD_LS vs AD_NL
PSO_LS vs PSO_NL
PSO_LS vs AD_LS
可能也可以做 PSO_NL vs AD_NL
```

最基本就是你教授說的三個 DEG 分析：

```text
1. PSO 的 LS 與 NL 的 DEGs
2. AD 的 LS 與 NL 的 DEGs
3. PSO 與 AD 的 DEGs
```

其中第三個建議定義成：

```text
PSO_LS vs AD_LS
```

比較乾淨，因為這是在比較兩種疾病的病灶狀態。

---

### 第二：建立模型

> 打造能評估「NL 惡化風險高低」的預測模型。

也就是未來可能會做：

```text
輸入：某個 NL 樣本的基因表現或免疫分數
輸出：這個 NL 樣本比較像健康、比較像 NL，還是比較接近 LS？
```

這可以包裝成：

```text
lesional-like risk stratification
```

也就是「病灶化風險分層」。

---

### 第三：預期貢獻

> 提升疾病早期的風險評估能力與臨床鑑別診斷的精準度。

簡單講就是：

如果你能從看似正常的 NL 皮膚中找出早期免疫異常，就可能比肉眼或傳統診斷更早發現疾病惡化風險。

---

# 第 3 頁：研究方法一 — 資料來源、前處理、比對與定量

這頁開始進入實作流程。

它在說你們的 RNA-seq 資料怎麼從原始資料變成可以分析的基因表現矩陣。

---

## 1. 資料來源與前處理

投影片寫：

> 樣本來源：利用異位性皮膚炎 AD 與乾癬 PSO 患者之病灶 LS 與非病灶 NL 皮膚組織的 RNA-seq 資料集。

對你們現在來說，就是：

```text
資料集：GSE121212
疾病：AD、PSO
皮膚狀態：LS、NL
資料型態：RNA-seq
```

GEO 上 GSE121212 的 title 就是 AD、Psoriasis 和 healthy control RNA-seq cohort，且 experiment type 是 high-throughput sequencing。([美國國立生物技術資訊中心][1])

---

## 2. FASTQ 是什麼？

投影片寫：

> 針對原始序列 FASTQ 進行品質檢測，並剪除低品質片段。

RNA-seq 最原始的資料通常是 FASTQ 檔。

你可以把 FASTQ 想成：

```text
一堆 RNA 被定序後得到的短片段 reads
```

每一條 read 會有：

```text
1. read ID
2. 序列，例如 ACTGACTG...
3. 分隔符號
4. 品質分數
```

所以 FASTQ 還不是基因表現量，它只是原始序列。

---

## 3. 品質檢測 QC

在做正式分析前，要先檢查 FASTQ 品質。

通常會用：

```text
FastQC
MultiQC
```

看：

```text
read quality 好不好
有沒有 adapter contamination
GC content 是否異常
序列長度是否合理
有沒有低品質 reads
```

如果品質不好，就要 trim。

---

## 4. 剪除低品質片段

這步通常用：

```text
Trimmomatic
Cutadapt
fastp
```

目的是把低品質 reads 或 adapter 切掉。

流程概念是：

```text
Raw FASTQ
→ QC
→ trimming
→ Clean FASTQ
```

---

## 5. STAR 1-pass 比對

投影片寫：

> 使用 STAR 1-pass 模式將序列比對至人類參考基因組 GRCh38。

STAR 是 RNA-seq 常用 aligner。

它的任務是把 reads 對回人類基因組。

簡單講：

```text
FASTQ 裡面的 reads
→ STAR
→ 找出每條 read 來自人類基因組哪個位置
```

輸出通常是：

```text
BAM 檔
```

BAM 就是比對結果。

---

## 6. GRCh38 是什麼？

GRCh38 是人類參考基因組版本。

也就是：

```text
人類基因組地圖
```

STAR 需要知道 reads 要對到哪張地圖上，所以會指定 GRCh38。

---

## 7. Gene expression counts 是什麼？

投影片寫：

> 獲得各樣本的基因表現量計數 Gene expression counts。

這是 DESeq2 最需要的東西。

Gene count matrix 長這樣：

| gene  | sample1 | sample2 | sample3 |
| ----- | ------: | ------: | ------: |
| IL13  |     120 |      95 |     300 |
| IL17A |       5 |     600 |     580 |
| KRT16 |      20 |     900 |     850 |

每一格代表：

> 某個基因在某個樣本中被 reads 支持的數量。

DESeq2 要吃的是這種 **raw integer counts**，不是 TPM、FPKM，也不是 log-normalized expression。

---

## 你現在要注意一件事

如果你們是直接從 GSE121212 下載 GEO supplementary count matrix，那你可能不用自己跑：

```text
FASTQ → STAR → counts
```

因為別人可能已經整理好 counts 了。

你的實作路線可能分成兩種：

### 路線 A：從 FASTQ 重跑

```text
SRA/FASTQ
→ FastQC
→ trimming
→ STAR
→ featureCounts
→ count matrix
→ DESeq2
```

這比較完整，但很花時間。

### 路線 B：直接用 GEO 提供的 count matrix

```text
GEO supplementary counts
→ 整理 metadata
→ DESeq2
→ DEGs
→ pathway / ssGSEA
```

你現在要無縫銜接，通常先走 **路線 B**，比較實際。

---

# 第 4 頁：研究方法二 — DEGs、Pathway、ssGSEA

這頁是在說：

> 拿到 gene expression counts 之後，要怎麼找差異基因和免疫特徵。

---

## Part A：DEGs & Pathway Analysis

投影片寫：

> DEGs 篩選：濾除低表達基因後，使用 DESeq2 進行差異表達基因分析。

這是你現在最該先接起來的部分。

---

## 1. 為什麼要濾除低表達基因？

RNA-seq 裡面會有很多基因幾乎沒有表現。

例如：

| gene  | sample1 | sample2 | sample3 |
| ----- | ------: | ------: | ------: |
| GeneA |       0 |       0 |       1 |
| GeneB |       0 |       2 |       0 |
| GeneC |     500 |     600 |     550 |

GeneA、GeneB 這種低表達基因很容易造成統計不穩，所以通常先移除。

常見篩法：

```r
keep <- rowSums(counts(dds) >= 10) >= 3
dds <- dds[keep, ]
```

意思是：

> 至少有 3 個樣本 count >= 10，才保留這個基因。

---

## 2. DESeq2 在做什麼？

DESeq2 的工作是：

```text
比較兩組樣本的 gene counts
→ 判斷哪些基因表現量顯著不同
```

例如：

```text
AD_LS vs AD_NL
```

DESeq2 會對每個基因算出：

| 欄位             | 意思          |
| -------------- | ----------- |
| baseMean       | 平均表現量       |
| log2FoldChange | 兩組之間差多少     |
| lfcSE          | log2FC 的標準誤 |
| stat           | 統計量         |
| pvalue         | p 值         |
| padj           | 多重檢定校正後 p 值 |

你最常用的是：

```text
log2FoldChange
padj
```

---

## 3. log2FoldChange 怎麼看？

假設你做：

```text
AD_LS vs AD_NL
```

如果某基因：

```text
log2FoldChange = 2
```

代表：

```text
AD_LS 比 AD_NL 高 2^2 = 4 倍
```

如果：

```text
log2FoldChange = -1
```

代表：

```text
AD_LS 是 AD_NL 的 2^-1 = 0.5 倍
```

也就是 AD_LS 比 AD_NL 低一半。

---

## 4. padj 是什麼？

RNA-seq 一次會測幾萬個基因。

如果每個基因都用 p < 0.05，會有大量假陽性。

所以要做多重檢定校正，常見是 Benjamini-Hochberg FDR。

DESeq2 的 `padj` 就是調整後的 p 值。

常見 DEG 門檻：

```text
padj < 0.05
abs(log2FoldChange) > 1
```

意思是：

```text
校正後顯著
而且表現差異至少 2 倍以上
```

---

## 5. 你們三個 DESeq2 比較

你教授要的三個分析可以定義成：

### 比較 1：PSO 的 LS vs NL

```text
PSO_LS vs PSO_NL
```

目的：

> 找出乾癬病灶皮膚相對於乾癬非病灶皮膚的差異基因。

解讀：

```text
log2FC > 0：PSO_LS 高於 PSO_NL
log2FC < 0：PSO_LS 低於 PSO_NL
```

---

### 比較 2：AD 的 LS vs NL

```text
AD_LS vs AD_NL
```

目的：

> 找出異位性皮膚炎病灶皮膚相對於非病灶皮膚的差異基因。

解讀：

```text
log2FC > 0：AD_LS 高於 AD_NL
log2FC < 0：AD_LS 低於 AD_NL
```

---

### 比較 3：PSO 與 AD 的 DEGs

這個要定義清楚。

我建議你用：

```text
PSO_LS vs AD_LS
```

原因是：

> 比較疾病差異時，最好固定皮膚狀態，否則 LS/NL 會混在一起干擾。

解讀：

```text
log2FC > 0：PSO_LS 高於 AD_LS
log2FC < 0：AD_LS 高於 PSO_LS
```

---

## 6. Pathway analysis 是什麼？

投影片寫：

> 針對顯著的 DEGs 進行路徑富集分析，探討與疾病相關的免疫與分子機制。

你可以這樣理解：

DESeq2 給你一堆基因，例如：

```text
IL13, CCL17, CCL18, KRT16, S100A7, DEFB4A...
```

但只看基因名很難解釋。

所以 pathway analysis 會問：

> 這些基因是不是集中在某些生物功能或免疫路徑？

例如可能發現：

```text
cytokine-cytokine receptor interaction
Th17 cell differentiation
JAK-STAT signaling pathway
skin barrier function
keratinization
inflammatory response
```

常用工具：

```text
clusterProfiler
enrichR
g:Profiler
DAVID
ReactomePA
```

你報告時可以說：

> 我們將顯著 DEGs 進行 GO、KEGG 或 Reactome enrichment analysis，以解析 AD 與 PSO 中與免疫活化、皮膚屏障、發炎反應相關的分子路徑。

---

# Part B：ssGSEA

投影片寫：

> 將基因表現量標準化並轉換為 TPM。
> 執行單一樣本基因集富集分析 ssGSEA，深入比較 LS vs NL 以及 AD vs PSO 之間的表現差異。

這是比較進階但很重要的部分。

---

## 1. 為什麼 DESeq2 用 counts，但 ssGSEA 用 TPM？

這點一定要搞清楚。

### DESeq2

DESeq2 要的是：

```text
raw counts
```

因為它自己會做 normalization 和統計模型。

### ssGSEA

ssGSEA 通常用：

```text
TPM / normalized expression
```

因為它是在每個 sample 裡面看一組基因整體表現高不高。

所以流程是：

```text
Raw counts → DESeq2 → DEGs
Raw counts → TPM → ssGSEA → immune enrichment score
```

兩條路是並行的，不要混用。

---

## 2. ssGSEA 到底在算什麼？

假設有一個 gene set 叫：

```text
Th17 pathway
```

裡面包含：

```text
IL17A, IL17F, IL23R, RORC, CCL20...
```

ssGSEA 會對每個樣本算一個分數：

| sample    | Th17 score |
| --------- | ---------: |
| PSO_LS_01 |       0.85 |
| PSO_NL_01 |       0.30 |
| AD_LS_01  |       0.40 |
| AD_NL_01  |       0.20 |

如果 PSO_LS 的 Th17 score 很高，就可以說：

> PSO 病灶皮膚具有較高的 Th17 pathway 活性。

---

## 3. ssGSEA 的價值

DESeq2 是基因層級：

```text
哪個 gene 上升？
哪個 gene 下降？
```

ssGSEA 是功能層級：

```text
哪個免疫路徑上升？
哪種免疫細胞特徵比較強？
```

所以它更容易放進報告和模型。

例如你可以比較：

```text
AD_LS vs AD_NL 的 Th2 score
PSO_LS vs PSO_NL 的 Th17 score
PSO_LS vs AD_LS 的 inflammatory score
```

---

# 第 5 頁：流程圖 — 整個專題流程總結

這張圖是在把第 3、4 頁整合成一條 pipeline。

圖上的流程是：

```text
FASTQ
→ STAR 1-pass
→ Gene Expression Counts
→ DEGs
→ Enrichment / Functional Analysis
```

另一條是：

```text
Gene Expression Counts
→ TPM
→ ssGSEA
→ enrichment score
```

也就是說：

你們的資料會從 raw RNA-seq 變成兩種分析結果。

---

## 路線 1：DEG 分析路線

```text
FASTQ
→ STAR
→ Gene expression counts
→ DESeq2
→ DEGs
→ pathway enrichment
```

這條路回答：

```text
哪些基因在 LS 和 NL 之間顯著不同？
哪些基因在 AD 和 PSO 之間顯著不同？
這些基因代表哪些生物路徑？
```

---

## 路線 2：ssGSEA 特徵路線

```text
Gene expression counts
→ TPM
→ ssGSEA
→ enrichment score
```

這條路回答：

```text
每個樣本的免疫路徑活性如何？
AD/PSO 的免疫特徵差在哪？
NL 是否已經出現接近 LS 的免疫活化？
```

---

## 為什麼這兩條路都需要？

因為它們提供不同層次的資訊。

| 分析               | 產出                  | 用途            |
| ---------------- | ------------------- | ------------- |
| DESeq2           | DEGs                | 找顯著差異基因       |
| Pathway analysis | enriched pathways   | 解釋生物機制        |
| ssGSEA           | 每個樣本的 pathway score | 做特徵比較、分群、機器學習 |
| ML model         | 風險分類結果              | 判斷 NL 是否偏向 LS |

---

# 你現在無縫銜接要做的事情

你不用一開始就碰完整 FASTQ pipeline。你現在最重要的是把 **GSE121212 的 metadata 和 count matrix 整理好**。

---

## 第一階段：確認資料

你要先拿到兩個東西：

```text
1. count matrix
2. sample metadata
```

### count matrix 長這樣

| gene            | sample1 | sample2 | sample3 |
| --------------- | ------: | ------: | ------: |
| ENSG00000141510 |     100 |      80 |     120 |
| ENSG00000136244 |     500 |     600 |     550 |

### metadata 長這樣

| sample  | disease | condition | patient |
| ------- | ------- | --------- | ------- |
| GSMxxxx | AD      | LS        | AD001   |
| GSMxxxx | AD      | NL        | AD001   |
| GSMxxxx | PSO     | LS        | PSO001  |
| GSMxxxx | PSO     | NL        | PSO001  |

你後面所有分析都靠這兩張表。

---

## 第二階段：整理分組

你至少要整理出四組：

```text
AD_LS
AD_NL
PSO_LS
PSO_NL
```

如果有 healthy control，可以先放著，不一定要用。

你教授現在要的三個比較只需要這四組。

---

## 第三階段：做 DESeq2

三個比較分開做：

```text
1. PSO_LS vs PSO_NL
2. AD_LS vs AD_NL
3. PSO_LS vs AD_LS
```

每次輸出：

```text
all_results.csv
DEGs.csv
volcano plot
heatmap
```

---

## 第四階段：做 pathway analysis

拿每個比較的 DEGs 去做：

```text
GO BP
KEGG
Reactome
```

輸出：

```text
top enriched pathways
barplot
dotplot
```

---

## 第五階段：做 ssGSEA

把 counts 轉成 TPM 或使用適合的 normalized expression，然後用免疫相關 gene sets 算每個 sample 的 score。

你可以得到：

| sample    | Th1 | Th2 | Th17 | IFN_gamma | skin_barrier |
| --------- | --: | --: | ---: | --------: | -----------: |
| AD_LS_01  | 0.3 | 0.8 |  0.4 |       0.5 |         -0.6 |
| PSO_LS_01 | 0.7 | 0.3 |  0.9 |       0.8 |         -0.4 |

---

## 第六階段：建立模型

這是後面進階部分。

可能模型目標有兩種：

### 模型 A：分辨 LS vs NL

```text
input: gene expression / ssGSEA score
output: LS or NL
```

### 模型 B：判斷 NL 的 lesional-like risk

```text
input: NL sample 的特徵
output: low / medium / high lesional-like risk
```

第二個比較像你們投影片講的「NL 惡化風險」。

---

# 你可以直接跟學長姐接的問題清單

你現在去接專題，可以直接問這些：

1. **GSE121212 的 count matrix 放在哪裡？**
2. **metadata 是否已經整理好 AD_LS、AD_NL、PSO_LS、PSO_NL？**
3. **目前是從 FASTQ 重跑 STAR，還是直接用 GEO 提供的 counts？**
4. **DESeq2 的三個比較是否定義為：PSO_LS vs PSO_NL、AD_LS vs AD_NL、PSO_LS vs AD_LS？**
5. **DEG 門檻是 padj < 0.05 且 |log2FC| > 1 嗎？**
6. **後續 enrichment analysis 用 GO、KEGG、Reactome 還是哪一個？**
7. **ssGSEA 的 gene sets 用 Hallmark、KEGG、Reactome，還是自訂 immune signatures？**
8. **最後模型是要分類 LS/NL，還是要對 NL 做 lesional-like risk 分層？**

這 8 個問題問完，你就能知道目前進度在哪裡。

---

# 這 5 頁可以濃縮成一段報告講法

你可以這樣講：

> 本研究聚焦於兩種常見慢性發炎皮膚病：異位性皮膚炎 AD 與乾癬 PSO。雖然兩者臨床上皆表現為皮膚發炎，但其免疫機制有所不同，AD 較偏向 Th2/Th22 反應，PSO 則較偏向 Th1/Th17 反應。此外，非病灶皮膚 NL 雖然外觀接近正常，但可能已存在皮膚屏障異常與輕度免疫活化，因此具有轉變為病灶皮膚 LS 的潛在風險。本研究將利用 GSE121212 RNA-seq 資料集，分析 AD 與 PSO 患者之 LS 與 NL 皮膚樣本。研究流程包含 RNA-seq count data 整理、DESeq2 差異表現分析、DEG pathway enrichment analysis，以及以 TPM 表現矩陣進行 ssGSEA 免疫特徵分析。最終希望找出 AD 與 PSO 在 LS/NL 間的免疫差異，並建立可評估 NL 病灶化風險的預測模型。

---

# 你現在最該先學會的不是全部，而是這三件事

第一，**會分組**：

```text
AD_LS
AD_NL
PSO_LS
PSO_NL
```

第二，**會跑 DESeq2 三個比較**：

```text
PSO_LS vs PSO_NL
AD_LS vs AD_NL
PSO_LS vs AD_LS
```

第三，**會解釋結果**：

```text
log2FC > 0 代表前面那組比較高
padj < 0.05 代表統計上顯著
DEGs 可以拿去做 pathway analysis
ssGSEA 可以把基因表現轉成免疫特徵分數
```

你先掌握這三個，就已經可以接上專題主線了。

[1]: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE121212&utm_source=chatgpt.com "GSE121212 - GEO Accession viewer - NIH"
[2]: https://www.sciencedirect.com/science/article/pii/S0022202X19300077?utm_source=chatgpt.com "Atopic Dermatitis Is an IL-13–Dominant Disease with ..."

---

# Q2：所以我們要做的是，輸入某個樣本的基因表現或免疫分數，輸出:1.AD還是PSO 2.是NL還是健康 3.如果是NL，那它變成LS的風險高低為何，也就是「病灶化風險分層」。

對，你理解的方向**大致正確**，但我會幫你修成比較「研究上站得住腳」的版本。你們專題不是單純做一個分類器，而是分成 **三層任務**：

```text
輸入：某個皮膚樣本的基因表現資料 / 免疫特徵分數

輸出：
1. 疾病類型：AD 還是 PSO
2. 皮膚狀態：LS、NL，或 Healthy
3. 若樣本是 NL：它是否具有接近 LS 的病灶化風險
```

不過第 2 點我建議不要寫成「NL 還是健康」而已，因為完整一點應該是：

```text
是病灶皮膚 LS、非病灶皮膚 NL，還是健康皮膚 Healthy
```

這樣才比較完整。

---

# 你們專題真正要做的是什麼？

可以整理成一句話：

> 本研究希望利用 RNA-seq 基因表現資料與免疫特徵分數，建立一個可區分 AD 與 PSO、判斷皮膚狀態，並進一步評估非病灶皮膚 NL 病灶化風險的機器學習框架。

簡單講就是：

```text
基因表現 / 免疫分數
        ↓
機器學習模型
        ↓
疾病分類 + 皮膚狀態分類 + NL 風險分層
```

---

# 這三個任務要分開理解

## 任務 1：判斷 AD 還是 PSO

這是疾病分類。

輸入可以是：

```text
gene expression counts / TPM
ssGSEA immune scores
selected DEGs
```

輸出是：

```text
AD 或 PSO
```

這個任務回答的是：

> 這個樣本比較像異位性皮膚炎，還是比較像乾癬？

可能用到的特徵包括：

```text
Th2 / Th22 signature
Th1 / Th17 signature
cytokine-related genes
skin barrier genes
immune pathway scores
```

理論上：

```text
AD 可能偏 Th2 / Th22
PSO 可能偏 Th1 / Th17
```

所以模型可以學到兩者的免疫差異。

---

## 任務 2：判斷 LS、NL 還是 Healthy

這是皮膚狀態分類。

輸出不是只有 NL 或健康，最好設計成：

```text
LS
NL
Healthy
```

這樣比較合理。

因為你們的研究重點是：

```text
Healthy：真正健康皮膚
NL：外觀看似正常，但來自病人
LS：已經有明顯病灶
```

三者不是同一件事。

可以想成一條疾病進展軸：

```text
Healthy → NL → LS
```

其中 NL 是最有研究價值的中間狀態。

---

# 為什麼不能只做「NL vs Healthy」？

因為如果只做：

```text
NL vs Healthy
```

你只能知道：

> 非病灶皮膚跟健康皮膚有沒有差異。

但你無法知道：

> 這個 NL 是不是已經接近 LS？

所以更完整的模型應該要看三類：

```text
Healthy
NL
LS
```

這樣你才能進一步定義：

```text
NL 越像 LS，風險越高
NL 越像 Healthy，風險越低
```

---

# 任務 3：NL 的病灶化風險分層

這是你們專題最核心、也最有亮點的地方。

意思是：

> 對於一個外觀看似正常的 NL 樣本，我們想知道它在分子層級上比較接近 Healthy，還是比較接近 LS。

如果一個 NL 樣本的基因表現或免疫分數很像 LS，那就可以說它是：

```text
High lesional-like risk
```

如果比較像 Healthy，就可以說：

```text
Low lesional-like risk
```

---

# 但這裡有一個很重要的限制

嚴格來說，如果資料集沒有追蹤同一塊 NL 皮膚未來是否真的變成 LS，那你不能直接宣稱：

```text
這個 NL 未來一定會變成 LS
```

你比較安全、比較學術的說法是：

```text
lesional-like immune activation risk
```

或中文：

```text
病灶樣免疫活化風險
```

也就是：

> 這個 NL 樣本在分子特徵上接近 LS，因此可能代表較高的病灶化傾向。

不要寫得太絕對：

```text
預測 NL 變成 LS
```

比較推薦寫成：

```text
評估 NL 的病灶樣分子特徵程度
```

或：

```text
評估 NL 的 lesional-like risk
```

---

# 所以你們的模型架構可以這樣設計

## 第一層：疾病分類模型

```text
Input: gene expression / ssGSEA scores
Output: AD or PSO
```

例如：

```text
Sample X → AD
Sample Y → PSO
```

---

## 第二層：皮膚狀態分類模型

```text
Input: gene expression / ssGSEA scores
Output: Healthy / NL / LS
```

例如：

```text
Sample X → NL
Sample Y → LS
Sample Z → Healthy
```

---

## 第三層：只針對 NL 做風險分層

```text
Input: NL sample 的 gene expression / ssGSEA scores
Output: Low / Medium / High lesional-like risk
```

例如：

```text
NL sample A → Low risk
NL sample B → Medium risk
NL sample C → High risk
```

---

# 最合理的分析流程

你可以把整個專題流程畫成這樣：

```text
GSE121212 RNA-seq data
        ↓
整理 metadata
        ↓
建立四大樣本群：
AD_LS, AD_NL, PSO_LS, PSO_NL
加上 Healthy control
        ↓
DESeq2 找 DEGs：
1. AD_LS vs AD_NL
2. PSO_LS vs PSO_NL
3. PSO_LS vs AD_LS
        ↓
Pathway enrichment analysis
        ↓
將 counts 轉 TPM
        ↓
ssGSEA 取得免疫 pathway scores
        ↓
建立 ML models：
1. AD vs PSO
2. LS vs NL vs Healthy
3. NL lesional-like risk stratification
```

---

# 你們的輸入資料可以有兩種版本

## 版本 A：用基因表現當特徵

例如：

| sample   | IL13 | IL17A | CCL17 | S100A7 | KRT16 |
| -------- | ---: | ----: | ----: | -----: | ----: |
| AD_LS_1  |  8.2 |   1.1 |   9.5 |    3.2 |   4.1 |
| PSO_LS_1 |  2.1 |   8.8 |   3.0 |    9.2 |   8.7 |

優點：

```text
資訊量多
可能分類效果好
```

缺點：

```text
基因太多，容易 overfitting
解釋性比較差
```

---

## 版本 B：用 ssGSEA 免疫分數當特徵

例如：

| sample   | Th1 | Th2 | Th17 | IFN | Barrier | Keratinization |
| -------- | --: | --: | ---: | --: | ------: | -------------: |
| AD_LS_1  | 0.3 | 0.9 |  0.4 | 0.5 |    -0.6 |            0.4 |
| PSO_LS_1 | 0.8 | 0.3 |  0.9 | 0.8 |    -0.4 |            0.9 |

優點：

```text
比較容易解釋
特徵數比較少
適合做模型和報告
可以說明免疫機制
```

缺點：

```text
依賴 gene set 品質
可能損失部分基因層級資訊
```

我會建議你們：

```text
先用 ssGSEA scores 做主要模型
再用 DEGs / gene expression 做輔助比較
```

這樣報告會比較漂亮，也比較容易解釋。

---

# NL 風險分層可以怎麼做？

這是重點。

因為你沒有真正的 longitudinal label，例如：

```text
這個 NL 後來變成 LS
這個 NL 後來沒有變成 LS
```

所以不能直接訓練一個真正的「未來惡化預測模型」。

比較可行的是做 **lesional-like score**。

---

## 方法 1：用 LS vs Healthy 訓練模型，再套用到 NL

這是最直觀的做法。

### Step 1

先用明確的兩端樣本訓練模型：

```text
Healthy = 0
LS = 1
```

模型學到：

> 什麼樣的免疫特徵比較像病灶皮膚。

---

### Step 2

把 NL 樣本丟進模型。

模型會輸出一個機率：

```text
P(LS-like)
```

例如：

| NL sample | P(LS-like) | 風險     |
| --------- | ---------: | ------ |
| NL_01     |       0.15 | Low    |
| NL_02     |       0.52 | Medium |
| NL_03     |       0.87 | High   |

這樣你的風險分層就可以定義成：

```text
P(LS-like) < 0.33 → Low
0.33 ≤ P(LS-like) < 0.66 → Medium
P(LS-like) ≥ 0.66 → High
```

這個方法很好講，也很符合你們的研究故事。

---

## 方法 2：用 LS vs NL 訓練模型，看 NL 的決策分數

這個方法也可以，但比較容易有邏輯問題。

因為如果模型本來就是用 NL 訓練成「不是 LS」，那再拿 NL 回去看風險，容易變成循環。

所以我比較不建議主打這個。

---

## 方法 3：計算 NL 到 LS 和 Healthy 的距離

例如用 PCA、UMAP 或 cosine similarity。

概念是：

```text
NL 越靠近 LS cluster → 高風險
NL 越靠近 Healthy cluster → 低風險
```

可以畫圖：

```text
Healthy cluster ---- NL samples ---- LS cluster
```

這對報告很有視覺效果。

---

# 我最建議你們的主流程

我會建議你們專題最後包裝成這樣：

## Model 1：Disease classifier

```text
目標：AD vs PSO
特徵：ssGSEA immune scores + selected DEGs
模型：Logistic Regression / Random Forest / XGBoost
輸出：AD or PSO
```

---

## Model 2：Skin-state classifier

```text
目標：Healthy vs NL vs LS
特徵：ssGSEA immune scores
模型：Random Forest / XGBoost / SVM
輸出：Healthy / NL / LS
```

---

## Model 3：Lesional-like risk score for NL

```text
目標：評估 NL 是否接近 LS
方法：用 Healthy vs LS 訓練模型
套用：只把 NL 樣本丟進去
輸出：P(LS-like)
分層：Low / Medium / High
```

這樣最順。

---

# 你可以把專題題目改成這種方向

原本：

> 基於免疫細胞豐度的可解釋機器學習框架，用於異位性皮膚炎與乾癬之病灶化免疫風險分層

可以改得更清楚：

> 整合 RNA-seq 基因表現與免疫特徵分數之可解釋機器學習框架：應用於異位性皮膚炎與乾癬之疾病分類與非病灶皮膚病灶樣風險分層

英文可以是：

> An Interpretable Machine Learning Framework Integrating RNA-seq Expression and Immune Signature Scores for Disease Classification and Lesional-like Risk Stratification in Atopic Dermatitis and Psoriasis

---

# 你可以直接這樣跟學長姐確認

你可以問：

> 我理解目前專題是以 GSE121212 RNA-seq 資料為主，先用 DESeq2 分析 AD_LS vs AD_NL、PSO_LS vs PSO_NL，以及 PSO_LS vs AD_LS 的 DEGs，接著用 TPM 做 ssGSEA 取得免疫特徵分數。後續模型分三個任務：第一，判斷樣本屬於 AD 還是 PSO；第二，判斷樣本屬於 Healthy、NL 或 LS；第三，針對 NL 樣本，利用其接近 LS 的程度做 lesional-like risk 分層。請問目前專題是不是這樣定義？

這段你可以直接複製去問。

---

# 最後幫你修正一句話

你剛剛說：

> 輸入某個樣本的基因表現或免疫分數，輸出：1. AD 還是 PSO 2. 是 NL 還是健康 3. 如果是 NL，那它變成 LS 的風險高低為何

我建議改成：

> 輸入單一皮膚樣本的基因表現資料或 ssGSEA 免疫特徵分數，模型首先判斷其疾病類型為 AD 或 PSO，接著判斷其皮膚狀態為 Healthy、NL 或 LS；若樣本屬於 NL，則進一步根據其分子特徵接近 LS 的程度，評估其 lesional-like risk，並分為低、中、高風險。

這樣比較像正式研究方法，也不會過度宣稱真的能預測未來一定惡化。
