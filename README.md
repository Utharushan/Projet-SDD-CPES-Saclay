# Projet-SDD-CPES-Saclay

## Résumé

Ce dépôt contient le projet de Sciences des Données mené par Rémi Malapert, Othmane Nammous et Tharushan Uthayakumar, encadré par Monsieur Antonio Ocello (post-doctorant au CMAP, École Polytechnique). L’objectif est de modéliser et prédire la dépense calorique lors de séances de sport à partir du [Gym Members Exercice Dataset](https://www.kaggle.com/datasets/valakhorasani/gym-members-exercise-dataset) (973 observations) de Kaggle. Après un nettoyage et une standardisation des variables continues, nous avons comparé plusieurs modèles de régression linéaire (complet, réduit, régularisé), évalué leur performance (MSE, MAE, R², AIC/BIC) et validé leur robustesse via des diagnostics résiduels et validation croisée 10-fold. Le modèle final, composé de quatres prédicteurs clés (Age, Height, Avg\_BPM, Fat\_Percentage), explique près de 50 % de la variance calorique avec une très bonne parcimonie.

---

## Structure du dépôt

```
README.md
gym_members_exercise_tracking.csv   # Jeu de données brut
main.tex                            # Source LaTeX du rapport complet
Rapport_Projet_SDD_…Tharushan.pdf   # Version PDF du rapport
*.png                               # Figures exportées (corrélation, distributions, diagnostics…)
```

* **gym\_members\_exercise\_tracking.csv**
  Données brutes extraites de Kaggle (973 sessions, variables continues et catégorielles).

* **main.tex** et **Rapport\_Projet\_SDD…Tharushan.pdf**
  Source LaTeX et document final PDF du rapport. Contient sections : Introduction, Méthodologie, Résultats, Diagnostics, Conclusion.

* **Figures**

  * `distribution.png`, `boxplot.png` : distributions et outliers
  * `correlation.png` : matrice de corrélation
  * `qqplot.png` : QQ-plot résidus
  * `cook.png`, `cooks_d.png` : diagnostics de Cook
  * `prediction.png` : comparaison prédictions vs réel
  * `information_criterion.png` : AIC/BIC comparatif

---

## Prérequis

* **Python 3.8+**
* Bibliothèques Python :

  ```bash
  pip install pandas numpy seaborn matplotlib statsmodels scikit-learn scipy
  ```
* **LaTeX** (TeX Live ou MikTeX) pour compiler `main.tex`.

---

## Usage

1. **Explorer et prétraiter les données**

   ```python
   import pandas as pd
   df = pd.read_csv("gym_members_exercise_tracking.csv")
   # suppression colonnes catégorielles, imputation, standardisation…
   ```

2. **Ajuster les modèles de régression** (extrait)

   ```python
   import statsmodels.api as sm
   X = sm.add_constant(df_scaled.drop("Calories_Burned", axis=1))
   y = df_scaled["Calories_Burned"]
   modele_full = sm.OLS(y, X).fit()
   ```

3. **Sélection de variables**

   * Backward elimination
   * Critères AIC/BIC

4. **Diagnostics et validation**

   * Résidus (Omnibus, Jarque–Bera, Durbin–Watson)
   * Leverage et distance de Cook
   * Validation croisée 10-fold

5. **Compilation du rapport**

   ```bash
   pdflatex main.tex
   ```

---

## Résultats clés

* **Modèle complet** : R² ≃ 0,50
* **Modèle réduit (Age, Height, Avg\_BPM, Fat\_Percentage)** : R² ≃ 0,497, AIC ↓, BIC ↓
* **Diagnostics** : résidus normalement distribués, absence de points influents, VIF < 2
* **Validation croisée 10-fold** : MSE et MAE stables entre splits

---

## Auteurs et contact

* **Rémi Malapert** : remi.malapert@hec.edu
* **Othmane Nammous** : othmane.nammous@hec.edu
* **Tharushan Uthayakumar** : tharushan.uthayakumar@hec.edu 
