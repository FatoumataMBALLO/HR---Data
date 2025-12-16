# 📊 Tableau de bord RH – Analyse du Turnover et de la Rétention
### 🧠 Présentation du projet

Ce projet consiste en la conception d’un tableau de bord RH interactif sous Power BI, basé sur un jeu de données issu de Kaggle (HRDataset_v14.csv).
L’objectif est d’analyser les effectifs, le turnover, la rétention, la satisfaction, l’engagement et les rémunérations, afin d’apporter une aide à la décision pour les équipes RH.
Le projet adopte une approche end to end, depuis l’exploration des données en SQL jusqu’à la visualisation décisionnelle.
________________________________________

### 🎯 Objectifs analytiques

- Suivre les indicateurs RH clés (effectif, turnover, rétention) ;
- Identifier les profils à risque de départ
- Analyser l’impact de l’ancienneté, de l’âge, du poste et du département
- Étudier la satisfaction, l’engagement et leur lien avec le turnover
- Analyser les salaires et l’équité salariale
________________________________________

## 🗂️ Source des données
- Origine : Kaggle
- Dataset : HRDataset_v14.csv
- Périmètre : données RH anonymisées (effectifs, postes, salaires, dates, satisfaction, départs)
________________________________________

## 🛠️ Stack technique
- Kaggle : environnement de travail
- DuckDB : exploration, nettoyage et enrichissement des données (SQL)
- Power Query (Power BI) : transformations métier
- Power BI Desktop : modélisation, DAX et visualisation
________________________________________

## 🔹 1. Exploration et préparation des données (DuckDB)
- 📌 Chargement des données
Les données CSV sont chargées dans DuckDB afin de travailler efficacement en SQL, sans dépendance à un SGBD externe.
CREATE TABLE hr AS
SELECT *
FROM read_csv_auto('HRDataset_v14.csv');

- 📌 Analyse exploratoire (EDA)
•	Vérification des types de colonnes
•	Comptage des employés
•	Calcul d’indicateurs globaux :
  -	satisfaction moyenne
  - salaire moyen
  - nombre de départs
  - absentéisme
    
SELECT
COUNT(*) AS total_rows,
AVG(EmpSatisfaction) AS avg_satisfaction,
AVG(Salary) AS avg_salary,
SUM(CASE WHEN DateofTermination IS NOT NULL THEN 1 ELSE 0 END) AS total_left
FROM hr;

- 📌 Nettoyage et enrichissement
•	Normalisation des noms et types
•	Conversion des dates
•	Création de l’ancienneté en années :
ROUND(
datediff('day', DateofHire, COALESCE(DateofTermination, CURRENT_DATE)) / 365.25,
2
) AS Years_at_Company

  
- 📌 Export
La table finale est exportée en CSV et devient la source unique pour Power BI.
________________________________________
## 🔹 2. Transformations métier (Power Query – Power BI)
-	Conversion et typage des colonnes
-	Correction des dates de naissance incohérentes
-	Calcul de l’âge réel
-	Création de variables analytiques : 
	- tranches d’âge
    - classes d’ancienneté
     - indicateurs TURNOVER / RÉTENTION

-	Harmonisation des libellés (genre, postes, départements)
👉 Objectif : garantir des calculs DAX fiables et une lecture métier claire.
________________________________________

## 🔹 3. Modélisation et indicateurs RH (Power BI)
### 📊 KPI principaux
-	Effectif total
-	Turnover (%)
-	Rétention (%)
- Ancienneté moyenne
-	Âge moyen
-	Satisfaction (%)
-	Engagement (%)
-	Salaire moyen
### 📈 Axes d’analyse
-	Vue d’ensemble RH
-	Engagement & satisfaction
-	Analyse des départs
-	Turnover vs rétention
-	Salaires et équité salariale
### 🧭 Filtres interactifs
-	Année
-	Département
-	Poste
-	Genre
-	Tranche d’âge
-	Motif de départ
________________________________________

## 📌 Résultats clés (exemple)
-	Effectif total : 311 employés
-	Turnover : 33,44 %
-	Rétention : 66,56 %
-	Satisfaction moyenne : 61,74 %
-	Engagement moyen : 66 %

Les départs sont plus concentrés sur certaines tranches d’âge, niveaux d’ancienneté et départements, mettant en évidence des zones à risque RH.
________________________________________

## 🚀 Valeur ajoutée du projet
-	Utilisation de SQL analytique avancé
-	Exploitation de DuckDB pour un workflow moderne
-	Séparation claire entre :
    -	préparation technique
  	- logique métier
    -	visualisation décisionnelle
-	Approche orientée décision RH
________________________________________

## 🏁 Conclusion
Ce projet illustre une approche complète de l’analyse de données RH, depuis l’exploration et le nettoyage en SQL jusqu’à la création d’un tableau de bord Power BI orienté décision. Il met particulièrement l’accent sur les problématiques de turnover, de fidélisation et de rémunération des collaborateurs.

📊 Un projet idéal pour démontrer des compétences en Data Analytics, BI et analyse RH.

## 🎥 Démonstration du rapport

Une courte vidéo présente la navigation, les filtres interactifs et les principaux axes d’analyse du tableau de bord RH.

👉 [Voir la vidéo de démonstration du rapport Power BI] :

https://drive.google.com/file/d/1PjExT15yWSn8nZs6dsVz2yTGGnHSdvQS/view?usp=sharing

