# Predicting tranquilizer misuse in Argentina based on the ENCOPRAC 2022

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Status](https://img.shields.io/badge/Status-Research%20Completed-success)

## Abstract
This study investigates the behavioral determinants of psychotropic substance consumption in Argentina, distinguishing between medical use and non-prescription misuse (self-medication). Utilizing data from the ENCOPRAC 2022 National Survey (N=~7,200), two random forest classifiers were developed to identify predictors for each consumption profile. The analysis highlights a structural dissociation: while medical consumption is predicted by demographic and systemic factors like age and healthcare access), misuse is primarily driven by behavioral covariates (risk perception, tobacco use history). To address severe class imbalance (<2% prevalence of misuse), the study employed SMOTE (Synthetic Minority Over-sampling Technique), achieving a recall of 0.59 in the detection of at-risk users.

---
## Introduction
The consumption of tranquilizers without medical supervision represents a significant public health challenge. Traditional statistical methods often fail to detect rare events in population surveys. 

---
## Objectives
1.  Isolate the drivers of self-medication compared to prescribed consumption.
2.  Evaluate the efficacy of random forest combined with resampling techniques to predict rare behavioral risks.

---
## Methodology
The dataset was derived from the National Survey on Consumption and Care Practices (ENCOPRAC 2022) conducted by INDEC, Argentina. The preprocessing included the handling of skip-patterns and imputation of non-response codes. Categorical variables (Education, Health Coverage, Risk Perception) were encoded as indicators.

Two distinct binary classification models were trained. One predicting lifetime consumption *with* prescription and another predicting lifetime consumption *without* prescription.

The non-prescription target presented a severe imbalance (Positive class < 2%). A standard approach yielded high accuracy but null sensitivity (Recall = 0.00).
The solution was the implementation of SMOTE on the training set to synthesize minority class examples based on nearest neighbors. The decision threshold was calibrated from 0.50 down to 0.15 to prioritize sensitivity, ensuring the detection of 59% of potential misuse cases.

---

## Results 

Feature importance analysis with Gini Impurity reveals that the two behaviors are governed by different mechanisms. Medical Consumption is strongly predicted by age and contact with the mental health system. It follows a clinical, structural pattern. On the other hand, on Non-Prescription Misuse the influence of age diminishes significantly. Instead, risk perception and other substances use history, like tobacco, emerge as dominant predictors.

![Feature Importance Comparison](images/dumbbell_chart.png)
*Figure 1: Dumbbell chart illustrating the shift in feature importance between the Medical Model in blue and the Misuse Model in orange.*

A correlation analysis confirms the direction of these effects. A high perception of risk acts as a significant deterrent (negative correlation) for self-medication. A history of tobacco consumption acts as a positive driver for tranquilizer misuse, suggesting a behavioral cluster of risk-taking.

![Direction of Effects](images/diverging_bars.png)
*Figure 2: Diverging bars displaying drivers (in green) and deterrents (in red) for each target variable.*

---

## Discussion
The findings suggest that public health interventions targeting tranquilizer misuse cannot rely on the same demographic profiling used for clinical patients. While medical consumption is a function of aging and healthcare access, misuse is a behavioral phenomenon driven by low risk perception. This implies that prevention campaigns should focus on psycho-education regarding risk, particularly among younger demographics who are invisible to standard clinical screenings.

---

## Reproducibility
To replicate this analysis:

1.  **Environment:** Python 3.9+ with libraries listed in `requirements.txt`.
2.  **Execution:** Run the Jupyter Notebook located in the `notebooks/` directory.
    ```bash
    pip install -r requirements.txt
    jupyter notebook notebooks/tranquilizer_misuse_analysis.ipynb
    ```

---

By **Juana Luz Carbajal** 

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/juanaluz/)
