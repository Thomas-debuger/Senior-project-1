| 階段                                     | 狀態            |
| -------------------------------------- | ------------- |
| Step 0：專案、版本、原始檔、MD5                   | 完成            |
| Step 1：Split／Exclude overlap           | 完成            |
| Step 2：tested genes、兩套 common universe | 完成            |
| Step 3：Split All＋Hallmark pilot與重現驗證   | 完成            |
| Step 4：Split Hallmark All／Up／Down      | 完成            |
| Step 4：Split Reactome All／Up／Down      | **尚未執行，現在要做** |
| Step 4：Split GO BP All／Up／Down         | 尚未做           |
| Step 4：Exclude 的9組 ORA                 | 尚未做           |
| Step 5：Split vs Exclude比較與正式圖          | 尚未做           |
| Step 6：四資料集 GSEA                       | 尚未做           |

---

9 組是：

```text
3 種基因方向 × 3 種 pathway 資料庫 = 9 組
```

## Split 主分析的 9 組

### All

1. `Split All + Hallmark`
2. `Split All + Reactome`
3. `Split All + GO Biological Process`

### Up

4. `Split Up + Hallmark`
5. `Split Up + Reactome`
6. `Split Up + GO Biological Process`

### Down

7. `Split Down + Hallmark`
8. `Split Down + Reactome`
9. `Split Down + GO Biological Process`

你目前已完成：

```text
1. Split All + Hallmark
4. Split Up + Hallmark
7. Split Down + Hallmark
```

所以 Split 還剩 6 組：

```text
Split All / Up / Down + Reactome
Split All / Up / Down + GO BP
```

## Exclude 敏感度分析也有相同的 9 組

只是把 foreground 和 universe 換成 Exclude：

```text
Exclude All / Up / Down
×
Hallmark / Reactome / GO BP
```

因此全部 ORA 是：

```text
Split 9 組
＋ Exclude 9 組
＝ 18 組 ORA
```

這正是你的單人工作流程中 Step 4 的設計。
