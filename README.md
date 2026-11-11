# Analyse-de-donnees-
# PARTIE 3 – Analyse temporelle (Date)

## 1. Objectif

Cette partie consiste à exploiter la variable `Date` déjà présente dans le fichier `Historical Data.csv` afin d'étudier l'évolution du taux de change USD/EUR dans le temps.

L'objectif est de compléter les deux premières parties de l'analyse statistique en ajoutant une dimension temporelle.

## 2. Création des variables temporelles

À partir de la colonne `Date`, nous avons créé quatre nouvelles variables :

| Variable | Description | Type |
|---|---|---|
| `annee` | Année de l'observation (2006 à 2025) | Temporelle discrète |
| `mois_num` | Numéro du mois (1 à 12) | Quantitative discrète |
| `mois` | Nom du mois (Janvier à Décembre) | Qualitative ordinale |
| `jour` | Jour du mois (1 à 31) | Quantitative discrète |

Ces variables permettent d'effectuer des analyses selon différentes périodes.

## 3. Questions et analyses réalisées

### Q3.1 – Identification des variables

Création des variables temporelles à partir de `Date` et vérification de leur structure avec `glimpse()`.

### Q3.2 – Répartition des observations par année

- Calcul du nombre d'observations pour chaque année.
- Calcul des fréquences relatives et des pourcentages.
- Création d'un diagramme en barres.

**Objectif :** visualiser la répartition des données disponibles sur chaque année.

### Q3.3 – Statistiques descriptives annuelles

Calcul, pour chaque année, de :
- L'effectif disponible.
- La moyenne.
- La médiane.
- L'écart-type.
- Le minimum.
- Le maximum.

**Graphique :** une courbe avec des points représentant l'évolution de la moyenne annuelle du taux USD/EUR.

**Objectif :** identifier les années où le taux moyen est le plus élevé ou le plus faible.

### Q3.4 – Distribution du taux USD/EUR par année

**Graphique : Boxplot (boîte à moustaches).**

Ce graphique permet de comparer :
- La médiane de chaque année.
- La dispersion des taux.
- Les valeurs extrêmes.
- Les différences de distribution entre les années.

### Q3.5 – Analyse du taux USD/EUR selon les mois

Calcul, pour chaque mois :
- L'effectif.
- La moyenne.
- La médiane.
- L'écart-type.
- Le minimum.
- Le maximum.

**Graphique :** diagramme en barres représentant la moyenne du taux USD/EUR pour les douze mois.

**Objectif :** comparer les taux moyens de janvier à décembre, toutes années confondues.

### Q3.6 – Analyse mensuelle par année

Calcul de la moyenne du taux USD/EUR pour chaque combinaison année-mois.

**Graphique : Courbes multiples.**

Chaque couleur représente une année et chaque courbe montre l'évolution du taux moyen au fil des douze mois.

**Objectif :** comparer les variations mensuelles entre les différentes années.

### Q3.7 – Analyse selon le jour du mois

Calcul de la moyenne du taux USD/EUR pour chaque jour du mois (de 1 à 31), toutes années confondues.

**Graphique : Courbe avec points.**

**Objectif :** observer les différences éventuelles entre les taux moyens des différents jours du mois.

## 4. Résumé des graphiques ajoutés

| Question | Type de graphique | Information représentée |
|---|---|---|
| Q3.2 | Diagramme en barres | Effectifs par année |
| Q3.3 | Courbe avec points | Moyenne annuelle |
| Q3.4 | Boxplot | Distribution annuelle |
| Q3.5 | Diagramme en barres | Moyenne par mois |
| Q3.6 | Courbes multiples | Évolution mensuelle par année |
| Q3.7 | Courbe avec points | Moyenne selon le jour |

## 5. Conclusion

Cette troisième partie permet d'étudier le comportement du taux USD/EUR selon différentes échelles temporelles : année, mois et jour.

Elle complète les analyses qualitatives et quantitatives précédentes en permettant d'observer les évolutions, les fluctuations et les différences entre les périodes.

**Remarque :** les années 2006 et 2025 sont incomplètes dans le jeu de données. De plus, les comparaisons mensuelles et journalières regroupent plusieurs années et ne suffisent pas, à elles seules, à démontrer un effet saisonnier.
