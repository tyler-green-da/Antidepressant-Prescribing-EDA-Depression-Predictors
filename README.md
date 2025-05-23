# Project: Antidepressant Prescribing Trends in England & Factors Associated with Depression in NHS Staff

## Overview & Motivation

This capstone project, developed as part of the Digital Futures Data Analyst training, undertakes a dual analysis of mental health in the UK:

1.  **Antidepressant Prescribing Landscape (2019-2024):** An Exploratory Data Analysis (EDA) of NHS England's Prescription Cost Analysis (PCA) data. This involved investigating national trends in the volume, cost, and types of antidepressants dispensed, alongside detailed geographical variations across Integrated Care Boards (ICBs).
2.  **Predictors of Depression in NHS Staff (Pandemic Context):** A predictive modelling component using the MeCare survey dataset (NHS staff in London, January 2021). This aimed to identify key psychosocial and occupational characteristics associated with probable depression (based on PHQ-9 scores) during a period of intense pressure.

My motivation for this project stems from an undergraduate background in Neuroscience and a specific interest in antidepressant prescription practices. My dissertation explored holistic alternatives to medication, such as Mindfulness-Based Cognitive Therapy (MBCT), which showed potential for significant additional symptom reduction. This project seeks to combine large-scale prescribing data analysis with a deeper look into individual-level factors influencing mental health states.

## Skills Demonstrated

This project showcases a range of data analysis and machine learning skills, including:

* **Data Acquisition & Sourcing:** Identifying and obtaining relevant public datasets (NHSBSA, Zenodo, ONS Geography).
* **Data Cleaning & Preparation (Python - Pandas, NumPy):**
    * Handling large datasets (millions of rows for PCA data).
    * Combining and merging data from multiple files and sources.
    * Data type conversion and management.
    * String manipulation and standardization (e.g., for geographical names, survey responses).
    * Systematic missing value analysis and imputation (mode, median, special value flagging).
    * Feature scaling and encoding (Label Encoding for categorical features for tree-based models).
    * Iterative feature selection based on EDA, domain knowledge, and statistical properties (variance, correlation).
* **Exploratory Data Analysis (EDA) (Python - Matplotlib, Seaborn; Tableau):**
    * Univariate analysis (distributions, value counts).
    * Bivariate analysis (feature vs. target relationships, feature vs. feature correlations).
    * Time-series trend analysis.
    * Geospatial analysis and mapping (joining with shapefiles, visualizing regional variations).
    * Identifying and interpreting anomalies and significant patterns in data.
* **Predictive Modelling (Python - Scikit-learn):**
    * Problem framing (classification).
    * Feature engineering and selection for modelling.
    * Train-test splitting for model validation.
    * Model training (Decision Tree, Random Forest).
    * Hyperparameter tuning using `GridSearchCV`.
    * Model evaluation using various metrics (Accuracy, Precision, Recall, F1-score, Confusion Matrix).
    * Interpretation of model results, including feature importance.
* **Data Visualization & Storytelling (Tableau):**
    * Designing and building an interactive, multi-faceted dashboard.
    * Creating effective charts (KPIs, line charts, bar charts, treemaps, pie charts, maps).
    * Implementing dashboard interactivity (filters, parameters, highlight actions).
    * Crafting a clear narrative to communicate complex data insights to a target audience.
* **Project Management & Documentation:**
    * Structured project planning.
    * Use of Miro to plan and organise workload.
    * Clear documentation of process and findings (Jupyter Notebooks, README).

## Datasets Used

