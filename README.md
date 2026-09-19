# LeGenD Glycan Profiler

單檔網頁工具：輸入 **lectin microarray**、**ELLA/ELISA** 或 **FACS** 的 lectin 結合強度，重建純化蛋白質（或細胞）的 **N-glycan profile**。

方法依據：

> Li H, Peralta AG, Schoffelen S, et al. **LeGenD: determining N-glycoprofiles using an explainable AI-leveraged model with lectin profiling.** *bioRxiv* (2024). [PMC10996628](https://pmc.ncbi.nlm.nih.gov/articles/PMC10996628/)

線上使用（GitHub Pages）：發布後見本 repo 的 Pages 網址。

## 這頁做什麼

1. 說明為什麼 lectin 圖譜**不能**一一對應完整 glycoprofile（文獻 Figure 1）。
2. 依論文步驟說明資料庫如何建立：309 張 geCHO UPLC 剖面 → LinearCode 特徵矩陣 → Bojar et al. 結合規則 → 模擬 lectin profile → ANN / SHAP。
3. 下拉或點選文獻 Table S1 的 8 種 lectin（DSL, LCA, MAL-I, PHA-E, PHA-L, RCA-I, SNA, WGA），列出對應醣結構與 SNFG 示意。
4. 輸入實驗數據或載入示範樣本，做可解釋的剖面重建。

## 示範樣本

| 樣本 | 格式 | 預期特徵 |
| --- | --- | --- |
| 人類血清 IgG | ELLA | 高 LCA（core Fuc），低 MAL-I / PHA-L |
| 牛 Fetuin B | ELLA | 高 MAL-I、SNA、PHA-L，低 LCA |
| 高甘露糖型 | FACS | 末端 Manα1,2；RCA / SNA 低 |
| 去唾液酸化 IgG | lectin array | SNA / MAL-I 降、RCA-I 升 |
| EPO 樣高度分枝 | ELLA | PHA-L、唾液酸化與 poly-LacNAc 同時升高 |

示範 lectin 訊號由「參考 glycoprofile × 文獻式結合規則」正向模擬，與 LeGenD 用模擬 lectin profile 當訓練輸入的邏輯一致。

## 本地開啟

用瀏覽器直接打開 `index.html`，或：

```bash
python -m http.server 8080
```

然後開啟 `http://localhost:8080`。

## 重要限制

本工具是**教學用可解釋重建**（特徵矩陣 × 結合規則 + 非負最小平方，閾值 0.02），**不是**論文未公開的 ANN 權重重現。FACS 細胞表面還有 O-glycan 與糖脂，解釋需更謹慎。SNA / MAL-I 無法分辨 α2,8 polysialic acid（文獻對 Fetuin 的討論）。

結構符號依 [SNFG](https://www.ncbi.nlm.nih.gov/glycans/snfg.html)。結合規則概念取自 Bojar et al., *ACS Chem. Biol.* 2022。
