# Breast-Cancer-Diagnostic-Analysis
A machine learning project to diagnose breast cancer (benign/malignant) using cell nuclei characteristics, featuring robust classification, model interpretability, and a Power BI dashboard.

# Breast Cancer Diagnostic Analysis

## Table of Contents
- [1. Overview](#1-overview)
- [2. Data Source](#2-data-source)
- [3. Methodology](#3-methodology)
    - [3.1 Data Cleaning & Preprocessing](#31-data-cleaning--preprocessing)
    - [3.2 Exploratory Data Analysis (EDA)](#32-exploratory-data-analysis-eda)
    - [3.3 Model Selection & Training](#33-model-selection--training)
    - [3.4 Model Evaluation](#34-model-evaluation)
- [4. Key Findings & Actionable Insights](#4-key-findings--actionable-insights)
- [5. Interactive Dashboard (Power BI)](#5-interactive-dashboard-power-bi)
- [6. Tools Used](#6-tools-used)
- [7. Future Work](#7-future-work)
- [8. Contact Information](#8-contact-information)

---

## 1. Overview

This project focuses on building a machine learning model to **diagnose breast cancer** (predicting whether a tumor is benign or malignant) based on characteristics of cell nuclei. Leveraging a publicly available dataset, the analysis demonstrates a complete data science pipeline from data acquisition and preprocessing to model training, evaluation, and interpretability, culminating in an interactive Power BI dashboard for actionable insights.

---

## 2. Data Source

The dataset used is the **"Breast Cancer Diagnostic Data Set"** from Kaggle. It comprises various features computed from a digitized image of a fine needle aspirate (FNA) of a breast mass, describing characteristics of the cell nuclei.

* **Link to Dataset:** [Breast Cancer Diagnostic Data Set](https://www.kaggle.com/datasets/iamtanmayshukla/breast-cancer-diagnostic-data-set)

---

## 3. Methodology

My analytical approach involved a structured machine learning pipeline:

### 3.1 Data Cleaning & Preprocessing

* **Initial Data Inspection:** Checked for missing values, data types, and initial distributions.
* **Handling Missing Values:** Confirmed **no missing values** were present, simplifying this step.
* **Handling Unnecessary Columns:** Dropped the `id` column (an identifier) and `Unnamed: 32` (if present, typically an empty column).
* **Target Encoding:** The `diagnosis` column ('M' for Malignant, 'B' for Benign) was encoded into numerical format (1 for Malignant, 0 for Benign).
* **Feature Scaling:** Applied `StandardScaler` to all numerical features to normalize their range, which is beneficial for many machine learning algorithms.

### 3.2 Exploratory Data Analysis (EDA)

Comprehensive EDA was performed to understand the dataset's characteristics and inform model building:

* **Diagnosis Distribution:** Identified the class imbalance, with more Benign cases (357) than Malignant (212), guiding the choice of evaluation metrics.
    ![Diagnosis Distribution](plots/[YOUR_DIAGNOSIS_DISTRIBUTION_PLOT_FILENAME].png)
* **Feature Distributions by Diagnosis:** Visualized key features like `radius_mean`, `perimeter_mean`, `concave points_mean`, etc., showing clear separation between Benign and Malignant diagnoses, with Malignant cases typically having higher values.
    ![Feature Distributions by Diagnosis](plots/[YOUR_FEATURE_DISTRIBUTIONS_PLOT_FILENAME].png)
* **Correlation Analysis:** Generated a correlation matrix to understand inter-feature relationships and correlations with the diagnosis. Features related to `concave points`, `perimeter`, `radius`, `area`, and `concavity` showed the highest positive correlation with malignancy.
    ![Correlation Matrix](plots/[YOUR_CORRELATION_MATRIX_PLOT_FILENAME].png)
* **Top Correlated Features:** Highlighted the top 10 features most correlated with a malignant diagnosis, explicitly showing their strong linear association.
    ![Top 10 Correlations](plots/[YOUR_TOP_10_CORRELATIONS_PLOT_FILENAME].png)
* **Pairwise Relationships:** Pairplots of top features visually confirmed their strong discriminative power, showing distinct clustering of Benign and Malignant cases.
    ![Pairplot of Top Correlated Features](plots/[YOUR_PAIRPLOT_PLOT_FILENAME].jpg)

### 3.3 Model Selection & Training

* **Data Split:** The data was split into training (80%) and testing (20%) sets using a **stratified split** to maintain the original class distribution in both sets, crucial for the imbalanced nature of the dataset.
* **Model Choices:** Evaluated three robust classification models:
    * **Logistic Regression:** As a strong, interpretable baseline.
    * **Random Forest Classifier:** For its robustness and ensemble power.
    * **LightGBM Classifier:** For its efficiency and high performance on tabular data.
* All models were trained on the scaled training data.

### 3.4 Model Evaluation

The models demonstrated exceptionally strong performance on the unseen test set, indicating high accuracy and reliability for diagnostic purposes.

* **Key Metrics (LightGBM Classifier):**
    * **Accuracy:** **[YOUR_ACCURACY_VALUE]** (e.g., 0.9649)
    * **Precision (Malignant):** **[YOUR_PRECISION_M_VALUE]** (e.g., 1.0000)
    * **Recall (Malignant):** **[YOUR_RECALL_M_VALUE]** (e.g., 0.9048)
    * **F1-Score (Malignant):** **[YOUR_F1_M_VALUE]** (e.g., 0.9500)
    * **ROC AUC Score:** **[YOUR_ROC_AUC_VALUE]** (e.g., 0.9940)
* **Interpretation:** The exceptionally high Precision (1.0000) for Malignant cases means the model made **zero False Positives**, minimizing unnecessary patient anxiety and follow-up. The high Recall indicates it correctly identified most actual malignant cases, crucial for timely treatment. The near-perfect ROC AUC scores across all models (see plot below) demonstrate outstanding discriminatory power.
* **ROC Curves:**
    ![ROC Curves](plots/[YOUR_ROC_CURVE_PLOT_FILENAME].png)

---

## 4. Key Findings & Actionable Insights

The feature importance analysis from the LightGBM model provided crucial insights into the cellular characteristics most indicative of breast cancer:

![Feature Importances](plots/[YOUR_FEATURE_IMPORTANCE_PLOT_FILENAME].png)

The **most significant diagnostic indicators** (top 5) were identified as:

1.  `texture_worst`
2.  `texture_mean`
3.  `perimeter_worst`
4.  `concave points_worst`
5.  `concave points_mean`

* **Insights:** These findings suggest that the **coarseness or variability of the cell surface (texture)**, the **irregularity/severity of indentations (concave points)**, and the **overall size/shape (perimeter)**, particularly their "worst" (most severe) and "mean" values, are the most critical factors for distinguishing between benign and malignant breast masses.

* **Actionable Recommendations:**
    * For medical professionals, these features highlight the most discriminative cellular characteristics for focused analysis during diagnosis.
    * For future research and advanced diagnostic tool development, these features should be prioritized for data collection and algorithmic focus.

---

## 5. Interactive Dashboard (Power BI)

An interactive Power BI dashboard was developed to provide a user-friendly and intuitive view of the model's performance and key diagnostic insights for a non-technical audience.

* **Purpose:** To clearly present the model's high accuracy, detailed performance metrics (like the confusion matrix), and the most influential diagnostic features in an accessible format.
* **Key Visuals:** The dashboard includes KPI cards for Accuracy, Precision, Recall, and F1-Score; a visual Confusion Matrix; and a Feature Importance bar chart.
* **Dashboard Overview:**
    ![Dashboard Overview](plots/[YOUR_DASHBOARD_OVERVIEW_FILENAME].png)
* **Feature Importance View:**
    ![Dashboard Feature Importance](plots/[YOUR_DASHBOARD_FEATURE_IMPORTANCE_FILENAME].png)

---

## 6. Tools Used

* `Python`
* `Pandas` (for data manipulation)
* `NumPy` (for numerical operations)
* `Scikit-learn` (for preprocessing, model selection, and evaluation)
* `LightGBM` (for gradient boosting classification)
* `Matplotlib` & `Seaborn` (for data visualization in Python)
* `Power BI` (for interactive dashboarding and reporting)

---

## 7. Future Work

* **Clinical Validation:** Partner with medical experts to validate model findings against real-world clinical practice and patient outcomes.
* **External Data Integration:** Explore integrating additional patient data (e.g., patient demographics, medical history) if available and ethically permissible, to potentially enhance diagnostic accuracy or identify specific patient subgroups.
* **Model Deployment:** Develop a secure, user-friendly interface for medical professionals to input data and receive real-time diagnostic predictions.

---

## 8. Contact Information

* **Naveen Lakshman Kumar Basina**
* **LinkedIn:** [https://www.linkedin.com/in/naveen-lakshman/](https://www.linkedin.com/in/naveen-lakshman/)
* **Email:** [naveenklaxman22@gmail.com](mailto:naveenklaxman22@gmail.com)
