# ShowTime OTT — Linear Regression Analysis

## Project Overview

This project analyzes first-day content viewership on the **ShowTime OTT platform** and develops a multiple linear regression model to identify the factors associated with viewership and predict first-day content views.

The analysis covers the complete data science workflow:

- Exploratory Data Analysis (EDA)
- Data quality checks
- Univariate, bivariate, and multivariate analysis
- Outlier analysis
- Feature engineering
- Categorical variable encoding
- Multiple Linear Regression using OLS
- Regression assumption testing
- Multicollinearity analysis using VIF
- Influence analysis using Cook's Distance
- Model performance and generalization evaluation
- Business insights and recommendations

## Business Objective

The objective is to identify the key factors influencing first-day content viewership and build a Linear Regression model that can predict first-day views for upcoming releases.

**Target variable:** `views_content` — first-day content views, measured in millions.

## Dataset

The dataset contains **1,000 content releases and 8 variables** covering platform traffic, advertising, trailer engagement, release timing, season, genre, sporting-event overlap, and first-day content views.

The dataset was provided as part of Great Learning coursework and is **not included in this repository** due to data-sharing restrictions.

### Variables

| Variable | Type | Description |
|---|---|---|
| `visitors` | Numerical | Average platform visitors in the past week |
| `ad_impressions` | Numerical | Advertising impressions for the content |
| `major_sports_event` | Categorical / Binary | Whether a major sports event occurred on the release day |
| `genre` | Categorical | Content genre |
| `dayofweek` | Categorical | Day on which the content was released |
| `season` | Categorical | Season in which the content was released |
| `views_trailer` | Numerical | Trailer views |
| `views_content` | Numerical | First-day content views — target |

## Exploratory Data Analysis

The EDA included:

- Dataset structure and data-quality checks
- Distribution analysis of numerical variables
- Univariate analysis of categorical variables
- Outlier screening using the IQR method
- Numerical predictor vs. target analysis
- Viewership comparison by release day
- Viewership comparison by season
- Impact of major sporting events
- Genre-level viewership analysis
- Pairwise relationships and correlation analysis
- Multivariate analysis

Key observations included:

- The dataset contained **no duplicate rows and no missing values**.
- `views_trailer` showed the strongest correlation with first-day viewership (**r = 0.754**).
- `visitors` had a weaker positive correlation (**r = 0.259**).
- `ad_impressions` showed very little linear correlation with viewership (**r = 0.050**).
- First-day viewership varied across release days and seasons.
- Releases coinciding with major sporting events had lower average first-day viewership.

## Data Preprocessing

The preprocessing workflow included:

1. Evaluating candidate feature transformations.
2. Testing a log transformation for trailer views.
3. Testing an advertising-intensity feature.
4. Testing a weekend indicator.
5. Retaining the raw specification based on the analysis results.
6. One-hot encoding categorical variables using `drop_first=True`.
7. Splitting the data into training and testing sets using an **80/20 split** with `random_state=42`.

The final training set contained **800 releases** and the test set contained **200 releases**.

## Linear Regression Model

A multiple linear regression model was fitted using **Ordinary Least Squares (OLS)** with:

- Platform visitors
- Advertising impressions
- Trailer views
- Major sporting event
- Genre
- Day of week
- Season

The encoded feature set contained **20 predictors**.

### Model Performance

| Metric | Training | Testing |
|---|---:|---:|
| MAE | 0.0389M | 0.0399M |
| RMSE | 0.0489M | 0.0500M |
| MAPE | 8.61% | 9.08% |
| R² | 0.7868 | **0.7743** |

The model explained **77.43% of the variation in first-day viewership on the held-out test data**.

The training-to-testing R² difference was **0.0125**, providing a generalization check against substantial overfitting.

## Regression Assumption Testing

The project formally evaluated the major regression assumptions:

| Assumption / Diagnostic | Test | Result |
|---|---|---|
| Linearity | Residuals vs. fitted/predictors | No systematic pattern |
| Independence | Durbin-Watson | 2.038 |
| Normality | Shapiro-Wilk | p = 0.4376 |
| Homoscedasticity | Breusch-Pagan | p = 0.4245 |
| Multicollinearity | VIF | Maximum = 2.75 |
| Influence | Cook's Distance | Maximum = 0.0164 |

The report concludes that the regression assumptions were reasonably satisfied and that no high-influence observations required removal.

## Key Findings

The analysis identified several statistically significant relationships:

- **Trailer views** were the strongest predictor in the regression model.
- **Platform visitors** were positively associated with first-day viewership.
- **Major sporting-event overlap** was negatively associated with first-day viewership.
- Release day showed meaningful differences relative to Friday, the reference category.
- Season also showed statistically significant differences relative to Fall, the reference category.
- **Advertising impressions** were not statistically significant in the fitted model.
- The individual **genre coefficients were not statistically significant** at the 5% level.

A reduced-model robustness check also found that removing advertising impressions and genre variables did not materially reduce explanatory power.

## Business Recommendations

Based on the analysis, the report recommends focusing on:

- Increasing trailer engagement before release.
- Considering release-calendar adjustments based on observed day-of-week patterns.
- Avoiding major sporting-event clashes where practical.
- Considering seasonal release patterns when planning launches.
- Evaluating advertising effectiveness beyond impression volume alone, since raw advertising impressions did not show a statistically significant relationship with first-day viewership in this model.

These recommendations are based on the relationships observed in the analyzed dataset and should not be interpreted as causal effects without further experimentation.

## Repository Contents

```text
showtime-ott-linear-regression/
│
├── README.md
├── Linear_Regression_Project.html
└── ShowTime_Linear_Regression_Report.pdf
```

The HTML file contains the detailed analysis and visualizations, while the PDF contains the structured project report.

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Statsmodels
- Scikit-learn
- Jupyter Notebook

## Project Documentation

- **Analysis:** `Linear_Regression_Project.html`
- **Project Report:** `ShowTime_Linear_Regression_Report.pdf`

## Author

**Shankar Ganesh D**

Data Science | Data Analytics
