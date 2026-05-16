坦白說：**這版程式碼已經比一開始的 GEO2R + Excel 手動篩選好很多，但還不能說「已經夠優秀到可以當最終嚴謹版」。**
它可以作為**報告用的進階實作版本**，但如果教授要你精準比對 supplementary DEG list，還有幾個地方需要補強。

---

## 你這版已經做得好的地方

第一，你有設定動態參數：

```r
CUTOFF_PVAL
CUTOFF_ADJ_PVAL
CUTOFF_LOGFC
```

這很好，因為之後要測不同 P-value 或 logFC 門檻時，不需要整份程式到處改，只要改前面參數即可。你目前也已經把 `CUTOFF_LOGFC` 改成 2.0。

第二，你有做資料快取：

```r
GSE182740_data.rds
```

這可以避免每次重新下載 GEO 資料，對反覆測試 cutoff 很有幫助。

第三，你有做 probe-to-gene 的前處理，也就是計算每個 probe 的平均表現量，刪除空白 Gene.symbol，並且同一個 Gene.symbol 只保留平均表現量最高的 probe。這就是你簡報裡講的 **Max Mean** 方式。

第四，你把 limma 分析包成 function：

```r
run_limma_analysis <- function(keyword, pdata, exprs_matrix)
```

這樣 PsO、Mixed、AD 三組可以共用同一個分析流程，程式結構比三段重複 code 乾淨很多。

第五，你同時輸出 raw P-value 和 FDR adjusted P-value 兩套結果。這對應到論文裡「P < 0.05」和「Benjamini-Hochberg 校正」之間的模糊處。

所以這版可以說是：

> **比 GEO2R 手動版更模組化、更可重複、更適合做報告的版本。**

---

## 但還不能說「最優秀」的地方

### 1. LS / NL 判斷方式還不夠穩

你現在判斷 Lesion 的方式是：

```r
ls_index <- apply(sub_pdata, 1, function(x) any(grepl("normal: LS", x)))
status <- ifelse(ls_index, "Lesion", "NonLesion")
```

這行比較危險，因為它是在整列 metadata 裡面搜尋 `"normal: LS"`。如果 metadata 格式稍微不同，可能會抓錯。

更穩的寫法應該直接使用這個欄位：

```r
pdata$`lesional (ls) vs. nonlesional (nl) vs. normal:ch1`
```

因為你之前 Step 2 已經確認這個欄位明確標示 LS、NL、Normal。
所以這裡建議改成直接讀欄位，不要用 `apply()` 搜整列。

---

### 2. 沒有輸出 overlap 指標

你現在的程式只會輸出六個 CSV：

```text
PsO_DEGs_RawP_result.csv
PsO_DEGs_AdjP_result.csv
Mixed_DEGs_RawP_result.csv
Mixed_DEGs_AdjP_result.csv
AD_DEGs_RawP_result.csv
AD_DEGs_AdjP_result.csv
```

這些能告訴你自己篩出了哪些 genes，但**還沒有直接跟 supplementary list 做 overlap**。
既然你現在已經有 supplementary 官方 gene list，最重要的不是只看 DEG 數量，而是要算：

```text
overlap 數量
recall
precision
F1-score
missing genes
extra genes
```

你目前程式還沒有這一段。

---

### 3. 只有一種 probe-to-gene 規則

你現在只用：

> 同一個 Gene.symbol 保留平均表現量最高的 probe。

這是合理方法，但不是唯一方法。
如果目標是找出哪個方法最接近 supplementary，應該至少比較：

| 合併規則          | 意義                   |
| ------------- | -------------------- |
| Max Mean      | 保留平均表現量最高的 probe     |
| Min P.Value   | 保留 P.Value 最小的 probe |
| Max |logFC|   | 保留變化幅度最大的 probe      |
| Min adj.P.Val | 保留 FDR 最小的 probe     |

你目前這版只有 Max Mean。

---

### 4. 先去重再跑 limma，可能會影響結果

你現在是在 limma 前就做：

```r
clean_exprs <- exprs_data[clean_anno$ID, ]
rownames(clean_exprs) <- clean_anno$Gene.symbol
```

也就是你先把 probe-level matrix 轉成 gene-level matrix，再跑 limma。

這有一個問題：
如果作者是先在 probe-level 跑 GEO2R / limma，再把顯著 probe 轉成 gene list，你現在的流程就和作者不同。

兩種流程差很多：

```text
你的流程：
先 probe 去重 → 再 limma → 再篩 DEG

另一種可能：
先 probe-level limma → 篩 DEG → 再轉 gene-level
```

這可能是你和 supplementary 不一致的主要原因之一。

---

## 所以這版程式碼的評價

我會這樣評分：

| 面向                         | 評價   |
| -------------------------- | ---- |
| 作業報告可讀性                    | 高    |
| 自動化程度                      | 不錯   |
| 比 Excel 手動版                | 明顯更好 |
| 嚴謹重現論文                     | 還不夠  |
| 和 supplementary overlap 分析 | 還缺   |
| 探索最佳規則                     | 還缺   |

結論是：

> **這版程式碼已經適合放在報告中說明「我如何改進 GEO2R 手動分析」，但還不是最終最佳 DEG 重現程式。**

---

## 你可以在報告中怎麼說

你可以這樣講，會比較安全：

> 這版 RStudio limma 程式相較 GEO2R 網頁版有三個優化：第一，將 P-value、adjusted P-value 和 logFC 設為動態參數，方便重新測試不同門檻；第二，加入快取機制，避免每次重新下載 GEO 資料；第三，針對 microarray 的 probe-level 問題，採用 Max Mean 方法，保留同一基因中平均表現量最高的 probe。
>
> 不過，這仍然是其中一種合理的 probe-to-gene 處理策略，並不一定等於論文作者的實際方法。因此後續需要再將結果與 supplementary DEG list 做 overlap 分析，並比較不同 probe-to-gene 合併規則，例如保留 P-value 最小或 |logFC| 最大的 probe。

這樣不會把你的程式講得太滿，也能展現你知道限制在哪裡。

