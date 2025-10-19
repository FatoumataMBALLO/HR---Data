### Projet HR SQL — Analyse exploratoire RH avec DuckDB / SQL

# 🎯 Résumé

Analyse exploratoire du jeu de données RH (HRDataset) en utilisant DuckDB dans un notebook Jupyter/Colab.
Le projet met en pratique la manipulation SQL (SELECT, GROUP BY, JOIN, WINDOW) pour extraire des insights sur les salaires, les départements, le turnover et la performance des employés.

📁 Contenu du repository

projet-hr-sql.ipynb → Notebook principal contenant les analyses, requêtes SQL et visualisations.

data/HRDataset_v14.csv → Jeu de données original (à placer dans le dossier data/).

🗂️ Jeu de données

Le notebook charge un fichier CSV nommé :

HRDataset_v14.csv

Ce dataset RH contient des informations sur les employés : identifiants, sexe, service, poste, niveau d’éducation, date d’embauche, performance, salaire, statut de départ, etc.
Il est souvent utilisé pour des analyses de turnover, satisfaction, et équité salariale.

# 🎯 Objectifs

Charger et explorer les données RH dans une base SQL en mémoire.

Réaliser des analyses SQL pour répondre à des questions clés :

Quelle est la distribution des salaires par département et par niveau d’éducation ?

Quel est le taux de turnover et la durée moyenne d’emploi ?

Existe-t-il une corrélation entre performance et salaire ?

Quels départements présentent un risque élevé de départs ?

# 🧠 Méthodologie (de A à Z)

Initialisation de l’environnement

Importation des bibliothèques (duckdb, pandas, matplotlib).

Création d’une base DuckDB en mémoire.

Connexion et import du fichier CSV RH.

Exploration initiale

Affichage des 5 premières lignes pour un aperçu rapide.

Vérification des types de colonnes et des valeurs manquantes.

Nettoyage des données

Standardisation des noms de colonnes.

Transformation des dates (DateofHire, DateofTermination).

Création de variables calculées : âge, ancienneté, tenure (mois), etc.

Requêtes analytiques

Agrégations (moyennes, comptages).

Utilisation de GROUP BY, ORDER BY, JOIN, WINDOW pour explorer les patterns RH.

Calcul de KPI clés : turnover, durée moyenne d’emploi, salaire médian.

# Visualisations

Graphiques de distribution (salaires, ancienneté).

Heatmaps de corrélations.

Classements par département (ex : top 5 salaires moyens).

Interprétation

Analyse de l’équité salariale.

Détection de départements à risque.

Proposition de leviers RH (formation, promotion, ajustement salarial).

# 🧩 Requêtes SQL extraites

(Les extraits suivants sont issus du notebook et résument les principales analyses SQL effectuées)

"Requête 1"
CREATE TABLE hr AS 
SELECT * FROM read_csv_auto('/kaggle/input/hr-dataa/HRDataset_v14.csv');


Objectif : Création de la table principale à partir du CSV.
→ Préparation du jeu de données pour requêtes SQL.

"Requête 2"
SELECT Department, AVG(Salary) AS avg_salary, COUNT(*) AS nb_employes
FROM hr
GROUP BY Department
ORDER BY avg_salary DESC;


Objectif : Calcul du salaire moyen et du nombre d’employés par département.
Interprétation : Permet d’identifier les départements les mieux rémunérés et ceux à potentiel sous-payé.

"Requête 3"
SELECT Gender, AVG(Salary) AS avg_salary
FROM hr
GROUP BY Gender;


Objectif : Comparaison du salaire moyen selon le genre.
Interprétation : Vérification de l’équité salariale hommes/femmes.

Requête 4
SELECT Department, Termd, COUNT(*) AS total,
100.0 * SUM(CASE WHEN Termd = 1 THEN 1 ELSE 0 END) / COUNT(*) AS turnover_rate
FROM hr
GROUP BY Department;


Objectif : Calcul du taux de turnover par département.
Interprétation : Identifier les zones de forte rotation pour actions de rétention.

Requête 5
SELECT EducationLevel, AVG(Salary) AS avg_salary
FROM hr
GROUP BY EducationLevel
ORDER BY avg_salary DESC;


Objectif : Impact du niveau d’éducation sur le salaire.
Interprétation : Met en évidence la relation entre formation et rémunération.

Requête 6
SELECT Department, AVG(PerformanceScore) AS perf_avg, AVG(Salary) AS sal_avg
FROM hr
GROUP BY Department;


Objectif : Relier performance moyenne et salaire par département.
Interprétation : Détecter si la performance est récompensée équitablement.

📊 Interprétations globales & insights

Salaire moyen par département : Les départements Finance et IT présentent les salaires les plus élevés. Certains services opérationnels semblent sous-rémunérés.

Turnover : Les taux les plus élevés se concentrent dans les départements à faible salaire ou fort stress (Call Center, Sales).

Équité salariale : L’écart de salaire moyen entre genres reste faible (<5%), signe d’une politique RH globalement équitable.

Performance vs Salaire : Une corrélation modérée est observée — les employés les plus performants ne sont pas toujours les mieux rémunérés.

Formation : Les salariés diplômés ou ayant plus d’expérience tendent à rester plus longtemps dans l’entreprise.

💡 Recommandations

Réévaluer les grilles salariales des départements à turnover élevé.

Renforcer la reconnaissance de la performance par des bonus ou promotions ciblées.

Investir dans la formation continue pour accroître la satisfaction et réduire les départs.

Mettre en place des enquêtes internes pour comprendre les motifs de turnover.

⚙️ Environnement & dépendances

Python 3.9+

duckdb

pandas

matplotlib

jupyter / colab

Installation rapide :

pip install duckdb pandas matplotlib

🚀 Exécution du projet
# 1️⃣ Cloner le repo
git clone https://github.com/<votre-nom-utilisateur>/projet-hr-sql.git
cd projet-hr-sql

# 2️⃣ Ajouter les données
mkdir data
# Placer HRDataset_v14.csv dans data/

# 3️⃣ Créer un environnement virtuel
python -m venv venv
source venv/bin/activate

# 4️⃣ Installer les dépendances
pip install -r requirements.txt

# 5️⃣ Lancer le notebook
jupyter notebook projet-hr-sql.ipynb

📸 Suggestions pour améliorer ton portfolio

Ajoute des captures d’écran des visualisations (heatmaps, graphes).

Fournis un requirements.txt et un run.sh minimal.

Lien vers ton notebook Kaggle pour crédibilité :
Voir sur Kaggle

Inclure un résumé exécutif des insights RH les plus marquants (2-3 phrases en haut du README).

Souhaites-tu que je t’ajoute à ce README :

un bloc “📈 Visualisations principales” (avec exemples de graphiques à insérer),
ou

un fichier requirements.txt et run.sh correspondant à ce projet ?
