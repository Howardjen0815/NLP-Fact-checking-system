# Climate Change Fact-Checking System (Top-10 Ranking)

[cite_start]這是一個針對氣候科學領域開發的自動化事實查核系統。本專案實現了一個結合**多階段證據檢索 (Multi-stage Evidence Retrieval)** 與**深度學習標籤分類 (Claim Classification)** 的混合式管線。在 University of Melbourne NLP 專案競賽中獲得了 **Top-10** 的排名 [cite: 9, 17]。

## 🚀 技術亮點 (Technical Highlights)

* [cite_start]**三階段混合檢索架構**：結合了 SBERT 的高效過濾與 Cross-Encoder 的精確重排序，平衡了大規模資料檢索的效率與準確率 [cite: 27, 83]。
* [cite_start]**SBERT 微調優化**：採用 **Multiple Negatives Ranking Loss (MNRL)** 進行微調，相較於 TF-IDF Baseline，檢索表現大幅提升 [cite: 26, 61, 69]。
* [cite_start]**證據串接策略**：實驗證實將多個證據 passages 進行 **Concatenation** 處理，能為 BERT 分類器提供最穩健的語義背景，開發集準確率達 **0.4870** [cite: 6, 174]。

## 🏗️ 系統架構 (System Architecture)

本系統的核心模組如下：

### 1. 證據檢索模組 (Retrieval Pipeline)
* [cite_start]**Stage 1 & 2: SBERT 稠密檢索與過濾**：使用微調後的 SBERT 模型提取 Top-2000 候選，並透過預計算嵌入向量縮減至 Top-15 [cite: 86, 89]。
* [cite_start]**Stage 3: Cross-Encoder 重排序**：利用 RoBERTa-based Cross-Encoder 捕捉 Claim 與 Evidence 之間的細微語義互動，最終選定 **Top-4** 證據 [cite: 92, 100]。

### 2. 標籤分類模組 (Classification)
* [cite_start]**模型選擇**：對比了 MLP, TextCNN, BiLSTM 等模型，最終選用 **BERT** 作為核心分類器，處理四類標籤預測 (`SUPPORTS`, `REFUTES`, `NOT_ENOUGH_INFO`, `DISPUTED`) [cite: 132, 150, 169]。

## 📊 實驗結果 (Experimental Results)

| 評估指標 | 開發集 (Dev Set) | 測試集 (Test Set) |
| :--- | :--- | :--- |
| **分類準確率 (Accuracy)** | **0.4870** | **0.4935** |
| **檢索 F1-Score** | 0.2253 | 0.1737 |
| **調和平均數 (Harmonic Mean)** | 0.3080 | 0.2569 |

> [cite_start][cite: 211]

## 🛠️ 開發與貢獻 (Individual Contributions - Yu-Han Jen)
* [cite_start]負責開發、部署與實驗 **SBERT-based 稠密檢索**、**Cross-Encoder 重排序**以及最終的混合檢索模型 [cite: 214]。
* [cite_start]進行創新性實驗嘗試，包含 **BM25 混合重排序**、多重評分系統 (Multi-Score Reranking) 以及輕量化 MMR 演算法 [cite: 214]。

## 📂 檔案清單
* [cite_start]`COMP90042_essay.pdf`: 完整的 ACL 格式技術報告 [cite: 18, 212]。
* `NLP fact checking model.ipynb`: 包含模型訓練與評估的完整程式碼。
