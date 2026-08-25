# Analyse des données TETE de l'ADEME
### ADEME TETE Data Analysis

Analyse des caractéristiques démographiques et financières associées aux niveaux d'engagement des intercommunalités françaises dans le programme **Territoire Engagé Transition Écologique (TETE)**.

*Data analysis of demographic and financial characteristics associated with the engagement of French intermunicipal authorities in the **Territoire Engagé Transition Écologique (TETE)** programme.*

**[🇫🇷 Version française](#-version-française) | [🇬🇧 English version](#-english-version)**

---

# 🇫🇷 Version française

## Présentation

Ce projet prolonge un travail d'analyse initié lors de mon stage à **l'ADEME Nouvelle-Aquitaine**.

L'objectif est d'explorer les liens entre les caractéristiques des **EPCI** (établissements publics de coopération intercommunale) et leur niveau d'engagement dans le programme **Territoire Engagé Transition Écologique (TETE)**.

Le projet reprend l'ensemble de la chaîne d'analyse en Python : préparation et croisement des données, analyse exploratoire, tests statistiques et modélisation.

Les résultats mettent en évidence des **associations statistiques** et ne doivent pas être interprétés comme des relations causales.

---

## Contexte

Le programme **Territoire Engagé Transition Écologique (TETE)** de l'ADEME accompagne les collectivités dans la structuration et l'amélioration de leurs politiques de transition écologique.

Il repose notamment sur deux référentiels :

- **CAE – Climat-Air-Énergie**, consacré aux politiques climatiques, énergétiques et de qualité de l'air ;
- **ECI – Économie Circulaire**, consacré aux politiques territoriales d'économie circulaire.

Les collectivités peuvent obtenir différents niveaux de reconnaissance selon leur progression dans ces démarches.

L'analyse porte ici sur les **EPCI**, c'est-à-dire les structures intercommunales regroupant plusieurs communes.

---

## Question d'analyse

Le projet cherche à répondre à la question suivante :

> **Les caractéristiques démographiques et financières des EPCI sont-elles associées à leur niveau d'engagement dans le programme TETE ?**

Trois caractéristiques sont étudiées plus particulièrement :

- la **population** ;
- le **potentiel fiscal par habitant** ;
- le **coefficient d'intégration fiscale (CIF)**.

L'objectif est notamment d'observer si la taille et les caractéristiques financières des intercommunalités sont associées aux niveaux obtenus dans les démarches CAE et ECI.

---

## Données

Le projet croise deux principales sources de données.

### Données TETE

La base TETE contient les informations relatives à l'engagement des collectivités dans le programme, notamment :

- les niveaux CAE ;
- les niveaux ECI ;
- les informations permettant d'identifier les collectivités.

### Données BANATIC

Les données BANATIC apportent des informations administratives, démographiques et financières sur les intercommunalités françaises.

Parmi les variables utilisées :

- population ;
- nature juridique ;
- revenus ;
- potentiel fiscal ;
- potentiel fiscal par habitant ;
- coefficient d'intégration fiscale (CIF).

Les deux bases sont principalement rapprochées à partir de leur **identifiant SIREN**.

Après nettoyage et appariement, la base finale utilisée pour l'analyse contient **425 EPCI**.

---

## Méthodologie

L'analyse est organisée en trois notebooks.

### 1. Préparation des données

`notebooks/01_data_cleaning.ipynb`

Cette première étape permet de construire la base d'analyse :

- importation des données TETE et BANATIC ;
- nettoyage et harmonisation des variables ;
- sélection des informations utiles ;
- appariement des EPCI à partir des identifiants SIREN ;
- contrôle des doublons et valeurs manquantes ;
- export de la base finale.

---

### 2. Analyse exploratoire

`notebooks/02_exploratory_analysis.ipynb`

Cette partie étudie notamment :

- la distribution des niveaux CAE et ECI ;
- les différences de population selon les niveaux CAE ;
- le potentiel fiscal par habitant ;
- les relations entre population, revenus et potentiel fiscal ;
- les principales différences démographiques et financières entre les EPCI.

L'analyse descriptive fait notamment apparaître une progression importante de la taille des EPCI avec le niveau CAE.

La population médiane passe d'environ **23 500 habitants pour les EPCI sans étoile CAE à plus de 500 000 habitants pour ceux ayant cinq étoiles**.

Les relations observées pour ECI sont moins marquées.

---

### 3. Analyse statistique

`notebooks/03_statistical_analysis.ipynb`

L'analyse statistique approfondit les relations observées lors de l'exploration des données.

Elle mobilise notamment :

- le **test de Kruskal-Wallis** ;
- la **corrélation de Spearman** ;
- des comparaisons deux à deux avec le **test de Mann-Whitney** et une correction de **Holm** ;
- l'analyse des facteurs d'inflation de variance (**VIF**) ;
- une **régression logistique ordinale** pour les niveaux CAE ;
- une **régression logistique binaire** pour ECI.

---

## Principaux résultats

### CAE

La population présente une relation positive nette avec le niveau CAE.

La corrélation de Spearman entre population et niveau CAE est d'environ **0,53**.

Dans le modèle ordinal, la population, le potentiel fiscal par habitant et le CIF présentent tous une association positive et statistiquement significative avec les niveaux CAE.

Toutes choses égales par ailleurs :

- une population supérieure de **10 %** est associée à environ **10 % de chances relatives supplémentaires** d'appartenir à une catégorie CAE plus élevée ;
- une population supérieure de **50 %** est associée à environ **51 % de chances relatives supplémentaires** ;
- **100 € supplémentaires de potentiel fiscal par habitant** sont associés à environ **32 % de chances relatives supplémentaires** ;
- une augmentation de **0,1 du CIF** est associée à environ **28 % de chances relatives supplémentaires**.

### ECI

Les niveaux ECI sont davantage concentrés à zéro et les catégories supérieures comportent peu d'observations.

L'analyse distingue donc :

- **316 EPCI sans étoile ECI** ;
- **109 EPCI avec au moins une étoile ECI**.

Dans le modèle logistique, la **population** reste positivement et significativement associée à la présence d'au moins une étoile ECI.

En revanche, le potentiel fiscal par habitant et le CIF ne présentent pas d'association statistiquement significative une fois les variables considérées conjointement.

---

## Interprétation

Les résultats suggèrent que les **EPCI de plus grande taille tendent à présenter des niveaux d'engagement TETE plus élevés**, particulièrement pour CAE.

Les caractéristiques financières étudiées apparaissent également associées aux niveaux CAE, tandis que leur relation avec ECI est moins nette.

Ces résultats restent exploratoires. Ils ne permettent pas d'affirmer que la taille ou les ressources financières causent directement un meilleur niveau d'engagement.

D'autres facteurs non présents dans les données — comme les moyens humains, les capacités d'ingénierie, l'organisation administrative, les priorités politiques ou l'ancienneté des politiques environnementales — peuvent également contribuer aux différences observées.

---

## Structure du projet

```text
ADEME-transition-data-analysis/
│
├── data/
│   ├── raw/
│   │   ├── données TETE
│   │   └── données BANATIC
│   │
│   └── processed/
│       └── tete_epci_clean.csv
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   └── 03_statistical_analysis.ipynb
│
├── .gitignore
└── README.md
```

---

## Outils utilisés

Le projet a été réalisé en **Python** avec notamment :

- `pandas` — préparation et manipulation des données ;
- `numpy` — calcul numérique ;
- `scipy` — tests statistiques ;
- `statsmodels` — modèles statistiques ;
- Jupyter Notebook — développement et présentation des analyses.

---

## Origine du projet

Ce projet a été développé personnellement à partir d'un travail d'analyse initié au cours de mon stage à **l'ADEME Nouvelle-Aquitaine**.

L'objectif était de prolonger cette première exploration professionnelle en construisant un projet Python reproductible allant des données brutes jusqu'à l'analyse statistique.

---

# 🇬🇧 English version

## Overview

This project extends analytical work initiated during my internship at **ADEME Nouvelle-Aquitaine**.

It explores whether the demographic and financial characteristics of French **intermunicipal authorities (EPCIs)** are associated with their level of engagement in the **Territoire Engagé Transition Écologique (TETE)** programme.

The project covers the full analytical workflow in Python: data preparation and matching, exploratory data analysis, statistical testing and modelling.

The results identify **statistical associations** and should not be interpreted as causal relationships.

---

## Context

**Territoire Engagé Transition Écologique (TETE)** is an ADEME programme supporting French local authorities in structuring and improving their ecological transition policies.

The programme includes two complementary frameworks:

- **CAE – Climate-Air-Energy** (*Climat-Air-Énergie*);
- **ECI – Circular Economy** (*Économie Circulaire*).

Local authorities can achieve different recognition levels according to their progress within these frameworks.

This analysis focuses on French **EPCIs**, public intermunicipal authorities grouping several municipalities.

---

## Research question

The project investigates the following question:

> **Are the demographic and financial characteristics of EPCIs associated with their level of engagement in the TETE programme?**

Three characteristics are examined more specifically:

- **population**;
- **fiscal potential per capita**;
- **coefficient of fiscal integration (CIF)**.

---

## Data

Two main data sources are combined:

- **TETE data**, providing CAE and ECI engagement information;
- **BANATIC data**, providing administrative, demographic and financial characteristics of French intermunicipal authorities.

The datasets are primarily matched using **SIREN identifiers**.

After cleaning and matching, the final analytical dataset contains **425 EPCIs**.

---

## Methodology

The analysis is organised into three notebooks:

### 1. Data cleaning

`notebooks/01_data_cleaning.ipynb`

Import, cleaning, variable selection, SIREN matching, quality checks and construction of the final analytical dataset.

### 2. Exploratory data analysis

`notebooks/02_exploratory_analysis.ipynb`

Exploration of CAE and ECI ratings and their relationships with population and financial characteristics.

Median population increases from approximately **23,500 inhabitants among EPCIs with no CAE stars to more than 500,000 among those with five stars**.

### 3. Statistical analysis

`notebooks/03_statistical_analysis.ipynb`

The statistical analysis includes:

- Kruskal-Wallis tests;
- Spearman rank correlation;
- pairwise Mann-Whitney tests with Holm correction;
- variance inflation factors (VIF);
- ordinal logistic regression for CAE;
- binary logistic regression for ECI.

---

## Main findings

### CAE

Population is clearly positively associated with CAE ratings.

The Spearman correlation between population and CAE rating is approximately **0.53**.

In the ordinal model, population, fiscal potential per capita and CIF are all positively and statistically significantly associated with higher CAE ratings.

Holding the other variables constant:

- a **10% larger population** is associated with approximately **10% higher odds** of belonging to a higher CAE category;
- a **50% larger population** is associated with approximately **51% higher odds**;
- an additional **€100 of fiscal potential per capita** is associated with approximately **32% higher odds**;
- a **0.1 increase in CIF** is associated with approximately **28% higher odds**.

### ECI

ECI ratings are more concentrated at zero, with relatively few observations in the highest categories.

The analysis therefore distinguishes between:

- **316 EPCIs with no ECI star**;
- **109 EPCIs with at least one ECI star**.

Population remains positively and statistically significantly associated with having at least one ECI star.

Fiscal potential per capita and CIF are not statistically significant once the variables are considered jointly.

---

## Interpretation and limitations

Overall, larger EPCIs tend to display higher levels of TETE engagement, particularly for CAE.

Financial characteristics are also associated with CAE ratings, while their relationship with ECI engagement is less clear.

These findings remain exploratory and should not be interpreted as causal effects. Other factors — including administrative capacity, staffing, political priorities, previous environmental policies or territorial context — may contribute to the observed relationships.

---

## Project structure

```text
ADEME-transition-data-analysis/
│
├── data/
│   ├── raw/
│   └── processed/
│       └── tete_epci_clean.csv
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   └── 03_statistical_analysis.ipynb
│
├── .gitignore
└── README.md
```

---

## Tools

The project was developed in **Python**, mainly using:

- `pandas`;
- `numpy`;
- `scipy`;
- `statsmodels`;
- Jupyter Notebook.

---

## Project background

This project was independently developed from analytical work initiated during my internship at **ADEME Nouvelle-Aquitaine**.

Its purpose is to extend this initial professional exploration into a reproducible Python project covering the workflow from raw data preparation to statistical analysis.
