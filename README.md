# Sell4All ( Exploration et nettoyage des données clients)

## 1. Besoin traité

Sell4All, une entreprise de vente en ligne de vêtements d'occasion, souhaite lancer une fonctionnalité de recommandation de produits basée sur l'IA. Avant d'entraîner un tel système, il faut d'abord vérifier que les données clients disponibles (`dataset-sell4all.csv`) sont fiables : complètes, cohérentes, sans doublons ni valeurs aberrantes. Ce projet réalise cet audit et livre un dataset nettoyé, prêt pour une future étape de Machine Learning.

## 2. Étapes suivies

**Jour 1  Exploration et audit**
- Installation de l'environnement (Miniconda, Jupyter, Pandas, Matplotlib).
- Chargement du CSV, aperçu des 5 premières lignes, résumé technique (`info()`, `describe()`).
- Audit de qualité sur 5 dimensions : complétude, validité, exactitude, cohérence, unicité.

**Jour 2 Analyse et visualisation**
- Calcul de la moyenne/médiane de `Age` et `Customer spendings`.
- Médiane d'âge par pays (question bonus).
- Détection des outliers par la méthode IQR.
- Comparaison sum / mean / median des dépenses par pays.
- Graphiques à barres (dépenses par pays, répartition par genre, distribution de l'âge).

**Jour 3  Nettoyage, validation et export**
- Correction du `Gender` (`Women` → `Woman`).
- Conversion des dates et heures en types appropriés (`datetime`, `time`).
- Suppression des clients ayant dépensé moins de 10 €.
- Suppression des doublons exacts.
- Sélection et tri des colonnes finales (`Country`, `Age`, `Gender`, `Customer spendings`).
- Export du CSV final et vérification du fichier généré.
- Rédaction du README.

## 3. Fonctionnalités développées

- Chargement et inspection automatique du dataset (structure, types, aperçu).
- Audit complet : valeurs manquantes, types, plages de valeurs, cohérence des catégories, doublons.
- Statistiques demandées par le brief (moyenne/médiane Age et Customer spendings, médiane d'âge par pays).
- Visualisations : dépenses par pays, distribution de l'âge, répartition par genre, boxplots.
- Nettoyage justifié (règle métier des 10 €, suppression des doublons, harmonisation du Gender) avec mesure de l'impact à chaque étape.
- Export du fichier CSV final, relu et vérifié après export.

## 4. Difficultés rencontrées et solutions

**Incohérence grammaticale dans Gender :** La colonne `Gender` contenait `Man` (singulier) et `Women` (pluriel). On a harmonisé en remplaçant `Women` par `Woman` pour garantir la cohérence entre les deux valeurs.

**Deux formats de date mélangés :** La colonne `Last date of connection` mélangeait deux formats différents (`5-Apr-21` et `oct. 10, 2021`). On a converti toute la colonne en `datetime` avec `pd.to_datetime(format='mixed')` pour unifier le format.

**Heure stockée en string :** La colonne `Last time of connection` était stockée en texte au lieu d'un type horaire. On l'a convertie en `time` avec `pd.to_datetime(format='%H:%M').dt.time`.

**Données synthétiques dans Phone, Address et Postal Code :** Les adresses sont de type Lorem Ipsum (`Risus Street`, `Enim Ave`), les numéros de téléphone sont fictifs avec deux formats mélangés, et certains codes postaux ne correspondent pas au format du pays (ex : France avec un code à 4 chiffres au lieu de 5). Ces colonnes sont hors du périmètre du livrable final, donc on a documenté l'anomalie sans la corriger.

**Absence de valeurs manquantes et d'outliers :** Le dataset ne contenait ni valeur manquante ni outlier statistique. Le risque était de forcer des corrections inutiles pour paraître plus rigoureux. On a documenté que l'absence de problème est aussi un résultat d'audit valide.

**Moyenne trompeuse pour les dépenses par pays :** La moyenne plaçait le Nigeria en tête alors qu'il ne compte que 11 clients. On a utilisé la médiane en complément pour réduire l'effet des petits échantillons.

**Distinguer doublons et homonymes :** Pour ne pas confondre un vrai doublon avec un simple homonyme, on a comparé l'ensemble des colonnes (nom, pays, âge, genre, dépenses) avant de conclure à un doublon exact.

## 5. Mode d'exécution

Ouvrir **Anaconda Prompt** (ou Miniconda Prompt) et exécuter les commandes suivantes :

```bash
conda env list
```

Cette commande affiche les environnements disponibles. Si l'environnement du projet n'existe pas encore, le créer :

```bash
conda create -n sell4all-exploration python=3.11 pandas matplotlib jupyter
```

Activer l'environnement :

```bash
conda activate sell4all-exploration
```

Naviguer vers le dossier du projet puis lancer Jupyter :

```bash
cd chemin/vers/le/projet
jupyter notebook
```

Dans le navigateur, ouvrir `Sell4All_Data_Cleaning.ipynb` et exécuter toutes les cellules dans l'ordre (`Run All`). Le fichier `dataset-sell4all.csv` doit se trouver dans le même dossier que le notebook. Le fichier `dataset-sell4all-clean.csv` est régénéré automatiquement à l'exécution.

## Fichiers du dépôt

- `SA_data_Cleaning.ipynb` — notebook complet (audit, analyse, nettoyage)
- `dataset-sell4all-clean.csv` — dataset nettoyé (`Country`, `Age`, `Gender`, `Customer spendings`)
- `README.md` — ce fichier