1.  **NHS Prescription Cost Analysis (PCA) Data (England, 2019-2024):**
    * **Source:** NHS Business Services Authority (NHSBSA) Open Data Portal.
    * **Description:** Aggregated data on prescription items dispensed in England, detailing costs and volumes.
    * **Link (Example):** [NHSBSA PCA Data](https://opendata.nhsbsa.net/dataset/prescription-cost-analysis-pca-annual-statistics)
2.  **MeCareNWL – Psychosocial and Occupational Impact of COVID-19 among NHS Staff (January 2021):**
    * **Source:** Zenodo / F1000Research.
    * **Description:** Survey data from >1000 NHS staff in NW London (demographics, occupational factors, psychosocial factors, mental health scale scores).
    * **Link:** [Zenodo Dataset](10.5281/zenodo.7352557) | [F1000Research Article](https://zenodo.org/records/8112940)
3.  **ICB Shapefile:**
    * **Source:** ONS Geography Portal.
    * **Description:** Geospatial data for Integrated Care Board boundaries.
4.  **ICB Population Data (England):**
    * **Source:** Manually transcribed from a table image (original source ONS).
    * **Description:** Population figures for ICBs, used for normalizing prescribing rates.

## Methodology & Workflow

The project followed an iterative data analysis workflow:

1.  **Data Acquisition & Initial Understanding:** Sourcing datasets and familiarizing with their structure, content, and documentation.
2.  **Data Cleaning & Preparation (Python - Pandas, NumPy):**
    * **PCA Data:** Involved combining multiple annual files, extensive string standardization for geographical names (ICB/STP transitions to ensure consistency for mapping with shapefiles and population data) using RegEx, filtering for antidepressant medications (BNF Chapter 4, Section 3), data type conversions, and handling missing values (e.g., for `SUPPLIER_NAME`). The meaning of `PREP_CLASS` codes was researched and applied for branded/generic analysis.
    * **MeCare Data:** This involved an initial reduction from ~194 raw survey columns to ~55 relevant features. Q-number column headers were renamed to meaningful variable names. A systematic process of data type conversion (object to numeric/category, mapping ordinal/binary scales with attention to scoring direction) was undertaken. Missing values were handled strategically: rows with missing target variables were dropped, highly sparse columns were removed, specific contextual features had missingness flagged with a special value (-1), and remaining missing feature data was imputed using median or mode.
3.  **Exploratory Data Analysis (Tableau & Python):**
    * **PCA Data (Tableau):** Focused on visualizing national prescribing trends (total items, NIC, average NIC/item over 2019-2024), geographical variations (items/1000 population, avg NIC/item by ICB on interactive maps), breakdowns by antidepressant class, identification of top prescribed chemicals, and analysis of branded vs. generic prescribing patterns and costs.
    * **MeCare Data (Python):** Univariate and bivariate analyses were performed on the cleaned and imputed data to understand feature distributions and their individual relationships with the target variable (`probable_phq`), informing the final feature selection for the predictive model.
4.  **Predictive Modelling (Python - Scikit-learn):**
    * **Target Variable (MeCare):** `probable_phq` (Probable Depression, derived from PHQ-9 scores).
    * **Feature Selection:** Iterative process based on EDA insights and domain knowledge to select ~25 impactful predictors from the MeCare dataset.
    * **Encoding:** Nominal categorical features in the final selected set were Label Encoded.
    * **Model Training & Tuning:** A Decision Tree Classifier was selected as the primary model. Train-test splitting was performed, followed by hyperparameter tuning using `GridSearchCV` (optimizing `max_depth`, `min_samples_split`, `min_samples_leaf`, `max_features`, `criterion`) with 10-fold cross-validation.
    * **Model Evaluation:** The tuned Decision Tree was evaluated on the unseen test set using accuracy, precision, recall, F1-score, and a confusion matrix. Feature importances were extracted and analyzed. (A Random Forest model was also tuned and evaluated for comparison).
5.  **Data Storytelling & Visualization (Tableau):**
    * An interactive, single-page, scrollable dashboard was created to present the key EDA insights from the PCA data and the feature importance findings from the MeCare predictive model, forming a cohesive narrative.

## Key Findings/Insights (Brief Summary)

* **PCA Data EDA:**
    * Antidepressant prescribing volume in England consistently increased from 2019-2024.
    * A notable spike in the average cost of *both* generic and branded antidepressants occurred in 2020, likely linked to COVID-19 pandemic impacts on supply chains.
    * Significant geographical variations in prescribing rates (items per 1000 population) and average cost per item exist across ICBs.
    * Generic antidepressants constitute the vast majority of items dispensed suggesting strong adherence to NHS cost-effectiveness strategies, though substantial absolute spending on branded versions persists (£155M). This highlights an area for further cost reduction.
* **MeCare Predictive Model (Predicting Probable Depression in NHS Staff):**
    * The strongest factors associated with the delevopment of depression were probable generalised anxiety and burnout from work. Other significant psychosocial factors included measures of social connection (e.g., how close the partcicipant feels to others), financial worries, demographic variables, and specific workplace factors like manager support.

## Tools & Technologies Used

* **Python:**
    * **Pandas & NumPy:** Core libraries for data manipulation, cleaning, and numerical operations.
    * **Scikit-learn:** For machine learning tasks including `LabelEncoder`, `train_test_split`, `DecisionTreeClassifier`, `RandomForestClassifier`, `GridSearchCV`, and various `metrics` (accuracy, precision, recall, F1, confusion matrix).
    * **Matplotlib & Seaborn:** For generating visualizations within Jupyter Notebooks during the EDA and model evaluation phases.
* **Tableau Desktop:** Primary tool for comprehensive Exploratory Data Analysis, creating interactive visualizations (maps, line charts, bar charts, treemaps, pie charts), and building the final data storytelling dashboard.
* **Jupyter Notebooks:** For all Python-based data processing and model development.
* **Excalidraw:** For initial dashboard layout sketching.
* **Coolors.co:** For developing the dashboard color theme.

## Future Work (Optional)

* Explore advanced time-series forecasting for antidepressant prescribing trends.
* Incorporate more granular socio-economic data at the ICB level to investigate drivers of prescribing variation.
* Conduct a more in-depth analysis of specific antidepressant drug categories (e.g., SNRIs, older TCAs).

## Acknowledgements (Optional)

* Thanks to my instructors and peers at Digital Futures for their support and guidance throughout this capstone project.
* Acknowledgement to NHSBSA and the MeCareNWL study researchers for making their valuable data publicly available for research and analysis.

---
