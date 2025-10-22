# QRT Data Challenge – Predicting Survival in Blood Cancer Patients

## 📌 Context
In recent years, the medical field has increasingly adopted **data-driven methods** for prognosis and treatment of complex diseases such as cancer. Predictive models in healthcare have transformed patient care, enabling more tailored and effective treatment strategies.  

These advances are particularly valuable in **oncology**, where accurate survival predictions can significantly improve the quality and timing of therapeutic decisions.

---

## 🎯 Goal
In partnership with **Institut Gustave Roussy**, this year’s **QRT Data Challenge** focuses on predicting the **risk of death** for patients diagnosed with a blood cancer, specifically a subtype of **adult myeloid leukemia**.  

For these patients, risk evaluation is measured by **overall survival (OS)** — the time from initial diagnosis until death or last recorded follow-up.

---

## 💡 Why It Matters
Estimating a patient’s prognosis is essential for adapting therapeutic approaches:

- **Low-risk patients** may receive supportive therapies to improve blood parameters and overall quality of life.  
- **High-risk patients** may be prioritized for more intensive treatments, such as **hematopoietic stem cell transplantation**.  

Accurate risk predictions can therefore lead to:
- Better clinical decision-making  
- Improved patient quality of life  
- More efficient use of healthcare resources  

This challenge offers participants a unique opportunity to work with **real-world data from 24 clinical centers** and contribute to a concrete application of data science in medicine.

---

## 📂 Dataset Description
The dataset is provided in two ZIP files and one CSV file:

- **X_train.zip** – Training input data  
- **X_test.zip** – Test input data  
- **Y_train.csv** – Training labels  

- Training set: **3,323 patients**  
- Test set: **1,193 patients**  

Input data is split into two categories:
1. **Clinical Data** (one row per patient)  
2. **Molecular Data** (one row per somatic mutation per patient)  

The column **`ID`** uniquely identifies each patient and links the clinical data, molecular data, and `Y_train`.

---

## 🧾 Prediction Task
The objective is to predict **overall survival (OS)** for each patient.  

Two key outcomes are provided in `Y_train.csv`:
- **OS_YEARS**: Overall survival time in years since diagnosis  
- **OS_STATUS**: Survival status (1 = deceased, 0 = alive at last follow-up)  

### Expected Submission
A CSV file with:
- **ID**: Patient identifier  
- **risk_score**: Predicted risk of death  

⚠️ Only the **ranking** of predictions matters, not their absolute scale.  
If patient *i* is predicted with lower risk than patient *j*, the model estimates that *i* will survive longer than *j*.  

An example submission with random predictions is provided in the **Files** section.

---

## 📊 Evaluation Metric: IPCW-C-index
The challenge uses the **Inverse Probability of Censoring Weighted Concordance Index (IPCW-C-index)**, implemented in [scikit-survival](https://scikit-survival.readthedocs.io/).

### Concordance Index (C-index)
The C-index measures how well a model orders survival times.  
It is the proportion of all **comparable patient pairs** where the predicted risk ordering matches the actual survival ordering.

- **1.0** → Perfect concordance (ideal ranking)  
- **0.5** → Random model (no predictive power)  

### IPCW Extension
The **IPCW-C-index** extends the C-index to handle **right-censored data** by applying inverse probability weights.  
This accounts for patients who were still alive at the last observation.  

For this challenge, the metric is **truncated at 7 years**.

---

## 🧪 Data Details

### Clinical Data (one row per patient)
- **ID**: Unique patient identifier  
- **CENTER**: Clinical center where the patient was treated  
- **BM_BLAST**: Percentage of blasts in bone marrow (abnormal blood cells)  
- **WBC**: White blood cell count (Giga/L)  
- **ANC**: Absolute neutrophil count (Giga/L)  
- **MONOCYTES**: Monocyte count (Giga/L)  
- **HB**: Hemoglobin level (g/dL)  
- **PLT**: Platelet count (Giga/L)  
- **CYTOGENETICS**: Cytogenetic description (chromosomal abnormalities, e.g., *46,XX* for normal female, *46,XY* for normal male, or high-risk anomalies such as monosomy 7)  

### Molecular Data (one row per somatic mutation per patient)
- **ID**: Unique patient identifier  
- **CHR, START, END**: Chromosomal position of the mutation  
- **REF, ALT**: Reference and alternative nucleotides  
- **GENE**: Gene affected by the mutation  
- **PROTEIN_CHANGE**: Impact of the mutation on the resulting protein  
- **EFFECT**: General classification of mutation effect  
- **VAF**: Variant allele fraction (proportion of cells carrying the mutation)  

---

## ✅ Summary
- **Task**: Predict survival risk in blood cancer patients  
- **Data**: Clinical + molecular features from 24 centers  
- **Metric**: IPCW-C-index (truncated at 7 years)  
- **Submission**: CSV with `ID` and `risk_score`  

This challenge bridges **data science and medicine**.
