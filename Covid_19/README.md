# Machine Learning Project : Covid-19

Un modèle pour prédire si un patient est malade ou non.


Exploratory Data Analysis
---

Objectif: comprendre au maximum les données dont on dispose pour définir une stratégie de modélisation.

Checklist de base (non exhaustive):

1. Analyse de la forme:

    - Identification de la target : SARS-Cov-2 exam result
    - Nombre de lignes et de colonne : (5644, 111)
    - Types de variables (qualitatives, discrètes, continues) => (df.dtypes) = qualitatives = 70, quantitatives = 41
    - Identification des valeurs manquantes :
        - beaucoup de NaN (moitié des variables > 90% de NaN)
        - 2 groupes de données: 76% => Test viral, 89% => Taux sanguins

2. Analyse du fond:

- Visualisation de la target (histogramme / boxplot) : 10% de cas positifs (558 / 5000)

- Compréhension des différentes variables (internet) :
    - variables continues standardisées, skewed (asymétriques), test sanguin
    - age quantile: difficile d'interpréter le graphique de cette variable.
    - variables qualitatives : binaire (0, 1), viral, Rhinovirus qui semble très élévé

- Visualisation des relations features-target (histogramme / boxplot)
    - target / blood : les taux Monocytes, Platelets, Leukocytes semblent liés au covid-19 => hypothèse à tester
    - target / age : les individus de faible age sont très peu contaminés? attention: on ne connait pas l'age et on ne sait pas de quand date le dataset. En revanche, cette variable pourra etre intéressante pour la comparer avec les résultats de tests sanguins.
    - target / viral : les doubles maladies sont très rares. Rhinovirus / Enterovirus positif - covid 19 négatif? (hypothèse à tester)
    - blood_data / blood_data : certaines variables sont très correlées: +0.9 (à surveiller plus tard)
    - blood_data / age : très faible correlation entre age et taux sanguin
    - viral / viral : Influenza rapid test donne de mauvais résultat. Il faudra peut etre la laisser tomber.
    - relation maladie / blood_data : les taux sanguins entre malades et covid-19 sont différents
    - relation hospitalisation / est malade :
    - relation hospitalisation / blood : intéressant dans le cas où on pourra prédire dans quel service un patient devrait aller.

- NaN analyse : viral : 1350 (92/8), blood : 600(87/13), both : 90

- Identification des outliers

- Hypothèse nulles (Ho):
    - Les individus atteints du covid-19 ont des taux de Leukocytes, Monocytes, Platelets significativement différents
        H0 = Les taux moyens sont égaux chez les individus positifs et négatifs ==> Rejetée
    - Les individus atteints d'une quelconque maladie ont des taux significativement différents


Pre-processing & Modelling
---

Objectifs : 

1. Mettre les données dans un format propice au ML
    - Train / Test
    - Encodage
    - Nettoyage des NaN
    
2. Améliorer la performance du modèle
    - Feature Selection
    - Feature Engineering
    - Feature Scaling
    - Suppression des Outliers