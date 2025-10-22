# Education Project (DATA 5100-02) - School Poverty, Institutional Resources, and Academic Achievement: A Mediation Analysis of U.S. High Schools

## Project Overview:
This project examines whether schools serving higher concentrations of economically disadvantaged students systematically offer fewer college-preparatory opportunities, and whether these institutional differences help explain achievement gaps in ACT scores. Using data from 7,227 U.S. high schools, we integrated socioeconomic indicators with institutional resource measures to uncover the structural factors that contribute to standardized test performance disparities. Our analysis reveals that while high-poverty schools face significant resource disadvantages—offering fewer Advanced Placement courses, reduced calculus access, higher suspension rates, and elevated chronic absenteeism—these institutional differences account for only approximately 12% of the poverty-achievement relationship, suggesting comprehensive interventions must address factors beyond school-level resources.

## Data
### Data sourced from three national educational databases:

- EdGap.org: School-level ACT/SAT scores and socioeconomic indicators (unemployment rates, college degree percentages, family structures, median household income, and free/reduced-price lunch eligibility) for 7,986 schools
  - From my repo: [EdGap Data Access](https://github.com/dcnguyen060899/education/blob/main/data/EdGap_data.xlsx) OR
  - [Professor Brian Fischer's Repo](https://github.com/brian-fischer/DATA-5100/blob/main/EdGap_data.xlsx)


- Common Core of Data (CCD): School characteristics from the National Center for Education Statistics (NCES) for the 2016-2017 academic year, including school names, locations, types, educational levels, and charter status
  - From my repo: [NCES Common Core of Data](https://github.com/dcnguyen060899/education/blob/main/data/ccd_sch_029_1617_w_1a_11212017.csv) OR
  - [Alternative Link](https://www.dropbox.com/scl/fi/fkafjk8902sq8ptxh94r2/ccd_sch_029_1617_w_1a_11212017.csv?rlkey=gucrdz5f6e38bezz2y3yalxbw&e=1&dl=0)
- Civil Rights Data Collection (CRDC): Institutional resource measures for the 2015-16 school year, including AP/IB programs, advanced mathematics offerings, teacher qualifications, counselor availability, disciplinary rates, and chronic absenteeism
  - From my repo: [CRDC Data Access](https://github.com/dcnguyen060899/education/blob/main/data/CRDC_2015-16_School_Data.csv) OR
  - [Alternative Link](https://www.ed.gov/about/offices/list/ocr/docs/2015-16-crdc-data.zip) 

The processed datasets used in this analysis are available in the [data folder](https://github.com/dcnguyen060899/education/tree/main/data): 
- The initial dataset was cleaned after merging socioeconomic factors from the EdGap dataset with the NCES Common Core of Data, resulting in [education_clean.csv](https://github.com/dcnguyen060899/education/blob/main/data/education_clean.csv).
- Next, we integrated the Civil Rights Data Collection (CRDC) dataset, performed additional cleaning, and saved the result as [education_crdc_cleaned.csv](https://github.com/dcnguyen060899/education/blob/main/data/education_crdc_cleaned.csv).
- Finally, we conducted further iterative cleaning and created new columns (such as resource rates and standardized variables) to support more robust analysis, producing the final dataset [education_crdc_final.csv](https://github.com/dcnguyen060899/education/blob/main/data/education_crdc_final.csv).

## Requirements
This project requires the following Python packages:

- pandas: Data manipulation and analysis
- numpy: Numerical computations
- matplotlib: Basic plotting and customization
- seaborn: Statistical visualization
- scipy: Statistical testing
- statsmodels: Advanced statistical modeling
- scikit-learn: Machine learning utilities for imputation and preprocessing
- plotly: Interactive geographic visualizations
- openpyxl: A Python library for reading and writing Excel `.xlsx` files. It is included because your local machine requires it to load the EdGap dataset, which is provided in Excel format.

Environment:

- Python 3
- Jupyter Notebook/Lab or Visual Studio Code

All dependencies are listed in requirements.txt. Run pip install -r requirements.txt to install libraries.

## Analysis
The complete data preparation, cleaning, exploratory analysis, and statistical modeling are documented in [final_education_project_notebook.ipynb](https://github.com/dcnguyen060899/education/blob/main/code/final_education_project_notebook.ipynb), located in the project repository.

Our workflow summary:
1. **Data Preparation**
  - Loaded and merged three datasets using standardized 12-digit school identification codes (NCESSCH)
  - Filtered to traditional high schools with complete ACT data, resulting in 7,227 schools across 20 states
  - Achieved 96% match rate (NCESSCH School ID from datasets matched) across all three data sources
  - Standardized datetime formats and column names to lowercase snake_case conventions
  - Created unified, cleaned dataset ready for exploratory data analysis and modeling

2. **Data Quality Control**
  - Identified and corrected impossible values (negative ACT scores, negative free lunch percentages)
  - Set out-of-range values to NaN to preserve other valid information
  - Used iterative imputation (IterativeImputer from scikit-learn) for missing socioeconomic predictors
  - Removed duplicate entries and filtered to relevant school types (high schools only)
  - Validated completeness of final dataset

3. **Predictor Construction (Derived Columns)**
  - Converted raw counts (teachers, AP courses, enrollments) to rates per 100 students to standardize measures across different school sizes (mitigate size effect and account for opportunity metrics)
  - Created derived variables including total AP enrollment, total calculus enrollment, total chronic absenteeism, and total suspensions
  - Validated that rate variables showed minimal correlation with total enrollment, confirming successful removal of size confounding
    - However, even after converting AP Calculus counts to rate variables (per 100 students), the effect of school size remains a confounding factor. Larger schools tend to offer fewer AP Calculus courses per student, and this size-related pattern persists in the rate-based analysis. For a detailed explanation and supporting analysis, please refer to [final_education_project_notebook.ipynb](https://github.com/dcnguyen060899/education/blob/main/code/final_education_project_notebook.ipynb).
  - Standardized all predictors (mean=0, SD=1) for direct effect size comparison in regression models
  - Created poverty tertiles (low/medium/high) for Analysis of Variance (ANOVA) testing

4. **Exploratory Data Analysis**
  - Examined correlation patterns between socioeconomic factors and ACT scores using heatmaps
  - Visualized bivariate relationships using pair plots with regression lines
  - Analyzed geographic distribution of schools across 20 states using choropleth maps
  - Investigated resource disparities across poverty levels using grouped bar charts
  - Created boxplots to identify outliers in socioeconomic and resource variables

5. **Statistical and Regression Modeling**
  - Conducted Analysis of Variance (ANOVA) to test whether resource levels differ significantly across poverty groups
  - Fit multiple regression models to quantify the relationship between poverty, institutional resources, and ACT scores
  - Compared three models: (1) baseline socioeconomic model, (2) full model with institutional resources, (3) reduced model with significant predictors only
  - Assessed model fit using R-squared, Mean Absolute Error (MAE), and Root Mean Squared Error (RMSE)
  - Evaluated mediation effects by comparing poverty coefficients across models to determine the proportion of the poverty-achievement relationship explained by institutional resources

## Results
The complete findings and conclusions from this analysis are documented in the final communication eucation project report for a more technical audience: [Communicate-the-Results-Education.pdf](https://github.com/dcnguyen060899/education/blob/main/reports/Communicate%20the%20Results%20%7C%20Education.pdf), located in the reports folder. This report provides a comprehensive overview of how school poverty concentration relates to institutional resources and academic achievement, written for a general audience with clear explanations of statistical concepts.

## Main Findings:
1. **Resource Disparities Across Poverty Levels:**
  - High-poverty schools offer significantly fewer Advanced Placement courses (0.16 standard deviations below average) compared to low-poverty schools (0.17 standard deviations above average)
  - Calculus enrollment access shows even larger gaps: low-poverty schools average 0.38 SD above mean, while high-poverty schools average 0.24 SD below mean
  - High-poverty schools experience chronic absenteeism rates 0.44 SD above average and suspension rates 0.56 SD above average
  - All resource differences were statistically significant (all F > 67, all p < 0.001)

2. **Mediation Analysis:**
  - School-level poverty concentration (free/reduced lunch eligibility) is the strongest predictor of ACT scores, with a coefficient of -1.78 in the baseline model
  - Adding institutional resource variables (AP courses, calculus access, suspensions, absenteeism) reduces the poverty coefficient to -1.57
  - This represents a 12% mediation effect, meaning institutional resources explain approximately one-eighth of the poverty-achievement relationship
  - The remaining 88% operates through unmeasured mechanisms such as instructional quality, peer norms, family supports, and developmental impacts of economic stress

3. **Significant Predictors of ACT Performance:**
  - Calculus enrollment rate: +0.24 points per standard deviation increase
  - Suspension rate: -0.25 points per standard deviation increase
  - Chronic absenteeism rate: -0.14 points per standard deviation increase
  - AP course availability: +0.10 points per standard deviation increase (after controlling for school size)
  - School size shows a suppression effect: larger schools score higher despite offering fewer AP courses per capita

4. **Model Performance:**
  - Baseline socioeconomic model: R² = 0.628, MAE = 1.15, RMSE = 1.53
  - Full model with institutional resources: R² = 0.657, MAE = 1.11, RMSE = 1.47
  - Reduced model (significant predictors only): R² = 0.657, MAE = 1.11, RMSE = 1.47
  - Adding institutional resources improves predictive accuracy by approximately 3 percentage points

## Study Limitations
- Data from a single year (2016-2017 for CCD, 2015-16 for CRDC), limiting ability to assess trends over time
- Only 20 states represented in the final dataset, which may not generalize to all U.S. schools
- Institutional resources explain only 12% of the poverty-achievement relationship, indicating unmeasured factors play a larger role
- ACT scores are not available for all schools, potentially introducing selection bias
- Resource measures based on course offerings and enrollments may not capture instructional quality differences within courses

## Study Limitations
- Data from a single year (2016-2017 for CCD, 2015-16 for CRDC), limiting ability to assess trends over time
- Only 20 states represented in the final dataset, which may not generalize to all U.S. schools
- Institutional resources explain only 12% of the poverty-achievement relationship, indicating unmeasured factors play a larger role
- Resource measures based on course offerings and enrollments may not capture instructional quality differences within courses


## Author
**Duy Nguyen**  
MS in Data Science - Seattle University

Email: [dnguyen44@seattleu.edu](mailto:dnguyen44@seattleu.edu)  
LinkedIn: [https://www.linkedin.com/in/duwe-ng/](https://www.linkedin.com/in/duwe-ng/)


## License
This project is licensed under the [MIT License](LICENSE) - Copyright (c) 2025 Duy Nguyen
