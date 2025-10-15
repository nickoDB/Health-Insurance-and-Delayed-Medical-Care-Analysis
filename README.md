# Health Insurance Coverage and Delayed Medical Care — MEPS 2020

This project investigates the relationship between health insurance coverage and the likelihood of postponing necessary medical treatment. Drawing from the 2020 Medical Expenditure Panel Survey (MEPS), a comprehensive, nationally representative survey of U.S. households we employed two predictive models: a logistic regression model and a k-nearest neighbors (KNN) classifier. These models aimed to predict delays in medical care based on insurance type (private, public, or none), while accounting for variables such as age, gender, race/ethnicity, and educational attainment. The results indicate that individuals without health insurance are significantly more prone to delaying care, even after controlling for various demographic and socioeconomic factors.

---

## Overview

Many Americans postpone medical care due to barriers such as lack of insurance coverage. Understanding how demographic and socioeconomic factors interact with insurance type can help policymakers and healthcare professionals address inequities in access to care.

**Research Question:**

To what extent does health insurance status (private, public, or uninsured) influence an individual’s likelihood of delaying needed medical care, and how do demographic and socioeconomic factors such as income, education, and overall health interact with this relationship?

---

## Data Source

- **Dataset:** 2020 Full-Year Consolidated File (HC-224)
- **Source:** [Medical Expenditure Panel Survey (MEPS)](https://meps.ahrq.gov/mepsweb/data_files/pufs/h224/h224dta.zip)
- **Provider:** U.S. Department of Health and Human Services, Agency for Healthcare Research and Quality (AHRQ)
- **Sample:** Nationally representative U.S. household survey

### Key Variables

| Variable | Description |
|-----------|--------------|
| DLAYCA42 | Delayed medical care (1 = Yes, 2 = No) |
| INSCOV20 | Insurance type (1 = Private, 2 = Public, 3 = Uninsured) |
| AGELAST | Age |
| SEX | Gender |
| RACETHX | Race/Ethnicity |
| HIDEG | Education level |
| REGION53 | U.S. Census region |
| INTVLANG | Interview language |
| PERWT20F, VARSTR, VARPSU | Survey design and weight variables |

---

## Tools and Packages

The analysis was conducted in **R**, using the following packages:

- survey  
- dplyr  
- haven  
- FNN  
- caret  
- broom  
- class  
- kableExtra  

---

## Methodology

1. **Data Cleaning and Preparation**
   - Removed missing and invalid values.
   - Converted categorical variables to factors.
   - One-hot encoded categorical variables for KNN.
   - Created a binary target variable `delay_medical` (1 = delayed, 0 = not delayed).

2. **Exploratory Analysis**
   - Conducted descriptive summaries and cross-tabulations.
   - Found higher rates of delay among uninsured individuals.

3. **Modeling**
   - **Model 1:** Survey-weighted Logistic Regression.
   - **Model 2:** K-Nearest Neighbors (KNN) classifier.

4. **Evaluation**
   - Logistic regression identified significant predictors (p < 0.001).
   - KNN achieved ~93% accuracy but struggled to identify positive delay cases.

---

## Results Summary

### Key Findings
- Uninsured individuals were significantly more likely to delay medical care.
- Public insurance performed comparably to private insurance.
- Female respondents and certain racial groups were more likely to report delays.
- Education levels showed strong effects (potentially due to variable coding).



### Model Performance

<img width="682" height="497" alt="image" src="https://github.com/user-attachments/assets/68309f03-e86b-4ae1-ab01-cabaf316a804" />


| Model | Accuracy | Strengths | Weaknesses |
|--------|-----------|------------|-------------|
| Logistic Regression | High interpretability | Statistically sound, survey-weighted | Assumes linear relationships |
| KNN (k = 3) | 93.3% | Non-parametric, intuitive | Poor at identifying delayed cases |

---

## Conclusion

This project affirms that health insurance coverage plays a critical role in timely access to medical care. Among all groups, uninsured individuals were significantly more likely to delay treatment, underscoring how coverage gaps directly affect health-seeking behavior. On the other hand, public insurance appeared to perform on par with private insurance, suggesting that expanding public options could effectively reduce disparities in care access. 
Gender also played a role - female respondents were more likely to postpone care, a pattern that may reflect unique barriers such as caregiving responsibilities or reproductive health limitations. Racial and ethnic disparities were present as well. For example, Asian respondents delayed care less frequently than other groups, while White and mixed-race individuals reported more delays compared to Hispanic individuals. These differences may stem from a complex mix of cultural, systemic, and economic influences. 


Though region and language were not significant predictors in this model, further investigation could determine whether these factors interact with others in more nuanced ways. The findings that education levels produced disproportionately large coefficients suggest potential issues in how education was coded or its influence on other variables - future studies should address this.
We also developed a KNN classification model using the same variables. While it achieved an acceptable accuracy, it lacks the interpretability of logistic regression and is more suited as a supporting method rather than a primary analytical tool.

