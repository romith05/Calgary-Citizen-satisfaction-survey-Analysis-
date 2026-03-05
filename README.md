# Calgary Citizen Satisfaction Survey Analysis (2018–2021, focused on 2021)

Statistical analysis and predictive modeling on the City of Calgary’s Citizen Satisfaction Survey to understand **what drives overall quality-of-life satisfaction** and how demographics + municipal service ratings relate to satisfaction. 

---

## Project Goals

This project answers two core questions:

1. **Demographic drivers:** Which socio-demographic characteristics (income, tenure, age, education, etc.) are associated with overall satisfaction? 
2. **Service drivers:** Which municipal services (transit, roads, parks, snow removal, etc.) most strongly impact overall satisfaction? 

---

## Dataset

- Source: City of Calgary open data (Citizen Satisfaction / Fall Survey of Calgarians).
- Coverage: Survey years **2018–2021**; this analysis **restricts to 2021**. :contentReference[oaicite:3]{index=3}
- Original size: ~10,000 responses, 139 variables; filtered to ~2,500 observations for 2021 with a selected feature subset. 
### Target Variable

Overall quality-of-life satisfaction is converted from a 1–10 rating into a **binary classification**:

- **Yes (Satisfied)** if rating > 5  
- **No (Not satisfied)** if rating ≤ 5  

This binary target is referred to as `Satisfaction`. 

---

## Methods

### 1) Exploratory Data Analysis (EDA)
Explored satisfaction distribution/proportions across:
- Age groups
- Years lived in Calgary
- Income groups
- Education levels
- City quadrant  
(see the report visuals and interpretations). 

### 2) Statistical Testing (Independence)
Used **Pearson’s Chi-Square tests** to test dependence between `Satisfaction` and each categorical predictor.

### 3) Predictive Modeling

#### Demographics model set
- Logistic Regression:
  - Full logit model
  - Reduced logit model
  - Class-weighted + higher threshold model
  - **Upsampled** logistic regression + K-fold CV
- Classification Trees:
  - Tree trained on original train split
  - Tree trained on upsampled train split 

#### Service model set
- Logistic Regression for services + variable importance (`varImp`) to identify influential services. 

---

## Key Results (Demographics Modeling)

Class imbalance was a major issue (the “No” class is much smaller), so multiple imbalance-handling strategies were tested (weighting, thresholding, upsampling). 

**Best-performing approach:** Logistic Regression with **upsampling**, validated with K-fold CV:  
- **K-fold accuracy:** **67.08%**   
- For **Yes (Satisfied)**:
  - Recall: **88.7%**
  - Precision: **74.6%**
  - F1: **81.1%** 
- For **No (Not satisfied)**:
  - Precision: **34.7%**
  - Recall: **16.6%**
  - F1: **22.5%** 

---

## Future Improvements

- Better handling of “Prefer not to answer” / uncertainty responses (imputation or separate handling strategies).   
- More imbalance-aware methods like **SMOTE**, cost-sensitive learning, and ensembles to improve “No” class performance. 

---

## Authors

- Deepika Gollamandala  
- Riya Chevli  
- Romith Bondada 

