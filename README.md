

# Credit Card Fraud Classifier


## Overview

This repository implements a fraud classifier for credit card transactions using logistic regression. The project analyzes a simulated dataset of credit card transactions from January 2019 to December 2020, covering 1000 customers and 800 merchants. It focuses on identifying fraudulent transactions through variable creation, model selection, and evaluation.

Key features:
- **Dataset Split**: Training (June-December 2020: 555,719 transactions), Validation (January-December 2019: 1,296,657 transactions).
- **Variables**: Includes original features (e.g., amount, gender, state) and derived binary variables (e.g., high-fraud categories, states, jobs, age groups).
- **Methodology**: Logistic regression with stepwise selection, LASSO for variable shrinkage, cross-validation, and accuracy assessment.
- **Results**: Model achieves over 99% accuracy on both training and validation sets.

The repository includes the project report (PDF), R Markdown code for reproduction, and references to the dataset source.

## Table of Contents

- [Overview](#overview)
- [Files](#files)
- [Requirements](#requirements)
- [Installation and Setup](#installation-and-setup)
- [Usage](#usage)
- [Methods](#methods)
- [Results](#results)
- [References](#references)

## Files

- **`ProjectFall23_ua118.pdf`**: Comprehensive report including abstract, introduction, materials/methods, results/discussion, acknowledgements, references, and appendix.
- **`ProjectFall23_ua118.Rmd`**: R Markdown file with code for data loading, variable creation, model fitting (logistic regression, stepwise, LASSO, CV), and evaluation.

(Note: The dataset is not included but can be obtained from Kaggle or generated via Sparkov tool as referenced.)

## Requirements

### R Dependencies
- modeldata
- faraway
- ggplot2
- data.table
- dplyr
- olsrr
- epiDisplay
- StepReg
- caret
- glmnet

## Installation and Setup

1. Clone the repository:
   ```
   git clone https://github.com/uday-andotra/CreditCardFraudClassifier.git
   cd CreditCardFraudClassifier
   ```

2. Install R dependencies if not already present:
   ```
   install.packages(c("modeldata", "faraway", "ggplot2", "data.table", "dplyr", "olsrr", "epiDisplay", "StepReg", "caret", "glmnet"))
   ```

3. Download the dataset files (`fraudTest.csv` and `fraudTrain.csv`) from Kaggle (search for "credit card fraud" by Kartik Shenoy) and place them in your working directory as specified in the Rmd code.

## Usage

### Running the R Markdown
- Open `ProjectFall23_ua118.Rmd` in RStudio.
- Update file paths for datasets if necessary.
- Knit the document to HTML for visualizations, model summaries, and results.
- Key outputs: Contingency tables, model summaries (full, stepwise, LASSO), correlation matrix, cross-validation results, and accuracy metrics.

### Viewing the Report
- Open `ProjectFall23_ua118.pdf` for a detailed explanation, including tables, model equations, and fraud statistics.

## Methods

### Dataset and Variables
- Simulated transactions with fraud indicators.
- Derived binary variables based on fraud rates (e.g., `catShop_net` for "shopping_net" category, `stateHF` for high-fraud states like AK/CT).
- Continuous variables: Amount (`amt`), age, city population.

### Logistic Regression
- Models fraud as binary outcome using sigmoid function: \( f(x) = \frac{1}{1 + e^{-x}} \).
- Full model includes all variables; tested against null model via likelihood ratio test.
- Stepwise selection (backward, SL=0.05) for variable reduction.
- LASSO regression for coefficient shrinkage and selection (alpha=1, 10-fold CV for lambda).
- 10-fold cross-validation for model refinement.

For details on equations and variable partitions, refer to the PDF report.

## Results

| Model Aspect            | Key Findings |
|-------------------------|--------------|
| Null vs. Full Model    | LR test: Chi-squared = 2794.565, p-value < 0.05 (reject null). |
| Full Model             | Significant variables include `amt`, `catShop_net`, `catMisc_net`, etc. (see summary in report). |
| Stepwise Logistic      | Reduced to key variables like `city_pop`, `amt`, `age`, `popG500`, etc. |
| LASSO Coefficients     | Shrunk coefficients; e.g., intercept ~ -7.5, `amt` ~ 0.003. |
| Cross-Validation       | MAE = 0.0075; refined coefficients for final model. |
| Model Accuracy         | Training: >99%, Validation: >99%. |

The model effectively differentiates frauds using derived binaries, with high accuracy but notes potential biases from small sample sizes in some partitions.

## References

1. Most Scammed States In America: Financial Fraud Statistics - Forbes Advisor.
2. Introduction to Linear Regression Analysis, 6th Edition (Wiley, 2021).

Dataset: Generated via Sparkov (GitHub: Brandon Harris), available on Kaggle (Kartik Shenoy).
