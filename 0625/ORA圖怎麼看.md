可以，把這張圖當成「每一個圓點代表一條 pathway」來看會最簡單。

---

# ORA dot plot 讀圖方式

* **每一個圓點代表一條 pathway**

  * 左側 Y 軸是 pathway 名稱。
  * 圖中每一列對應一條顯著 pathway。

* **圓點大小：命中的共同 DEGs 數量**

  * 圓點越大，表示這條 pathway 中有越多本研究的 foreground genes。
  * 例如本頁為 LS-up 分析，圓點大小代表該 pathway 命中了多少個四資料集共同 LS-up genes。
  * 但圓點較大不一定代表富集程度較強，因為大型 pathway 原本就可能包含較多 genes。

* **X 軸 Fold enrichment：實際命中比例相對於隨機預期的倍數**

  * 越靠右，表示這條 pathway 在 foreground genes 中出現得比隨機預期更多。
  * 例如 fold enrichment = 5，表示實際命中的程度約為隨機預期的 5 倍。
  * Fold enrichment 越高，代表 foreground genes 越集中在該 pathway 中。
  * 但它不是 gene expression 的 fold change，也不能解讀為 pathway 活性增加了幾倍。

* **顏色：統計顯著程度**

  * 顏色代表 `−log10(BH adjusted P)`。
  * 越偏黃色，代表數值越大，也就是 BH adjusted P 越小，統計證據越強。
  * 越偏紫色，代表 adjusted P 較大，但圖中顯示的 pathways 仍已通過設定的顯著門檻。

### 讀圖時的順序

1. 先看圓點是否靠右：富集倍數是否高。
2. 再看圓點大小：有多少共同 DEGs 支持。
3. 最後看顏色：多重檢定校正後的統計證據是否強。

### 注意

一條較有說服力的 pathway，通常會同時具備：

* 位於較右側：fold enrichment 較高
* 圓點較大：有較多 genes 命中
* 顏色較黃：BH adjusted P 較小

但不能只看其中一項，也不能把 ORA 結果直接解讀成因果關係或 pathway 活性增加的倍數。

---

## 用你的 Hallmark 圖舉例

以 `Interferon Gamma Response` 為例：

* 圓點位在相對右側，代表四資料集共同 LS-up genes 在這條 pathway 中的出現比例，明顯高於隨機預期。
* 圓點較大，代表命中的 LS-up genes 數量也較多。
* 顏色偏黃，代表經過 BH 多重檢定校正後，統計證據仍然很強。

因此這條 pathway 不是只有「有幾個 genes 命中」，而是同時具備：

> 命中 genes 較多、富集倍數高、adjusted P 小。

相較之下，某些圓點雖然很靠右，但圓點較小，可能表示只有少數 genes 命中一個很小的 pathway，所以仍要同時看圓點大小與顏色。

## 三個最容易搞混的地方

### 1. Fold enrichment 不是 logFC

* `logFC`：單一 gene 在 LS 與 NL 間的表現差異。
* `fold enrichment`：某 pathway 在 foreground gene list 中被命中的程度，相對於隨機預期高出多少倍。

所以圖上 X 軸的 10，不代表 pathway 在 LS 中表現高 10 倍。

### 2. 圓點大不一定比較重要

圓點大只表示命中的 genes 多，但大型 pathway 本來就可能較容易命中很多 genes。因此還要一起看 fold enrichment 和 adjusted P。

### 3. 顏色黃不代表生物效應一定最大

黃色表示統計證據較強，不代表它一定是最重要的疾病機制。生物意義仍要結合：

* pathway 功能
* 命中的 genes
* 是否在其他資料庫或 GSEA 中重現
* 是否與 PSO 已知機制相符

你口頭報告時可以用一句話概括：

> 每個圓點代表一條 pathway；越靠右表示富集倍數越高，圓點越大表示命中的共同 DEGs 越多，顏色越黃表示多重檢定校正後的統計證據越強。
