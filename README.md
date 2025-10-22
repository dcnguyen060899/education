# Education Project (DATA 5100-02) - School Poverty, Institutional Resources, and Academic Achievement: A Mediation Analysis of U.S. High Schools

## Project Overview:
This project examines whether schools serving higher concentrations of economically disadvantaged students systematically offer fewer college-preparatory opportunities, and whether these institutional differences help explain achievement gaps in ACT scores. Using data from 7,227 U.S. high schools, we integrated socioeconomic indicators with institutional resource measures to uncover the structural factors that contribute to standardized test performance disparities. Our analysis reveals that while high-poverty schools face significant resource disadvantages—offering fewer Advanced Placement courses, reduced calculus access, higher suspension rates, and elevated chronic absenteeism—these institutional differences account for only approximately 12% of the poverty-achievement relationship, suggesting comprehensive interventions must address factors beyond school-level resources.

## Data
###Data sourced from three national educational databases:

- EdGap.org: School-level ACT/SAT scores and socioeconomic indicators (unemployment rates, college degree percentages, family structures, median household income, and free/reduced-price lunch eligibility) for 7,986 schools
  - From my repo: [EdGap Data Access](https://github.com/dcnguyen060899/education/blob/main/data/EdGap_data.xlsx) OR
  - [Professor Brian Fischer's Repo](https://github.com/brian-fischer/DATA-5100/blob/main/EdGap_data.xlsx)


- Common Core of Data (CCD): School characteristics from the National Center for Education Statistics (NCES) for the 2016-2017 academic year, including school names, locations, types, educational levels, and charter status
  - From my repo: [NCES Common Core of Data](https://github.com/dcnguyen060899/education/blob/main/data/ccd_sch_029_1617_w_1a_11212017.csv) OR
  - [Alternative Link](https://www.dropbox.com/scl/fi/fkafjk8902sq8ptxh94r2/ccd_sch_029_1617_w_1a_11212017.csv?rlkey=gucrdz5f6e38bezz2y3yalxbw&e=1&dl=0)
- Civil Rights Data Collection (CRDC): Institutional resource measures for the 2015-16 school year, including AP/IB programs, advanced mathematics offerings, teacher qualifications, counselor availability, disciplinary rates, and chronic absenteeism
  - [CRDC Data Access](https://github.com/dcnguyen060899/education/blob/main/data/CRDC_2015-16_School_Data.csv)
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




## Author
**Duy Nguyen**  
MS in Data Science - Seattle University

Email: [dnguyen44@seattleu.edu](mailto:dnguyen44@seattleu.edu)  
LinkedIn: [https://www.linkedin.com/in/duwe-ng/](https://www.linkedin.com/in/duwe-ng/)


## License
This project is licensed under the [MIT License]() - Copyright (c) 2025 Duy Nguyen
