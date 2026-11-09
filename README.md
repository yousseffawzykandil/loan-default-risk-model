\# Loan Default Risk Model



Predicts whether a borrower will miss loan payments, using Home Credit application data. Built with pandas and scikit-learn.



\## Data

Home Credit Default Risk, from Kaggle: https://www.kaggle.com/competitions/home-credit-default-risk

Only `application\_train.csv` is used (307,511 loans, 8.1% defaults). The data is not included in this repo. Download it and place it in a `data/` folder.



\## Method

\- Cleaned the data: replaced the placeholder value 365243 in `DAYS\_EMPLOYED` with missing, and created `AGE\_YEARS`.

\- Removed `CODE\_GENDER` and the ID column. Gender is not used, because it would be unfair in lending.

\- Stratified 80/20 train/test split, which keeps the 8% default rate in both parts.

\- Models: a dummy baseline, logistic regression (with imputing, scaling and one-hot encoding), and gradient boosting.

\- Metric: ROC-AUC, because accuracy is misleading when 92% of loans are repaid.



\## Results



| Model | ROC-AUC |

|---|---|

| Baseline (no skill) | 0.500 |

| Logistic regression | 0.746 |

| Gradient boosting | 0.756 |



If a lender reviews the riskiest 20% of applicants according to the boosting model:

\- 21.2% of them default, against 4.8% in the other 80%.

\- This group contains 52.4% of all defaults.



!\[ROC curve](images/roc\_curve.png)

!\[Feature importance](images/feature\_importance.png)



\## Main risk drivers

The three external credit scores (`EXT\_SOURCE\_1`, `EXT\_SOURCE\_2`, `EXT\_SOURCE\_3`) matter most, followed by the goods price and the credit amount. Importance shows what the model uses, not what causes default.



\## Limitations

\- Random split. A real lender would test on later loans.

\- The model relies heavily on external scores, so it works less well where they are missing.

\- No tuning and only one table. The other Home Credit files (previous loans, payment history) are unused.

\- Not checked for fairness across groups beyond removing gender.



\## Next steps

Add features from the other Home Credit tables, tune the model, and test for fairness.



\## How to run

1\. Create a virtual environment and run `pip install -r requirements.txt`.

2\. Download `application\_train.csv` into `data/`.

3\. Open `loan\_default\_model.ipynb` and run all cells.

