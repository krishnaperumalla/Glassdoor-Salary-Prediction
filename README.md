# Glassdoor-Salary-Prediction
[![Ask DeepWiki](https://devin.ai/assets/askdeepwiki.png)](https://deepwiki.com/krishnaperumalla/Glassdoor-Salary-Prediction)

This project focuses on predicting job salaries using data scraped from Glassdoor. It involves a comprehensive data cleaning and feature engineering process, followed by the implementation and evaluation of various regression models to provide reliable salary estimates. The goal is to build a tool that can assist both job seekers in negotiating compensation and employers in setting competitive salaries.

## Problem Statement

In a competitive job market, understanding salary expectations is crucial for both job seekers and employers. However, publicly available data from sources like Glassdoor often suffers from inconsistencies, missing values, and unstructured formats (e.g., salary ranges, varied job titles). This project aims to overcome these challenges by building a robust regression model that can:
- Accurately predict job salaries based on key attributes.
- Identify the most significant predictors of compensation.
- Handle data inconsistencies to provide reliable estimates for better decision-making in recruitment and career planning.

## Data Processing and Feature Engineering

The initial dataset required significant preprocessing to be suitable for machine learning. The following steps were taken:

1.  **Salary Parsing**: The `Salary Estimate` column, given as a range (e.g., "$53K-$91K"), was converted into an average annual salary in thousands (e.g., 72.0).
2.  **Company Age**: A `COMPANY_AGE` feature was created by subtracting the `Founded` year from the current year (2025).
3.  **Job Title Simplification**:
    *   **Seniority Level**: Job titles were parsed to extract seniority levels (`junior`, `mid`, `senior`).
    *   **Job Function**: Core job functions like `data_scientist`, `data_engineer`, and `data_analyst` were identified.
    *   **Specialization**: Specializations such as `healthcare`, `finance`, and `research` were extracted.
4.  **Data Cleaning**:
    *   Irrelevant columns (`Job Description`, `Competitors`) were removed.
    *   Inconsistent values (e.g., `-1`) were replaced with `NaN`.
    *   Company names were cleaned by removing rating suffixes (e.g., "Tecolote Research\n3.8" -> "Tecolote Research").
5.  **Handling Missing Values**: Missing data in numerical columns (`Rating`, `Size`, `Revenue`, `COMPANY_AGE`) and categorical columns (`Headquarters`, `Industry`, `Sector`) was imputed using the mean and mode, respectively.
6.  **Categorical Encoding**:
    *   High-cardinality features like `Job Title`, `Company Name`, and `Location` were encoded using their mean salary estimates.
    *   Low-cardinality features (`Type of ownership`, `specialization`) were one-hot encoded.
7.  **Outlier Treatment**: Outliers in numerical features were capped using the Interquartile Range (IQR) method to prevent them from skewing the model.

## Exploratory Data Analysis

EDA revealed several key insights:

*   **Salary Distribution**: The distribution of salaries is right-skewed, with a mean of $102.4k and a median of $98.0k.
*   **Job Title vs. Salary**: Data scientists command the highest median salary, followed by data engineers, while data analysts have the lowest median salary among the top job titles.
*   **Correlations**: `COMPANY_AGE` and `Size` showed a moderate positive correlation with `Salary Estimate`. However, `Rating` had a very weak relationship with salary.



## Model Implementation and Evaluation

Several regression models were trained and evaluated to find the best performer. The data was split into an 80% training set and a 20% testing set.

| Model                     | MAE    | MSE      | RMSE    | R² Score | Accuracy (%) |
| ------------------------- | ------ | -------- | ------- | -------- | ------------ |
| **XGBRegressor**          | **3.55** | **82.29**  | **9.07**  | **0.884**  | **96.18%**   |
| RandomForestRegressor     | 4.35   | 88.57    | 9.41    | 0.875    | 95.33%       |
| DecisionTreeRegressor     | 4.31   | 141.13   | 11.88   | 0.802    | 95.55%       |
| GradientBoostingRegressor | 6.13   | 119.66   | 10.94   | 0.832    | 93.39%       |
| Linear Regression         | 7.94   | 149.39   | 12.22   | 0.790    | 91.65%       |
| SVR                       | 6.62   | 143.77   | 11.99   | 0.798    | 92.49%       |

### Final Model

The **XGBoost Regressor** was selected as the final model due to its superior performance across all metrics, achieving an **R² score of 0.88** and an **accuracy of 96.18%**. Its low MAE and RMSE indicate high predictive reliability, making it a robust choice for this task.




## How to Run

To run this project locally, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/krishnaperumalla/Glassdoor-Salary-Prediction.git
    cd Glassdoor-Salary-Prediction
    ```

2.  **Install dependencies:**
    It is recommended to use a virtual environment.
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn xgboost
    ```

3.  **Run the Jupyter Notebook:**
    Launch Jupyter Notebook and open `Glassdoor_prediction.ipynb` to explore the complete analysis and model implementation.
    ```bash
    jupyter notebook Glassdoor_prediction.ipynb
    ```

## Conclusion

This project successfully demonstrated the process of building a salary prediction model from raw Glassdoor data. Through careful feature engineering and model selection, the XGBoost Regressor proved to be a highly effective tool for forecasting salaries. The model provides valuable insights into the factors that determine compensation, serving as a useful resource for both professionals and organizations navigating the job market.

## XGBoost Prediction Visualization


## License

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.
