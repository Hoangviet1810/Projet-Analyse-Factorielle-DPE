# Projet-Analyse-Factorielle-DPE

# Analyse de la consommation énergétique et des émissions de GES des logements

## Table des Matières

- [1. Introduction](#1-introduction)
- [2. Structure des données](#2-structure-des-données)
- [3. Analyses réalisées](#3-analyses-réalisées)
  - [3.1 Statistiques descriptives](#31-statistiques-descriptives)
  - [3.2 Visualisations](#32-visualisations)
  - [3.3 Corrélations](#33-corrélations)
  - [3.4 Tests statistiques](#34-tests-statistiques)
- [4. Interprétation des résultats](#4-interprétation-des-résultats)
- [5. Outils utilisés](#5-outils-utilisés)
- [6. Instructions pour reproduire](#6-instructions-pour-reproduire)
  
## 1. Introduction

L’étude porte sur la performance énergétique de **1000 logements individuels** construits entre **1900 et 2020** dans le département de la **Haute-Garonne**, pour lesquels un **DPE** a été réalisé avant **juillet 2021**.

Ce projet consiste à analyser un jeu de données contenant des informations sur les logements :  
- **type de logement** (appartement, maison)  
- **type d’énergie de chauffage** (gaz, électricité, autre)  
- **classe de consommation énergétique** (A à G)  
- **surface habitable, année de construction, consommation d’énergie, émissions de GES**

L'objectif est de :  
- Comprendre les relations entre variables quantitatives et qualitatives  
- Identifier les corrélations entre consommation d’énergie et émissions de GES  
- Visualiser les profils de logements et l’impact du type de chauffage  
- Réaliser des tests statistiques (Chi-deux, ANOVA, t-tests)

Deux versions de codes accompagnent ce projet :  
- un fichier **Python** dédié à la visualisation des données (*plots*)  
- un fichier **R** utilisé pour la réalisation des **tests statistiques**

---
## 2. Installation

1. Clone this repository to your local machine:
    ```sh
   git clone https://github.com/Hoangviet1810/Projet-Analyse-Factorielle-DPE.git
    ```

2.Accédez au dossier du projet ::
    ```sh
    cd Projet-Analyse-Factorielle-DPE
    ```
---

## 3. Structure des données
| Variable                  | Type      | Description                                   |
|----------------------------|-----------|-----------------------------------------------|
| type_logement              | Catégorie | Appartement ou Maison                        |
| type_energie_chauffage     | Catégorie | Gaz, Électricité, Autre                       |
| classe_conso_energie       | Catégorie | Classe énergétique (A, B, C, …, G)           |
| annee_construction         | Numérique | Année de construction du logement            |
| surface_habitable          | Numérique | Surface habitable en m²                       |
| conso_energie              | Numérique | Consommation énergétique (kWh/m²/an)        |
| emission_ges               | Numérique | Émissions de gaz à effet de serre (kg CO2/m²)|

---

## 4. Analyses réalisées

### 4.1 Statistiques descriptives
- Calcul de la moyenne, médiane, variance et coefficient de variation pour les variables numériques.  
- Résumé des variables catégorielles et distribution par barplot.  

### 4.2 Visualisations
- Histogrammes et boxplots pour **conso_energie** et **emission_ges**  
- Barplots pour **type_logement**, **type_energie_chauffage**, **classe_conso_energie**  
- Cercle de corrélation pour les variables quantitatives (*annee_construction, surface_habitable, conso_energie, emission_ges*)  
- MCA (Analyse des Correspondances Multiples) pour les variables qualitatives  

### 4.3 Corrélations
- Corrélation positive : *conso_energie* et *emission_ges*  
- Corrélation négative : *annee_construction* vs consommation et émissions  
- Indépendance : *surface_habitable* peu corrélée avec consommation et année de construction  

### 4.4 Tests statistiques
1. **Chi-deux** : Dépendance entre *classe_conso_energie* et *type_energie_chauffage*  
   - p-value < 0.05 → H0 rejetée → relation significative  
2. **ANOVA** : Différence de *conso_energie* entre types de logement  
   - p-value < 0.05 → H0 rejetée → consommation différente selon type de logement  
3. **ANOVA / Welch** : Différence de *emission_ges* selon type de chauffage  
4. **Tests t de Student par paires** : Comparaisons des moyennes d’émissions entre groupes de chauffage  

---

## 5. Interprétation des résultats
- Les appartements sont généralement plus économes que les maisons individuelles.  
- Les logements chauffés à l’électricité tendent à avoir de meilleures performances énergétiques (classe B, C).  
- Les logements chauffés au gaz ont tendance à consommer plus et à émettre davantage de GES.  
- Le MCA montre clairement les profils des logements et leur association avec les classes énergétiques et les types de chauffage.  

---

## 6. Logiciels utilisés
- **Python** (pour des visualisations) : (**Pandas**, **NumPy**,**Matplotlib**, **Seaborn**, **Prince**)
- **R** (pour des tests) : `FactoMineR`, `factoextra`
- Visualisations : histogrammes, boxplots, barplots, cercle de corrélation, MCA plots  

---

## 6. Instructions pour reproduire
1. Cloner le repository  
2. Installer les dépendances :  
```bash
pip install pandas numpy matplotlib seaborn prince
