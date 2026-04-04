# Making Air Quality Data Accessible: Predicting Respiratory Health Risks

## Project Overview
Climate and environmental factors, particularly air quality, temperature, and extreme weather, are strongly linked to negative health outcomes, especially respiratory illness. However, these relationships are often difficult for non-experts to interpret due to the complexity of the data.

This project addresses that gap by developing an interactive Power BI dashboard that allows users to explore how environmental conditions influence respiratory health outcomes across countries and regions from 2015–2025.

The system transforms complex, multi-dimensional data into clear, accessible visual insights to support public understanding of environmental health risks.

## Research Question
How do changes in climate and air quality metrics (e.g., PM2.5, AQI, temperature, extreme weather events) predict respiratory disease rates and heat-related hospital admissions across countries globally?

## Problem Statement
Non-expert users lack accessible tools to interpret the relationship between environmental conditions and respiratory health outcomes. This creates a disconnect between available data and meaningful understanding of climate-related health risks.

## Project Goals
- Analyze how environmental factors relate to respiratory health outcomes
- Identify key drivers of respiratory disease rates and heat-related hospital admissions
- Develop an interactive Power BI dashboard for non-technical users
- Translate complex climate-health data into clear, actionable insights

## Dataset
**Source:** https://www.kaggle.com/datasets/sohumgokhale/global-climate-health-impact-tracker-2015-2025/data

**Dataset Characteristics:**
- Weekly data from 2015 to 2025
- 25 countries across multiple global regions
- Climate, air quality, health, and socioeconomic variables
- 100% complete dataset (no missing values)

**Countries Included:** USA, India, China, Brazil, Nigeria, Germany, Japan, UK, France, Australia, Kenya, Mexico, Indonesia, Pakistan, Bangladesh, Egypt, South Africa, Canada, Spain, Italy, Thailand, Philippines, Vietnam, Argentina, Colombia

This dataset synthesizes patterns from multiple authoritative sources including:
- World Bank Climate Data
- WHO Global Health Observatory
- Climate reanalysis models
- Air quality monitoring networks
- National health statistics

## Methodology

### Data Processing
- Data cleaning and preprocessing using pandas
- Exploratory Data Analysis (EDA)
- Lag features (2, 4, 8, and 12-week lags) and rolling window averages (4-week and 8-week) engineered for key climate variables (temperature, PM2.5, precipitation) to capture delayed health responses to climate events
- Time-series and cross-country comparisons

### Modeling Approaches

#### Statistical Analysis
- Correlation analysis to examine relationships between environmental and health variables
- Autocorrelation analysis of health targets and climate lag features
    -Found that lagged health outcomes (e.g. heat-related admissions at r=0.63) carry stronger time-series signal than shifted climate inputs, informing the LSTM target-lag model design
- Time-series analysis to identify trends and patterns from 2015–2025
- Comparative analysis across countries, regions, and income levels

#### Machine Learning Models
To explore predictive relationships between environmental factors and respiratory health outcomes, the following models were used:

- **Ridge Regression:** Baseline linear model to quantify relationships between climate and air quality metrics (e.g., PM2.5, AQI) and health outcomes across both targets
- **Random Forest:** Captures non-linear relationships and interactions between variables; used with time-series cross-validation to prevent data leakage
- **XGBoost:** Gradient boosting model that builds on the Random Forest approach to improve predictive accuracy, particularly for respiratory disease rate and heat-related admissions
- **LSTM:** Recurrent neural network designed to capture delayed and sequential effects in weekly time-series data using a 26-week sliding window

### Modeling Objective
The goal of modeling is to estimate relationships between environmental conditions and respiratory disease rates and heat-related hospital admissions, not to establish causation. Model outputs are used to support interpretation within the dashboard.

## Tools and Technologies
- Python (pandas, scikit-learn, matplotlib, seaborn)
- Power BI (dashboard development)

## Dashboard Features
The interactive dashboard enables users to:
- Explore global respiratory health risks geographically
- Analyze trends in environmental conditions and health outcomes over time
- Examine relationships between air quality, climate, and health outcomes
- Compare countries, regions, and income levels
- Interact with filters (country, region, year, income level)

## Outputs
- Data-driven summaries
- Interactive visualizations
- Correlation insights between environmental and health variables

## Limitations
- The analysis identifies correlations, not causal relationships
- Results depend on dataset assumptions and data quality
- Complex environmental-health relationships are simplified for interpretability

## Target Users
- Non-expert urban residents
- Individuals with limited background in climate science or public health
- General users seeking accessible insights into environmental health risks

## Evaluation Metrics

### Quantitative
- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- R² (model performance)
- System reliability

### Qualitative
- 15–20 user test scenarios
- Evaluation based on:
  - Clarity
  - Interpretability
  - Usefulness for non-expert users

## Deliverables
- Python analysis (data preprocessing, statistical analysis, predictive modeling)
- Interactive Power BI dashboard
- Final project report

## Project Timeline

| Week | Milestone |
|------|-----------|
| Week 4 | Data cleaning, EDA, initial visualizations, dashboard structure |
| Week 5 | Analysis development and dashboard integration |
| Week 6 | Testing, refinement, prepare presentation, review key insights and conclusions |
| Week 7 | Finalize written report, deliver final submission, system completion |

## Expected Impact
This project demonstrates how complex environmental and health data can be transformed into accessible, interactive tools that support public understanding and data-driven decision making and awareness of environmental health risks.

## Team Members
- Emmanuel Adeoti
- Carolyn Chaves
- Kyle DeSormier
- Abi Kambanis

## References
Global Climate-Health Impact Tracker (2015–2025). Soham Gokhale. Kaggle. https://www.kaggle.com/datasets/sohumgokhale/global-climate-health-impact-tracker-2015-2025/data
