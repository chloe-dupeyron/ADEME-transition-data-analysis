# ADEME Transition Data Analysis

Data analysis project on local ecological transition policies in France, developed from work initiated during an internship at ADEME Nouvelle-Aquitaine.

The project explores whether demographic and financial characteristics of French intermunicipal authorities (EPCIs) are associated with their level of engagement in the **Territoire Engagé Transition Écologique (TETE)** programme.

The analysis is exploratory: it identifies statistical associations and does not aim to establish causal relationships.

---

## Context

**Territoire Engagé Transition Écologique (TETE)** is an ADEME programme supporting local authorities in the implementation and continuous improvement of their ecological transition policies.

The programme includes two complementary frameworks:

- **CAE – Climate-Air-Energy** (*Climat-Air-Énergie*), covering climate, energy and air-quality policies;
- **ECI – Circular Economy** (*Économie Circulaire*), covering local circular-economy policies.

Local authorities receive ratings reflecting their level of progress within these frameworks. In the dataset used here, CAE ratings range from **0 to 5 stars**.

The analysis focuses on French **EPCIs** (*Établissements publics de coopération intercommunale*), which are intermunicipal public authorities grouping several municipalities.

---

## Research question

The project investigates the following question:

> Are the demographic and financial characteristics of EPCIs associated with their level of engagement in the TETE programme?

Three characteristics are examined more specifically:

- population;
- fiscal potential per capita;
- coefficient of fiscal integration (**CIF**).

The objective is to determine whether larger or financially different EPCIs tend to display different CAE and ECI engagement levels.

---

## Data

Two main data sources are combined:

### TETE data

The TETE dataset provides information on the engagement of local authorities in the programme, including:

- CAE ratings;
- ECI ratings;
- identification variables used to match local authorities across datasets.

### BANATIC data

BANATIC data provide administrative, demographic and financial information on French intermunicipal authorities.

Variables used during the project include:

- population;
- legal status;
- revenue;
- total fiscal potential;
- fiscal potential per capita;
- coefficient of fiscal integration (CIF).

The datasets are matched primarily using **SIREN identifiers**.

After cleaning, matching and filtering, the final analytical dataset contains **425 EPCIs**.

---

## Project structure

```text
ADEME-transition-data-analysis/
│
├── data/
│   ├── raw/
│   │   ├── TETE dataset
│   │   └── BANATIC dataset
│   │
│   └── processed/
│       └── tete_epci_clean.csv
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   └── 03_statistical_analysis.ipynb
│
├── outputs/
│
├── .gitignore
└── README.md
