#  Student Exam Score Prediction  
Prédiction des performances académiques des étudiants à partir de données comportementales, académiques et environnementales.

---

##  Contexte du projet

Ce projet, réalisé dans le cadre du module **Apprentissage Automatique**, a pour objectif de prédire la note finale `exam_score` (comprise entre 0 et 100) obtenue par un étudiant.  
Le dataset utilisé est particulièrement volumineux :

- **630 000** observations pour l’entraînement  
- **270 000** observations pour le test  
- **12 variables explicatives** (numériques et catégorielles)

L’enjeu principal est d’identifier le modèle de régression offrant la meilleure précision prédictive.

---

## Structure du dépôt

- **notebook.ipynb** : analyse exploratoire, prétraitement, entraînement des modèles  
- **rapport.pdf** : rapport complet du projet  
- **submission.csv** : prédictions finales  
- **README.md** : documentation du projet  

---

##  Prétraitement des données

Le prétraitement a comporté plusieurs étapes essentielles :

###  Encodage des variables
- **Encodage ordinal** pour : `sleep_quality`, `facility_rating`, `exam_difficulty`  
- **One‑Hot Encoding** pour : `gender`, `course`, `study_method`, `internet_access`

### Standardisation
Les variables numériques (`study_hours`, `class_attendance`, `sleep_hours`, `age`) ont été normalisées afin d’harmoniser les échelles.

###  Nettoyage
- Suppression des variables à variance nulle  
- Vérification de l’absence de valeurs infinies  
- Alignement strict des colonnes entre train et test  

---

##  Analyse exploratoire (EDA)

L’analyse exploratoire a permis d’identifier plusieurs tendances :

- **Corrélation forte** entre le temps d’étude (`study_hours`) et le score d’examen (r = 0.76)  
- **Corrélation modérée** pour l’assiduité (`class_attendance`)  
- Impact faible pour `sleep_hours` et `age`  
- Répartition équilibrée des catégories  
- Aucune valeur manquante dans le dataset  

Des visualisations (histogrammes, boxplots, heatmaps, hexbin plots) ont permis de confirmer ces observations.

---

##  Modèles testés

Plusieurs modèles de régression ont été entraînés et comparés selon la métrique **RMSE** (Root Mean Square Error).

###  Résultats comparatifs

| Modèle              | RMSE   |
|----------------------|--------|
| Linear Regression    | 8.877  |
| Ridge Regression     | 8.872  |
| Random Forest        | 8.992  |
| Stacking             | 8.811  |
| XGBoost              | 8.741  |
| CatBoost             | 8.736  |
| **Gradient Boosting** | **8.716** |

Le modèle **Gradient Boosting** obtient la meilleure performance.

---

## Modèle final retenu

Le modèle final choisi est **GradientBoostingRegressor**, car il présente le RMSE le plus faible parmi tous les modèles testés.

###  Hyperparamètres retenus
- 600 arbres  
- learning rate de 0.5  
- profondeur maximale de 3  
- sous‑échantillonnage de 0.8  

###  Performance finale
- **RMSE = 8.716**  
Ce score constitue la meilleure performance obtenue dans le projet.

---

##  Soumission finale

Les prédictions finales ont été générées sur l’ensemble de test et bornées entre 0 et 100 afin de respecter l’intervalle réel des scores.  
Le fichier `submission.csv` contient :

- l’identifiant de chaque étudiant  
- le score prédit par le modèle final  

---
