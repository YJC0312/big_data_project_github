# 碩一上大數據分析課程學期分析專案
資料集：[Supermarket dataset for predictive marketing 2023](https://www.kaggle.com/datasets/hunter0007/ecommerce-dataset-for-predictive-marketing-2023)  
使用：Apriori, K-means, Recommender systems    
實作細節文件 [ECommerce_consumer_behaviour_doc](./ECommerce_consumer_behaviour_doc.md)  
若想下載實作須注意：  
1. 將第一個 cell 修改成呼叫 Kaggle API
2. 使用到的 surprise 函數僅支援到 python 3.10 須注意版本
> 123


# 📊 電子商務消費者行為分析  
**E-commerce Consumer Behaviour Analysis**

> 碩一｜大數據分析課程｜學期分析專案  

本專案以大型超市交易資料為基礎，分析消費者購買行為，並透過 **關聯規則探勘（Apriori）**、**使用者分群（K-means）** 與 **推薦系統（Recommender System）**，提出具體且可落地的商業洞察與應用建議。

---

## 📁 專案內容說明

| 檔案 | 說明 |
|---|---|
| `ECommerce_consumer_behaviour.ipynb` | 主要分析與模型實作（EDA、Apriori、K-means、推薦系統） |
| `ECommerce_consumer_behaviour_doc.md` | **完整實作說明文件**（研究背景、資料處理、方法論、評估指標與結論） |
| `README.md` | 專案總覽與使用說明 |

📌 **完整分析流程與理論說明請參考：**  
👉 [ECommerce_consumer_behaviour_doc.md](./ECommerce_consumer_behaviour_doc.md)

---

## 🎯 問題背景與研究目標

### 業務背景
以美國大型超市交易資料為例，面對：
- 需求波動與庫存風險  
- 消費者回購與購物週期差異  
- 商品組合與交叉銷售機會  

### 分析目標
1. **發掘商品共現模式**（交叉銷售 / 貨架擺放）  
2. **消費者分群**（高頻補貨客、探索型用戶、新客等）  
3. **建立個人化推薦模型**，提升 Top-K 命中率與使用者體驗  

---

## 📊 使用資料集

- **資料來源**：  
  [Supermarket dataset for predictive marketing 2023 (Kaggle)](https://www.kaggle.com/)
- **資料規模**：  
  約 **2,019,501 筆交易紀錄 × 12 欄位**
- **資料粒度**：  
  商品列（Item-level），依分析目的轉換為訂單層與使用者層

---

## 🛠 使用方法與技術

### 1️⃣ 探索式資料分析（EDA）
- 下單時段、星期分布  
- 訂單規模（Basket Size）  
- 購買週期與回購行為  
- 商品與部門偏好分析  

### 2️⃣ 關聯規則探勘（Apriori）
- 交易籃轉換（One-hot encoding）
- 指標：Support / Confidence / **Lift**
- 發現高關聯商品組合（如生鮮 × 乳製品）

### 3️⃣ 使用者分群（K-means）
- 特徵工程（購買頻率、週期、多樣性、回購率、部門偏好）
- 前處理：`log1p`、StandardScaler、PCA
- 評估：Elbow、Silhouette、DB Index、穩定度（ARI）
- 最終分為 **5 類典型客群**

### 4️⃣ 推薦系統（Recommender System）
- 模型：
  - Item-based KNN
  - BaselineOnly
  - **SVD（Matrix Factorization）**
- 評估指標：
  - Precision@10、Recall@10、HitRate@10
  - **NDCG@10（主指標）**
  - AUC（sampled）

---

## 📈 主要分析結果摘要

- ✅ **Apriori**：  
  - 找出 13 條 Lift > 1 的強關聯規則（最高約 1.9）
- ✅ **K-means**：  
  - 辨識出穩定回購客、重度補貨客、探索型用戶、新客等族群
- ✅ **推薦系統**：  
  - **SVD 與 BaselineOnly 表現最佳且穩定**
  - NDCG@10、AUC 明顯優於 Random 與 KNN

---

## ⚙️ 環境與版本注意事項

⚠️ 若要在本地端完整重現分析，請注意：

1. **Kaggle API**
   - Notebook 第一個 cell 需設定 Kaggle API 金鑰
2. **Python 版本**
   - `surprise` 套件僅支援 **Python 3.10**
3. **建議套件**
   ```bash
   pandas
   numpy
   matplotlib
   seaborn
   scikit-learn
   mlxtend
   scikit-surprise
   ```

---

## 📌 研究限制與未來方向

- 冷啟動問題（新用戶、新商品）
- 高維稀疏資料的計算成本
- 可延伸方向：
  - Neural Collaborative Filtering (NCF)
  - 序列模型（LSTM / Transformer）
  - 外部資料（促銷、天氣、宏觀經濟）

---

## 👤 作者

- 碩一大數據分析課程專案  
- Author: *陳彥均 (Sam)*  
- Date: 20251230  
