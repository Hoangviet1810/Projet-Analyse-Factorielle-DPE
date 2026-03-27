# Projet-Analyse-Factorielle-DPE

# Analyse de la consommation énergétique et des émissions de GES des logements

## Table des Matières

- [1. Introduction](#1-introduction)
- [2. Installation](#2-installation)
- [3. Logiciels utilisés](#3-logiciels-utilisés)
- [4. Structure des données](#4-structure-des-données)
- [5. Analyses réalisées](#5-analyses-réalisées)
  - [5.1 Statistiques descriptives](#51-statistiques-descriptives)
  - [5.2 Visualisations](#52-visualisations)
  - [5.3 Corrélations](#53-corrélations)
  - [5.4 Tests statistiques](#54-tests-statistiques)
- [6. Interprétation des résultats](#6-interprétation-des-résultats)
- [7. Résultats des tests statistiques](#7-résultats-des-tests-statistiques)
  - [7.1 Test ANOVA](#71-test-anova)
  - [7.2 Tests t de Student par paires](#72-tests-t-de-student-par-paires)
- [8. Visualisations finales](#8-visualisations)
  
## 1. Introduction

L’étude porte sur la performance énergétique de **1000 logements individuels** construits entre **1900 et 2020** dans le département de la **Haute-Garonne**, pour lesquels un **DPE** a été réalisé avant **juillet 2021**. Pour plus de détails, vous pouvez consulter le [fichier PDF](Projet_DPE.pdf).

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
2. Accédez au dossier du projet:
    ```sh
   cd Projet-Analyse-Factorielle-DPE
    ```
---

## 3. Logiciels utilisés
- **Python** (pour des visualisations) : (**Pandas**, **NumPy**,**Matplotlib**, **Seaborn**, **Prince**)
- **R** (pour des tests) : `FactoMineR`, `factoextra`
- Visualisations : histogrammes, boxplots, barplots, cercle de corrélation, MCA plots

---
## 4. Structure des données
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

## 5. Analyses réalisées

### 5.1 Statistiques descriptives
- Calcul de la moyenne, médiane, variance et coefficient de variation pour les variables numériques.  
- Résumé des variables catégorielles et distribution par barplot.  

### 5.2 Visualisations
- Histogrammes et boxplots pour **conso_energie** et **emission_ges**  
- Barplots pour **type_logement**, **type_energie_chauffage**, **classe_conso_energie**  
- Cercle de corrélation pour les variables quantitatives (*annee_construction, surface_habitable, conso_energie, emission_ges*)  
- MCA (Analyse des Correspondances Multiples) pour les variables qualitatives  

### 5.3 Corrélations
- Corrélation positive : *conso_energie* et *emission_ges*  
- Corrélation négative : *annee_construction* vs consommation et émissions  
- Indépendance : *surface_habitable* peu corrélée avec consommation et année de construction  

### 5.4 Tests statistiques
1. **Chi-deux** : Dépendance entre *classe_conso_energie* et *type_energie_chauffage*  
   - p-value < 0.05 → H0 rejetée → relation significative  
2. **ANOVA** : Différence de *conso_energie* entre types de logement  
   - p-value < 0.05 → H0 rejetée → consommation différente selon type de logement  
3. **ANOVA / Welch** : Différence de *emission_ges* selon type de chauffage  
4. **Tests t de Student par paires** : Comparaisons des moyennes d’émissions entre groupes de chauffage  

---

## 6. Interprétation des résultats
- Les appartements sont généralement plus économes que les maisons individuelles.  
- Les logements chauffés à l’électricité tendent à avoir de meilleures performances énergétiques (classe B, C).  
- Les logements chauffés au gaz ont tendance à consommer plus et à émettre davantage de GES.  
- Le MCA montre clairement les profils des logements et leur association avec les classes énergétiques et les types de chauffage.  

---

## 7. Résultats des tests statistiques

### 7.1 Test ANOVA

| Test | Hypothèse nulle (H0) | Hypothèse alternative (H1) | Statistique | p-value | Conclusion | Moyenne(s) |
|------|---------------------|----------------------------|------------|---------|-----------|------------|
| Conso énergie vs type_logement | Pas de différence de consommation moyenne entre Maison et Appartement | Différence réelle de consommation moyenne entre Maison et Appartement | F = 11.1 | 0.000894 | H0 rejetée → différence significative | Maison: 197.63 kWh/m²/an<br>Appartement: 176.48 kWh/m²/an |
| Émissions GES vs type_energie_chauffage (ANOVA Welch) | Moyennes d’émissions égales | Au moins un groupe a une moyenne différente | F = 219.53 | < 2.2e-16 | Différences significatives → émissions dépendent du type d’énergie | Gaz: 33.6<br>Électricité: 11.1<br>Autre: 55.5 |

---

### 7.2 Tests t de Student par paires

| Comparaison | p-value | Conclusion |
|------------|---------|------------|
| Gaz vs Électricité | < 2e-16 | Différence extrêmement significative |
| Gaz vs Autre | 0.0053 | Différence significative |
| Électricité vs Autre | 1.8e-06 | Différence extrêmement significative |

**Observations clés :**  
- Les maisons consomment plus que les appartements, ce qui explique leur projection vers des classes énergétiques moins performantes (D, E, F).  
- Les émissions de GES dépendent fortement du type d’énergie de chauffage : l’électricité est la plus propre, le gaz intermédiaire, et “Autre” très polluant.  
- Tous les tests t montrent que toutes les paires de sources d’énergie diffèrent significativement au niveau des émissions.

---

##  8 Visualisations

Les visualisations finales sont créées pour l'analyse DPE et couvrent les aspects suivants :

1. **Distribution du type de logement :** Un graphique à barres montrant la fréquence des appartements et des maisons.  
2. **Classe énergétique par type de chauffage :** Un graphique à barres groupées illustrant la répartition des classes (A-G) selon l'énergie utilisée (gaz, électricité, autre).  
3. **Analyse des Correspondances Multiples (ACM) :** Une carte factorielle montrant les corrélations entre les variables catégorielles (type de logement, type de chauffage, classe énergétique).  
4. **Analyse en Composantes Principales (ACP) :** Un cercle de corrélation représentant les relations entre surface habitable, consommation d'énergie et émissions de GES.  
5. **Tests Statistiques et Émissions :** Tableaux (ANOVA, tests t) et boxplots analysant l'impact du type de chauffage sur les émissions de gaz à effet de serre.  

![assets/DPE-dashboard.png](assets/DPE-dashboard.png)
