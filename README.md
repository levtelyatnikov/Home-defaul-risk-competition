# Home-defaul-risk-competition
This .ipynb file is the my solution for Kaggle Home Default Risk Competition

## Cleaning.
I have performed general EDA analisys and workout diffent data problems such as outliers in "application" and "previous_application" datasets.

## Feature engineering
I have added features from credits' domain. There are features with nonlinear interaction: income ~ credit amount (payment rate - become the most important feature in LGBM, income over credit etc). Time features: (e.g. DAYS_EMPLOYED / DAYS_BIRTH - days worked by 1 day of life). Crossed features: (e.g. AMT_INCOME_TOTAL/ DAYS_BIRTH - income by each day of life). Next, I have created polynomial features with degree 3, which boosted the performance. Other categorical and numerical features were aggregated and statistics have been calculated. Other data in dataset has deep connections for example: bureau_balance connected to bureau which is connected to application. Thus, I did few levels of aggregation. In case of bureau, I first calculated sum, and mean for each status in bureau_balance and then merged with bureau and applied the second level aggregation (now numeric and categorical) by bureau ID. The same deep aggregation I applied to other tables. Numeric data aggregations includes count, mean, sum, std, min, max statistics.

In addition, the more advanced features were created. I decided to take into account not only frequencies of statuses but the longest runs of statuses (for example: CCCCXXCXXX - C=4, X=3). Moreover, the pairs of statuses in sequence may be important, so I calculated frequencies of CX, C0, XC, X1 etc. Since there are many such information, for each loan ID, I calculated regular statistics: mean, median, skew, std etc. I got around 500 features from statuses which gives us increase in around 0.003 without dimension reduction.

## Training

I started from logistic regression which gave me lower bound score on "application" and "bureau" dataset features.  I decided to move to decision trees algorithms. I tested two algorithms based on decision trees: CatBost and Light GBM. The performance of LGBM was slightly better 0.771 against 0.768 (accuracy) and these two results were much better than performance of logistic regression.


