# HIV Protease Inhibitor Resistance Predictor

A machine learning project that predicts HIV drug resistance from viral protease mutation data, using genotype-phenotype data from the Stanford HIV Drug Resistance Database (HIVdb).

## Project Goal

HIV replicates rapidly and error-prone, generating mutations that can make the virus resistant to antiretroviral drugs. Clinicians use genotypic resistance testing — sequencing a patient's virus and checking for known resistance mutations — to guide treatment decisions. This project builds a classifier that predicts resistance to a specific protease inhibitor (PI) drug, Nelfinavir (NFV), based on the pattern of mutations present in the viral protease sequence.

## Data

- **Source**: [Stanford HIV Drug Resistance Database — Genotype-Phenotype Datasets](https://hivdb.stanford.edu/_wrapper/download/GenoPhenoDatasets/PI_DataSet.txt)s
- **Dataset used**: PI (protease inhibitor) high-quality filtered dataset — phenotype results from isolates tested with the PhenoSense assay, with redundant/ambiguous sequences excluded
- **Note**: Raw data is not included in this repository (see `.gitignore`). To reproduce, download the dataset from the link above and place it in `data/raw/`.


## Setup

```bash
# clone the repo
git clone https://github.com/clappercm/hiv-resistance-predictor
cd hiv-resistance-predictor

# create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows

# install dependencies
pip install -r requirements.txt
```

Download the PI genotype-phenotype dataset from the Stanford HIVdb link above and place it in `data/raw/`.

## Approach

1. Load and clean genotype-phenotype data for the chosen drug
2. Define resistance labels from fold-change susceptibility values
3. Engineer features from mutation data (one-hot encoding by position)
4. Train and evaluate classification models (baseline → improved) using scikit-learn
5. Visualize mutation patterns and model performance with seaborn

## Status

First baseline model

## Results

Drug: NFV
** Chosen for having the most available phenotype data among the protease inhibitors in the dataset
Model: Logistic Regression (baseline)
Accuracy: 95.3% on held out test data (381 isolates)
Key finding: The model produced 8 false negatives. Isolates that were actually drug-resistant but predicted as susceptible. In clinical context, this is the MOST concerning error type. This means it could lead to prescribing a drug that won't work. By comparison, 10 isolates were false positives (predicted resistant when actually susceptible).
Next step: Try a Random Forest model to see if it improves on this baseline and compare feature importance between the two models.

## Author

Colin Clapper B.S. Bioinformatics (Computational Sciences)
September 21, 2026
