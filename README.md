# 📧 Email Spam Detection with Machine Learning

## 📌 Project Overview

Spam messages are a major challenge in digital communication systems, often containing promotional content, scams, or phishing attempts. Automatically identifying these messages is crucial for improving user experience and security.

This project builds a **machine learning-based spam detection system** that classifies messages into:

* **Ham (0)** → Legitimate messages
* **Spam (1)** → Unwanted or harmful messages

Beyond basic classification, this project explores how different **class imbalance handling techniques** affect model performance.

## 🎯 Objectives

The main goals of this project are:

* Build and evaluate multiple machine learning models for spam detection
* Perform **Exploratory Data Analysis (EDA)** to understand patterns in the data
* Apply **Natural Language Processing (NLP)** techniques
* Investigate the effect of:

  * Baseline training (no balancing)
  * Oversampling (RandomOverSampler)
  * Class weighting
* Compare models using multiple evaluation metrics
* Identify the best-performing model for real-world use

## 📂 Dataset Description

* Total messages: **5,572**
* Ham (Non-Spam): **4,825 (87%)**
* Spam: **747 (13%)**

⚠️ The dataset is **imbalanced**, meaning models may favor predicting ham more often than spam.

## 🧹 Data Cleaning & Preprocessing

The dataset originally contained unnecessary columns with missing values:

* `Unnamed: 2`
* `Unnamed: 3`
* `Unnamed: 4`

### Steps performed:

* Dropped irrelevant columns
* Renamed columns to:

  * `label`
  * `message`
* Converted labels:

  * `ham → 0`
  * `spam → 1`
* Checked for missing values

## 🔍 Exploratory Data Analysis (EDA)

### 📊 Class Distribution

![Class Distribution](images/class_distribution.png)

**Insight:**

* The dataset is heavily skewed toward ham messages
* This imbalance can affect model performance


### 📏 Message Length Distribution

![Message Length](images/message_length_distribution.png)

**Insight:**

* Spam messages tend to be **longer and more structured**
* Ham messages are shorter and conversational
* Long messages (400–800 characters) were retained as they likely represent real spam

### 🔤 Word Frequency Analysis (Spam Messages)

![Word Frequency](images/spam_word_frequency.png)

**Insight:**

* Common spam indicators include:

  * **free**
  * **call**
  * **txt**
  * **claim**
* These patterns make spam detection effective with NLP

## ⚙️ Text Preprocessing

To prepare text for modeling:

* Converted text to lowercase
* Removed punctuation
* Removed stopwords using NLTK
* Tokenized text


## 🔄 Feature Engineering

Text data was transformed into numerical features using:

### 🔹 TF-IDF Vectorization

* Converts text into weighted numerical representation
* Highlights important words while reducing noise


## 🔀 Train-Test Split

* Training set: **80%**
* Test set: **20%**
* Used **stratified sampling** to maintain class distribution


# 🤖 Modeling Approach

## 🔹 Baseline Models (No Imbalance Handling)

Models were first trained on the original dataset without any balancing.

### Models Used:

* Naive Bayes
* Logistic Regression
* Support Vector Machine (SVM)
* Random Forest

### 📊 Confusion Matrix — Naive Bayes (Baseline)

![NB Baseline](images/cm_nb_baseline.png)

* High accuracy but lower spam recall
* Some spam messages misclassified



### 📊 Confusion Matrix — SVM (Baseline)

![SVM Baseline](images/cm_svm_baseline.png)

* Strong and balanced performance
* Minimal misclassification

---

### 📊 Confusion Matrix — Random Forest (Baseline)

![RF Baseline](images/cm_rf_baseline.png)

* Very high precision
* Lower recall for spam

---

### 📊 Confusion Matrix — Logistic Regression (Baseline)

![LR Baseline](images/cm_lr_baseline.png)

* Balanced performance
* Good trade-off between precision and recall

---

## ⚖️ Oversampling Experiment

To address class imbalance, **RandomOverSampler** was applied to the training data.

### Goal:

Improve the model’s ability to detect spam (increase recall)

---

### 📊 Confusion Matrix — Naive Bayes (Oversampling)

![NB OS](images/cm_nb_os.png)

* Significant improvement in spam detection
* Slight drop in precision

---

### 📊 Confusion Matrix — SVM (Oversampling)

![SVM OS](images/cm_svm_os.png)

* Slight improvement in recall
* Minor precision trade-off

---

### 📊 Confusion Matrix — Random Forest (Oversampling)

![RF OS](images/cm_rf_os.png)

* Better recall compared to baseline
* More balanced predictions

---

### 📊 Confusion Matrix — Logistic Regression (Oversampling)

![LR OS](images/cm_lr_os.png)

* Performance remains stable
* No major improvement

---

## 🎯 Class Weighting

Instead of modifying the dataset, class weighting adjusts how the model penalizes errors.

Applied to:

* Logistic Regression

---

### 📊 Confusion Matrix — Logistic Regression (Class Weight)

![LR CW](images/cm_lr_cw.png)

* Improved focus on spam
* Balanced precision and recall

---

# 📊 Model Comparison

| Model               | Method       | Accuracy | Precision | Recall | F1 Score |
| ------------------- | ------------ | -------- | --------- | ------ | -------- |
| Naive Bayes         | Baseline     | 0.963    | 1.000     | 0.725  | 0.840    |
| Naive Bayes         | Oversampling | 0.981    | 0.951     | 0.906  | 0.928    |
| Logistic Regression | Baseline     | 0.981    | 0.927     | 0.933  | 0.930    |
| Logistic Regression | Oversampling | 0.980    | 0.926     | 0.926  | 0.926    |
| Logistic Regression | Class Weight | 0.981    | 0.927     | 0.933  | 0.930    |
| SVM                 | Baseline     | 0.983    | 0.971     | 0.899  | 0.934    |
| SVM                 | Oversampling | 0.981    | 0.951     | 0.906  | 0.928    |
| Random Forest       | Baseline     | 0.977    | 0.992     | 0.832  | 0.905    |
| Random Forest       | Oversampling | 0.982    | 0.992     | 0.872  | 0.929    |

---

# 🧠 Key Insights

* **SVM achieved the best overall performance**
* **Logistic Regression remained the most stable model**
* **Naive Bayes improved significantly with oversampling**
* **Random Forest had high precision but needed balancing for better recall**

---

# 🏁 Conclusion

* Class imbalance affects spam detection significantly
* Oversampling improves recall but may reduce precision
* Class weighting provides a cleaner alternative
* Best models:

  * **SVM → Best overall**
  * **Logistic Regression → Most balanced**

---

# 🚀 Future Improvements

* Hyperparameter tuning (GridSearchCV)
* Deep learning approaches (LSTM, BERT)
* Deployment with Streamlit
* Real-time spam filtering system

---

# 🛠️ Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* NLTK
* Matplotlib, Seaborn

---

# 📁 Project Structure

email-spam-detection/
│
├── data/
├── notebooks/
├── images/
├── README.md
└── requirements.txt

---

# ✨ Author

**Latifah Bashir**
Aspiring Data Analyst | Machine Learning Enthusiast
