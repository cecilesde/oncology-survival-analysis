# Oncology Survival Analysis

Survival analysis and ML-based mortality prediction on public oncology datasets, built as part of a personal research portfolio in computational oncology.

## Projects

### 1. TCGA Lung Adenocarcinoma
**Question**: Do specific mutation profiles influence survival outcomes 
in lung adenocarcinoma patients?

**Dataset**: 566 patients, 38 clinical variables, 225k somatic mutations 
(TCGA PanCancer Atlas, via cBioPortal)

**Analyses**:
- Exploratory data analysis: patient demographics, tumour stage distribution
- Kaplan-Meier survival curves stratified by tumour stage and mutation status
- KRAS subtype analysis and co-mutation patterns (STK11, KEAP1)
- Multivariable Cox proportional hazards model
- ML-based mortality prediction (Random Forest, XGBoost)

**Key biological question**: KRAS is mutated in ~30% of lung adenocarcinomas. 
Co-occurring mutations in STK11 and KEAP1 define aggressive subtypes with 
poor prognosis — can we predict this from genomic data alone?

### 2. METABRIC Breast Cancer
- Kaplan-Meier and Cox PH survival analysis
- Nottingham Prognostic Index (NPI) validation
- Confounding by indication analysis
- ML-based survival prediction

## Methods

### Kaplan-Meier Estimator
The survival function S(t) is estimated as:

$$S(t) = \prod_{t_i \leq t} \left(1 - \frac{d_i}{n_i}\right)$$

where $d_i$ is the number of events (deaths) at time $t_i$ and $n_i$ is the 
number of patients at risk just before $t_i$. Censored observations are 
accounted for by removing patients from the risk set without counting them 
as events.

Group comparisons are assessed with the log-rank test (H₀: identical 
survival functions across groups).

### Cox Proportional Hazards Model
The hazard function for patient $i$ is modelled as:

$$h(t | X_i) = h_0(t) \cdot \exp(\beta^T X_i)$$

where $h_0(t)$ is the baseline hazard, $X_i$ the covariate vector 
(age, stage, mutation status), and $\exp(\beta_j)$ the hazard ratio 
for covariate $j$. The proportional hazards assumption is verified 
via Schoenfeld residuals.

### ML-based Mortality Prediction
Binary classification (death within 24 months) using XGBoost and 
Random Forest. Features include clinical variables and top somatic 
mutation indicators. Model evaluation via time-aware cross-validation 
with AUC-ROC and Brier score.

## Stack
Python · pandas · numpy · lifelines · scikit-learn · XGBoost · matplotlib · seaborn

## Data Sources
All datasets are publicly available:
- TCGA Lung Adenocarcinoma via [cBioPortal](https://www.cbioportal.org)
- METABRIC via [cBioPortal](https://www.cbioportal.org)

Download from cBioPortal:
- https://www.cbioportal.org/study/summary?id=luad_tcga_pan_can_atlas_2018

Files needed:
- data_clinical_patient.txt
- data_mutations.txt"

## Author
Cécile Soudé — MSc Biomedical Engineering, Imperial College London
[LinkedIn](www.linkedin.com/in/cécile-soudé-384027218)
