# Q1：甚麼是LODO
# A1：意思是：

假設四個 development cohorts 是：

* GSE121212
* GSE182740
* GSE154200
* GSE306437

某一輪 outer LODO 先把 **GSE121212 完整保留作 outer-test**，這一輪的 outer-training data 就只剩：

* GSE182740
* GSE154200
* GSE306437

接著在這三個 outer-training datasets 裡面再做三次調參驗證：

| Inner fold | 訓練資料集               | 驗證資料集     |
| ---------- | ------------------- | --------- |
| 1          | GSE154200＋GSE306437 | GSE182740 |
| 2          | GSE182740＋GSE306437 | GSE154200 |
| 3          | GSE182740＋GSE154200 | GSE306437 |

每一組候選 alpha、lambda 都在這三個 inner validation cohorts 上測試，根據三次結果選出較穩定的超參數。

選完後：

1. 使用這一輪全部三個 outer-training cohorts 重新訓練模型。
2. 最後才拿去預測從頭到尾都沒參與調參的 GSE121212。

所以這句的白話意思是：

> **先完整留下一個資料集作最終內部測試；剩下三個資料集再輪流留一個作調參驗證，避免模型只在混合樣本的隨機切分上選參。**

完整流程是：

> 留 1 個 GSE 當 outer-test
> → 剩下 3 個 GSE 輪流留 1 個做 inner validation
> → 選定超參數
> → 用剩下 3 個 GSE 全部重訓
> → 測試最初保留的 outer-test GSE

你簡報中可改成更白話的：

> **每輪先完整保留一個 GSE 作為未見測試資料；其餘三個 GSE 再輪流以一個作為調參驗證集、兩個作為訓練集，選定超參數後，使用三個 GSE 重新訓練並測試最初保留的 GSE。**

# Q2：為何是用outer形容
# A2：因為這裡用的是 **nested cross-validation（巢狀交叉驗證）**，有兩層迴圈，所以才用 **outer／inner** 區分。

* **Outer loop**：負責估計整套建模流程對未見 cohort 的表現。
* **Inner loop**：只在 outer-training data 裡負責選超參數。

例如某一輪先完整保留 GSE121212：

* **outer-test cohort**：GSE121212
* **outer-training data**：另外三個 GSE

再於這三個 GSE 裡輪流留一個調參：

* 2 個 GSE 作 inner training
* 1 個 GSE 作 inner validation

所以「outer-training data」的意思不是「外部訓練資料」，而是：

> **外層切分後，被分到訓練端的資料。**

完整關係如下：

```text
Outer loop
├─ Outer-test：完整保留 1 個 GSE，最後測試
└─ Outer-training：其餘 3 個 GSE
   └─ Inner loop
      ├─ Inner-training：其中 2 個 GSE
      └─ Inner-validation：其中 1 個 GSE
```

之所以一定要加 `outer`，是因為單寫 `training data` 會不清楚：可能是指外層的三個資料集，也可能是指內層真正拿來擬合的兩個資料集。

最白話的中文可以寫：

> **在每輪外層驗證的訓練資料中，再以資料集為單位輪流留出一個資料集進行內層調參。**

另外，**outer-test 不等於真正的 external test**：

* outer-test：仍屬於 development data，只是該輪暫時完全保留。
* external test：從頭到尾都不參與模型開發，例如 GSE153007、GSE26952。
