# 📝 Comparative Analysis of 1-Stage and 2-Stage Text Classification Using IndoBERT

This project investigates the effectiveness of using IndoBERT for text classification of Indonesian sports news articles. Two modeling strategies were compared: a 1-stage classification model and a 2-stage hierarchical classification model. The study focuses on handling class imbalance issues, particularly in underrepresented categories such as *Liga Italia*.

---

## 📚 Dataset

### 🕸️ Data Collection via Web Scraping

To obtain real-world, domain-specific data, a custom dataset was created by scraping sports news articles from online sources. The scraping process involved:

- Extracting **titles** and **content** from sports news websites using `requests` and `BeautifulSoup`
- Filtering news into categories: **Sepak Bola** vs **Non-Sepak Bola**
- Further subcategorizing Sepak Bola articles into: **Liga Inggris**, **Liga Indonesia**, **Liga Spanyol**, and **Liga Italia**
- The final dataset consists of labeled text used for fine-tuning IndoBERT models

This scraping-based dataset better reflects the noise and imbalance found in real-world data, making it a strong basis for testing hierarchical classification approaches.

---

## 🎯 Objective

To evaluate and compare the performance of:
- A **1-stage model**: Directly classifies texts into all subcategories
- A **2-stage model**: First classifies into broad categories (e.g., Sepak Bola vs Non-Sepak Bola), then performs subcategory classification

Special focus is given to performance on **minority classes**, particularly Liga Italia.

---

## 🧠 Model Architecture

### 1-Stage Model
- Direct classification into 5 classes
- Based on IndoBERT with:
  - Dropout: 0.5
  - Batch Size: 2
  - Early stopping after 3 epochs

### 2-Stage Model
- **Stage 1**: Classifies into Sepak Bola vs Non-Sepak Bola
- **Stage 2**: Further classifies Sepak Bola into 4 Liga categories
- Based on IndoBERT with:
  - Dropout: 0.7 (more regularization)
  - Batch Size: 8
  - Early stopping with patience = 3

### Tokenization & Preprocessing
- Tokenizer: IndoBERT tokenizer
- Max sequence length: 512
- Padding & truncation applied

---

## 📊 Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1-Score (Macro and Weighted)
- Per-class F1 analysis, especially for *Liga Italia*

---

## ✅ Results Summary

| Model | Stage | Test Accuracy | F1-Score (Liga Italia) | Macro F1 | Weighted F1 |
|-------|-------|----------------|-------------------------|----------|-------------|
| 1-Stage | -     | 95%           | 0.67                    | 0.90     | 0.95        |
| 2-Stage (Model 1) | 2     | 84.2%         | 0.50                    | 0.84     | 0.85        |
| 2-Stage (Model 2) | 2     | 100%          | 1.00                    | 1.00     | 1.00        |

---

## 📂 Files

| File Name                                  | Description                                               |
|--------------------------------------------|-----------------------------------------------------------|
| `2602090076_No3_Poster.pdf`                | Scientific poster explaining the methodology and results  |
| `2602090076_No2_UAS (FINALE).ipynb`        | Notebook with IndoBERT implementation for classification |
| `2602090076_No1&3_UAS(FINALE).ipynb`       | Web scraping, training, and evaluation of both models     |

---

## 🛠 Tools & Technologies

- **Model**: IndoBERT (Pre-trained from IndoNLU)
- **Framework**: PyTorch / HuggingFace Transformers
- **Scraping**: `requests`, `BeautifulSoup`
- **Tokenizer**: IndoBERT tokenizer
- **Evaluation**: scikit-learn, matplotlib
