\# Methodology Notes: Feature Engineering \& Limitations



\## Feature Engineering Rationale



\### Lag Features

The model incorporates 2-, 4-, 8-, and 12-week lags on four key climate variables:

temperature, PM2.5, precipitation, and heat wave days. These lag lengths were chosen

to reflect the clinical and epidemiological understanding of how environmental exposures

translate into measurable health outcomes.



Respiratory illness does not respond instantaneously to air quality changes. PM2.5

particles cause cumulative airway inflammation, and population-level disease rates

typically rise 2–4 weeks after a sustained pollution event. The 8- and 12-week lags

capture slower-developing effects, such as chronic respiratory deterioration following

a prolonged heat or pollution episode, and seasonal patterns where exposure in one

period predicts admissions in the next.



For heat-related admissions, the physiological rationale is similar: sustained heat

exposure over multiple weeks strains cardiovascular and respiratory systems, and

hospital admission rates tend to lag peak temperature events by 1–4 weeks. Including

lags up to 12 weeks also helps capture the tail effects of summer heat waves that

extend into autumn admission patterns.



\### Rolling Window Features

Four- and eight-week rolling means were computed for temperature, PM2.5, and AQI.

Where lag features capture the value at a specific prior point in time, rolling means

capture the sustained average exposure level over a window — a distinct and

complementary signal. A single anomalous week of high PM2.5 may matter less than

four consecutive weeks of elevated exposure. Rolling averages smooth out week-to-week

noise and better represent the kind of cumulative burden that drives population-level

health outcomes.



The combination of lag features and rolling windows means the model can distinguish

between a brief spike (captured by lags but not strongly by rolling means) and a

prolonged elevation (captured strongly by both), which is important for correctly

weighting acute versus chronic environmental health effects.



\### Temporal Split

The dataset was split strictly by time: training on 2015–2021, validation on 2022–2023,

and testing on 2024–2025. No shuffling was applied at any stage. This is essential for

time-series data because shuffling would allow the model to learn from future

observations during training, artificially inflating performance metrics. The strict

temporal split ensures that reported R², RMSE, and MAE values reflect genuine

out-of-sample predictive performance.



\---



\## Limitations \& Future Work



\### Dataset

The dataset is a synthetic compilation sourced from Kaggle, designed to synthesize

patterns from multiple authoritative sources including the World Bank, WHO, and

national air quality monitoring networks. While this makes it well-structured and

complete (100% of values present, no missing data), it also means the results cannot

be directly generalised to real-world policy decisions without validation against

raw observational data. The absence of missing values in particular is atypical of

real environmental health datasets, where gaps in monitoring coverage are common,

especially in lower-income countries.



\### Mental Health Index

Across all four model architectures: Ridge Regression, Random Forest, XGBoost, and

LSTM; the `mental\_health\_index` target was effectively unpredictable from

environmental variables alone (R² ≈ 0.00 or negative across all val and test

evaluations). This consistent failure is informative rather than merely a limitation:

it suggests that climate and air quality variables are not meaningful predictors of

population-level mental health outcomes at weekly resolution. Mental health is

primarily driven by socioeconomic, social, and psychological factors — income

stability, access to services, social connectedness, housing security — none of which

are represented in the current feature set. Future work incorporating socioeconomic

indicators (e.g., unemployment rate, healthcare access indices, Gini coefficient)

alongside environmental variables would be needed before any predictive model for

mental health outcomes could be considered viable.



\### Correlation vs Causation

All findings in this project identify correlational relationships between environmental

conditions and health outcomes. The observational, cross-sectional nature of the data

means causal claims cannot be made. For example, while PM2.5 is the strongest

predictor of respiratory disease rate (r ≈ 0.76), this does not establish that PM2.5

directly causes respiratory illness at the observed rates — confounding factors such

as urbanisation, healthcare access, and pre-existing population health may mediate

or moderate this relationship.



\### Future Work

\- Incorporating socioeconomic variables (income inequality, healthcare access,

&#x20; urbanisation) to improve mental health prediction and refine other targets

\- Extending the LSTM sequence window to 52 weeks to capture full annual cycles

\- Applying SHAP analysis to the LSTM outputs (currently only available for XGBoost)

&#x20; to enable sequential feature attribution

\- Validating findings against raw observational datasets from WHO and national

&#x20; health agencies

