### **Project Summary**

#### **1. Objective**

The project aimed to explore predictors of average depressive symptoms (Av\_PHQ) among adolescents, using a cleaned and imputed dataset from the Shamiri project. The analysis focused on identifying significant factors through visualization and regression modeling, particularly the roles of anxiety levels (Av\_GAD), social support (Av\_MSSS), and demographic/school-related variables.

---

#### **2. Dataset Overview**

* **Source:** `shamiri_imputed_dataset.csv`
* **Observations:** 658
* **Variables:** 36 (including PHQ items, GAD items, MSSS items, demographic info, and computed average scores)
* **Target Variable:** `Av_PHQ` – Average score from PHQ-8, indicating depressive symptoms

---

#### **3. Preprocessing Steps**

* Removed irrelevant or redundant columns to focus on core predictors.
* Converted `Gender` into a factor with labels "Female" and "Male".
* Created a refined dataset (`shamiri_dataset`) for analysis.

---

#### **4. Data Visualization**

To understand variable distributions and relationships:

* **Histograms**: Plotted for `Av_PHQ` and `Av_GAD` showing overall mental health trends.
* **Boxplots**: Compared `Av_PHQ` and `Av_GAD` by gender and school resource level.
* **Scatterplots with trend lines**: Examined relationships between:

  * Age and `Av_PHQ` / `Av_GAD`
  * `Av_MSSS` (social support) and `Av_PHQ`

*Key Insights:*

* Depressive symptoms (Av\_PHQ) show variation across gender and social support levels.
* Positive linear association between anxiety (Av\_GAD) and depressive symptoms.
* Negative association between social support (Av\_MSSS) and depression.

---

#### **5. Data Splitting**

* Dataset was split into:

  * **Training set:** 427 observations (65%)
  * **Testing set:** 231 observations (35%)
* Used the `caTools` package for random splitting.

---

#### **6. Model Development**

##### **Model 1: Full Linear Regression**

* Predictors: All retained variables including Av\_GAD, Av\_MSSS, demographic factors, school, and school resources.
* **RMSE (Test Set):** 0.447
* **Key Findings:**

  * Significant predictors: `Av_GAD` (positive), `Av_MSSS` (negative)
  * Other variables (e.g., Gender, School, Age) were not statistically significant.
  * `School_Resources` had perfect multicollinearity (singularities), hence excluded automatically.

##### **Model 2: Reduced Linear Regression**

* Predictors: `Av_GAD` and `Av_MSSS` only
* Removed: `Tribe`, `Gender`, `Age`, `School`, `School_Resources`
* **RMSE (Test Set):** 0.451
* **Adjusted R²:** 0.533 (vs. 0.529 in Model 1)
* **Conclusion:** The simpler model performed comparably to the full model with slightly higher RMSE but similar explanatory power.

---

#### **7. Interpretation & Insights**

* **Anxiety levels (Av\_GAD)** are the **strongest positive predictor** of depressive symptoms.
* **Social support (Av\_MSSS)** is a **protective factor**, significantly reducing depressive symptoms.
* **Demographic and school-related variables** (like Gender, Tribe, School) did not significantly influence depression when mental health scores were included.

---

#### **8. Conclusion**

This analysis suggests that psychological measures—particularly anxiety and social support—are better predictors of adolescent depression than demographic or school factors. Simple linear models using just these two variables provide strong predictive power, making them useful for early identification in mental health interventions.
