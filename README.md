# 💬 SMS Transaction Parser - NLP Pipeline

This project builds a robust NLP pipeline to parse raw SMS alerts and extract structured financial information.

---

## 🎯 Objective

Classify SMS messages into categories and extract structured data fields:

- **Classification**: Identify whether the SMS is about a:
  - `debit` transaction
  - `credit` transaction
  
- **Entity Extraction**:
  - `amount`: Transaction amount (e.g., ₹5,000)
  - `balance`: Available balance if present (e.g., Avl Bal: ₹10,000)

---

## 🛠️ Project Workflow

### 1. Preprocessing
- Lemmatization using `spaCy`
- Removal of stopwords and punctuation
- Lowercasing text

### 2. Feature Engineering
- `TF-IDF` vectorization (unigrams + bigrams)
- Binary keyword features:
  - `has_fail`, `has_due`, `has_otp`, `has_credit_score`, `has_payment`, `has_credit_card`

### 3. Classification Model
- **Algorithm**: `RandomForestClassifier`
- **Input**: TF-IDF + binary features
- **Output**: `debit`, `credit`, or `misc`
- **Metrics**:
  - Accuracy
  - Precision, Recall, F1-score

### 4. Named Entity Recognition (NER)
- Trained a custom `spaCy` model to detect:
  - `AMOUNT` — Transaction amount
  - `BALANCE` — Available balance
- Annotated ~150+ real and synthetic SMS messages

### 5. Inference Pipeline
- Load Acutal SMS Test dataset (Data.xlsx)
- Predict class (`debit`, `credit`, `misc`)
- Extract `amount` and `balance` using trained `spaCy` NER
- Save output to `.csv` or display in notebook

---

## 🧠 How to Run

1. Install dependencies:
```bash
pip install spacy pandas scikit-learn joblib
python -m spacy download en_core_web_sm
```
2. Train Classifier (if needed):
```bash
train_pipeline("data/training_data.csv")
```
3. Call prediction function:
```bash
predict_sms("data/Data.csv")
```
4. Train spaCy NER (optional, already provided):
```bash
python -m spacy train config.cfg --output ./output --paths.train ./train.spacy --paths.dev ./dev.spacy
```
