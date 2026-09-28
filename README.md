# Analyse des données TETE de l'ADEME

## ADEME TETE Data Analysis

Analyse des caractéristiques démographiques et financières des intercommunalités françaises et de leur niveau d'engagement dans le programme Territoire Engagé Transition Écologique (TETE).

Data analysis of the demographic and financial characteristics of French intermunicipal authorities and their level of engagement in the Territoire Engagé Transition Écologique (TETE) programme.

🇫🇷 [Version française](#-version-française) | 🇬🇧 [English version](#-english-version)

# 🇫🇷 Version française

## Présentation

Ce projet fait suite à un premier travail réalisé pendant mon stage à l'ADEME Nouvelle-Aquitaine.

L'objectif est d'étudier les liens entre certaines caractéristiques des EPCI (établissements publics de coopération intercommunale) et leur niveau d'engagement dans le programme Territoire Engagé Transition Écologique (TETE).

L'analyse a été réalisée en Python, depuis la préparation et le croisement des données jusqu'aux tests statistiques et à la modélisation.

Les résultats montrent des associations statistiques et ne permettent pas d'établir de relations de causalité.

## Contexte

Le programme Territoire Engagé Transition Écologique (TETE) de l'ADEME accompagne les collectivités dans leurs politiques de transition écologique.

Il comprend notamment deux référentiels :

- `CAE` : Climat-Air-Énergie, consacré aux politiques climatiques, énergétiques et de qualité de l'air
- `ECI` : Économie Circulaire, consacré aux politiques territoriales d'économie circulaire

Les collectivités peuvent obtenir différents niveaux de reconnaissance selon leur progression dans ces démarches.

Ce projet se concentre sur les EPCI, qui regroupent plusieurs communes au sein d'une même structure intercommunale.

## Question d'analyse

La question étudiée est la suivante :

> Les caractéristiques démographiques et financières des EPCI sont-elles associées à leur niveau d'engagement dans le programme TETE ?

Trois variables sont étudiées plus particulièrement :

- la population
- le potentiel fiscal par habitant
- le coefficient d'intégration fiscale (CIF)

L'objectif est de voir si la taille et les caractéristiques financières des EPCI sont associées aux niveaux obtenus en CAE et ECI.

## Données

Le projet croise deux sources principales.

### Données TETE

La base TETE contient notamment :

- les niveaux CAE
- les niveaux ECI
- les informations d'identification des collectivités

### Données BANATIC

Les données BANATIC apportent des informations administratives, démographiques et financières sur les intercommunalités françaises :

- population
- nature juridique
- revenus
- potentiel fiscal
- potentiel fiscal par habitant
- coefficient d'intégration fiscale (CIF)

Les deux bases sont principalement reliées grâce aux identifiants SIREN.

Après nettoyage et appariement, la base finale contient 425 EPCI.

## Méthodologie

Le projet est organisé en trois notebooks.

### 1. Préparation des données

`notebooks/01_data_cleaning.ipynb`

Cette première partie comprend l'importation des données TETE et BANATIC, leur nettoyage, la sélection des variables utiles et l'appariement des EPCI grâce aux identifiants SIREN.

Les doublons et les valeurs manquantes sont également contrôlés avant l'export de la base finale.

### 2. Analyse exploratoire

`notebooks/02_exploratory_analysis.ipynb`

Cette partie permet d'explorer :

- la distribution des niveaux CAE et ECI
- la population selon les niveaux CAE
- le potentiel fiscal par habitant
- les relations entre population, revenus et potentiel fiscal
- les différences démographiques et financières entre les EPCI

Une différence importante apparaît notamment pour la population. La population médiane passe d'environ 23 500 habitants pour les EPCI sans étoile CAE à plus de 500 000 habitants pour ceux ayant cinq étoiles.

Les différences sont moins marquées pour ECI.

### 3. Analyse statistique

`notebooks/03_statistical_analysis.ipynb`

L'analyse statistique comprend :

- test de Kruskal-Wallis
- corrélation de Spearman
- tests de Mann-Whitney avec correction de Holm
- analyse des facteurs d'inflation de variance (VIF)
- régression logistique ordinale pour CAE
- régression logistique binaire pour ECI

## Principaux résultats

### CAE

La population est positivement associée au niveau CAE.

La corrélation de Spearman entre la population et le niveau CAE est d'environ `0,53`.

Dans le modèle ordinal, la population, le potentiel fiscal par habitant et le CIF sont tous positivement et significativement associés aux niveaux CAE.

Toutes choses égales par ailleurs :

- une population supérieure de 10 % est associée à environ 10 % de chances relatives supplémentaires d'appartenir à une catégorie CAE plus élevée
- une population supérieure de 50 % est associée à environ 51 % de chances relatives supplémentaires
- 100 € supplémentaires de potentiel fiscal par habitant sont associés à environ 32 % de chances relatives supplémentaires
- une augmentation de 0,1 du CIF est associée à environ 28 % de chances relatives supplémentaires

### ECI

Les niveaux ECI sont beaucoup plus concentrés à zéro et les catégories supérieures contiennent peu d'observations.

L'analyse distingue donc :

- 316 EPCI sans étoile ECI
- 109 EPCI avec au moins une étoile ECI

Dans le modèle logistique, la population reste positivement et significativement associée à la présence d'au moins une étoile ECI.

En revanche, le potentiel fiscal par habitant et le CIF ne sont plus statistiquement significatifs lorsque les variables sont étudiées ensemble.

## Interprétation

Dans l'ensemble, les EPCI les plus peuplés ont tendance à avoir des niveaux d'engagement TETE plus élevés, surtout pour CAE.

Les caractéristiques financières étudiées sont également associées aux niveaux CAE. Pour ECI, les résultats sont moins nets.

Ces résultats restent exploratoires et ne permettent pas de conclure à une relation de causalité.

D'autres éléments qui ne sont pas présents dans les données peuvent aussi jouer un rôle, par exemple les moyens humains, les capacités d'ingénierie, l'organisation administrative, les priorités politiques ou l'ancienneté des politiques environnementales.

## Structure du projet

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

## Outils utilisés

Le projet a été réalisé en Python avec :

- `pandas` pour la préparation et la manipulation des données
- `numpy` pour le calcul numérique
- `scipy` pour les tests statistiques
- `statsmodels` pour les modèles statistiques
- `Jupyter Notebook` pour réaliser et présenter les analyses

## Origine du projet

Ce projet a été développé personnellement à partir d'un travail d'analyse commencé pendant mon stage à l'ADEME Nouvelle-Aquitaine.

L'objectif était de poursuivre ce travail en construisant un projet Python complet et reproductible, depuis les données brutes jusqu'à l'analyse statistique.


# 🇬🇧 English version

## Overview

This project follows an initial analysis carried out during my internship at ADEME Nouvelle-Aquitaine.

The aim is to study the relationship between several characteristics of French intermunicipal authorities (EPCIs) and their level of engagement in the Territoire Engagé Transition Écologique (TETE) programme.

The analysis was carried out in Python, from data preparation and matching to statistical testing and modelling.

The results show statistical associations and should not be interpreted as causal relationships.

## Context

Territoire Engagé Transition Écologique (TETE) is an ADEME programme that supports French local authorities in their ecological transition policies.

It includes two main frameworks:

- `CAE`: Climate-Air-Energy (Climat-Air-Énergie)
- `ECI`: Circular Economy (Économie Circulaire)

Local authorities can achieve different recognition levels depending on their progress within these frameworks.

This project focuses on EPCIs, French public intermunicipal authorities grouping several municipalities.

## Research question

The main question is:

> Are the demographic and financial characteristics of EPCIs associated with their level of engagement in the TETE programme?

Three variables are studied more specifically:

- population
- fiscal potential per capita
- coefficient of fiscal integration (CIF)

The aim is to see whether the size and financial characteristics of EPCIs are associated with their CAE and ECI ratings.

## Data

The project combines two main data sources.

### TETE data

The TETE dataset contains:

- CAE ratings
- ECI ratings
- information used to identify each local authority

### BANATIC data

BANATIC provides administrative, demographic and financial information on French intermunicipal authorities, including:

- population
- legal status
- income
- fiscal potential
- fiscal potential per capita
- coefficient of fiscal integration (CIF)

The two datasets are mainly matched using SIREN identifiers.

After cleaning and matching, the final dataset contains 425 EPCIs.

## Methodology

The project is organised into three notebooks.

### 1. Data preparation

`notebooks/01_data_cleaning.ipynb`

This notebook covers the import and cleaning of the TETE and BANATIC datasets, variable selection and SIREN-based matching.

Duplicates and missing values are also checked before exporting the final dataset.

### 2. Exploratory data analysis

`notebooks/02_exploratory_analysis.ipynb`

This part explores:

- CAE and ECI rating distributions
- population across CAE ratings
- fiscal potential per capita
- relationships between population, income and fiscal potential
- demographic and financial differences between EPCIs

A clear difference appears for population. Median population increases from approximately 23,500 inhabitants among EPCIs with no CAE stars to more than 500,000 among those with five stars.

The differences are less pronounced for ECI.

### 3. Statistical analysis

`notebooks/03_statistical_analysis.ipynb`

The statistical analysis includes:

- Kruskal-Wallis tests
- Spearman rank correlation
- Mann-Whitney tests with Holm correction
- variance inflation factors (VIF)
- ordinal logistic regression for CAE
- binary logistic regression for ECI

## Main findings

### CAE

Population is positively associated with CAE ratings.

The Spearman correlation between population and CAE rating is approximately `0.53`.

In the ordinal model, population, fiscal potential per capita and CIF are all positively and statistically significantly associated with higher CAE ratings.

Holding the other variables constant:

- a 10% larger population is associated with approximately 10% higher odds of belonging to a higher CAE category
- a 50% larger population is associated with approximately 51% higher odds
- an additional €100 of fiscal potential per capita is associated with approximately 32% higher odds
- a 0.1 increase in CIF is associated with approximately 28% higher odds

### ECI

ECI ratings are much more concentrated at zero and there are few observations in the higher categories.

The analysis therefore distinguishes between:

- 316 EPCIs with no ECI star
- 109 EPCIs with at least one ECI star

In the logistic model, population remains positively and statistically significantly associated with having at least one ECI star.

Fiscal potential per capita and CIF are not statistically significant when the variables are considered together.

## Interpretation

Overall, more populated EPCIs tend to have higher levels of TETE engagement, especially for CAE.

The financial characteristics studied are also associated with CAE ratings, while the results for ECI are less clear.

These results are exploratory and cannot be interpreted as causal effects.

Other factors that are not included in the data may also play a role, such as staffing, administrative and engineering capacity, political priorities or previous environmental policies.

## Project structure

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

## Tools

The project was developed in Python using:

- `pandas` for data preparation and manipulation
- `numpy` for numerical computing
- `scipy` for statistical tests
- `statsmodels` for statistical modelling
- `Jupyter Notebook` for developing and presenting the analysis

## Project background

This project was developed independently from an initial analysis started during my internship at ADEME Nouvelle-Aquitaine.

The aim was to continue this work by building a complete and reproducible Python project, from raw data preparation to statistical analysis.
