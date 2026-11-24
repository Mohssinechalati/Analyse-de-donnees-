# Analyse de données – Taux de change par rapport au dollar américain (USD)

## 1. Présentation du projet

Ce projet est une analyse statistique réalisée avec **R** (tidyverse) sur les taux de change de 21 devises par rapport au dollar américain, de mai 2006 à décembre 2025.

L'analyse est organisée en quatre parties, de la plus simple à la plus complète :

| Partie | Thème | Variables étudiées |
|---|---|---|
| 1 | Analyse d'une variable qualitative | `type_eco` (type d'économie) |
| 2 | Analyse d'une variable quantitative | `USD/EUR` |
| 3 | Analyse temporelle | `Date` et `USD/EUR` |
| 4 | Analyse bivariée | `USD/EUR` et `USD/GBP` |

## 2. Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `Historical_Data.csv` | Taux de change journaliers (jeu de données principal) |
| `Currencies_and_Country_EconomyWise.csv` | Pays, type d'économie et nom de chaque conversion |
| `TP2_Cas_d_une_variable_devises.R` | Script des parties 1 et 2 (une variable) |
| `TP3_Analyse_bivariee.R` | Script de la partie 4 (deux variables) |
| `projet.Rproj` | Projet RStudio (définit le dossier de travail) |
| `README.md` | Ce document |

## 3. Les données

### 3.1 `Historical_Data.csv`

- **6722 lignes** : une ligne par jour, du **16/05/2006 au 12/12/2025**.
- **22 colonnes** : la colonne `Date` et 21 taux de change.
- La date est au format `jj-mm-aaaa` (conversion avec `dmy()` de lubridate).
- Chaque colonne `USD/XXX` indique **combien d'unités de la devise XXX on obtient pour 1 dollar**. Par exemple, `USD/EUR = 0,85` signifie que 1 dollar vaut 0,85 euro.

Les 21 devises : EUR, GBP, JPY, CHF, CAD, AUD, SGD, KRW, CNY, INR, BRL, ZAR, RUB, MXN, IDR, TRY, VND, LKR, NGN, KES, BDT.

**Nature des variables :** `Date` est une variable temporelle, les 21 taux sont des variables quantitatives continues.

**Les unités ne sont pas comparables.** 1 dollar vaut environ 0,8 euro mais plus de 20 000 dongs vietnamiens. On ne peut donc pas comparer directement les écarts-types de deux devises : il faut utiliser le coefficient de variation (écart-type / moyenne).

**Valeurs manquantes.** Plusieurs devises ont des jours sans cotation :

| Devise | Valeurs manquantes | Devise | Valeurs manquantes |
|---|---|---|---|
| CHF | 0 | MXN | 399 |
| CAD | 22 | INR | 422 |
| JPY | 33 | BRL | 425 |
| ZAR | 56 | TRY | 443 |
| IDR | 147 | CNY | 582 |
| EUR | 178 | RUB | 779 |
| GBP | 181 | KES | 783 |
| AUD | 294 | LKR | 1024 |
| KRW | 315 | BDT | 1062 |
| SGD | 361 | NGN | 1127 |
| | | VND | 1279 |

Pour `USD/EUR`, il reste donc 6722 − 178 = **6544 observations**.

**Répartition par année.** Les années 2006 (à partir du 16 mai) et 2025 (jusqu'au 12 décembre) sont incomplètes : 164 observations en 2006 et 342 en 2025, contre environ 365 pour une année complète.

### 3.2 `Currencies_and_Country_EconomyWise.csv`

- **21 lignes** (une par devise) et **3 colonnes**, toutes qualitatives nominales :

| Colonne (renommée dans R) | Contenu |
|---|---|
| `Country/Zone` (`pays`) | Pays ou zone (Europe, Japon, Brésil…) |
| `Economy Type` (`type_eco`) | Type d'économie |
| `Conversion Name` (`conversion`) | Nom de la colonne correspondante dans `Historical_Data.csv` |

Les trois types d'économie sont : **économie développée** (8 pays), **marché émergent** (8 pays) et **économie frontière** (5 pays).

Ce fichier sert à relier chaque devise à son type d'économie (jointure sur `conversion`).

### 3.3 Nettoyage effectué dans R

- Le nom de colonne `USD/NGN ` contient un **espace final** : il est supprimé avec `str_trim()`.
- De même, les noms de conversion du second fichier sont nettoyés avec `str_trim()`.
- La date est convertie du texte au format date avec `dmy()`.

## 4. Utilisation

1. Ouvrir **`projet.Rproj`** dans RStudio : le dossier de travail est alors défini automatiquement.
2. Installer les packages si nécessaire :
   ```r
   install.packages(c("tidyverse", "e1071"))
   ```
3. Ouvrir un script (`TP2_...R` ou `TP3_...R`) et l'exécuter ligne par ligne avec **Ctrl + Entrée**.

Les scripts lisent les fichiers CSV par leur nom. Si R ne les trouve pas, vérifier que le nom dans `read_csv()` correspond exactement au nom du fichier dans le dossier (espaces ou tirets bas).

---

## PARTIE 1 – Variable qualitative : `type_eco`

**Objectif :** décrire la répartition des pays selon leur type d'économie.

**Analyses réalisées :**
- Tableau des effectifs, fréquences relatives et pourcentages.
- Mode d'une variable qualitative.
- Construction d'une variable ordinale (5 niveaux de USD/EUR, de « Très faible » à « Très élevé ») et recherche du maximum local.
- Déséquilibre des classes, imputation par le mode, regroupement des modalités rares.
- Graphiques : diagramme en barres (simple, trié, horizontal, avec pourcentages), camembert, facettes.

**Résultats principaux :**
- Développée : 8 (38,1 %), Émergente : 8 (38,1 %), Frontière : 5 (23,8 %).
- Il y a **deux modes** (développée et émergente) : la distribution est bimodale.
- Le rapport entre la plus grande et la plus petite modalité est de 1,6 : la variable est peu déséquilibrée.
- La moyenne n'a pas de sens pour une variable qualitative nominale.

## PARTIE 2 – Variable quantitative : `USD/EUR`

**Objectif :** décrire la distribution du taux USD/EUR.

**Analyses réalisées :**
- Variable discrète : nombre de devises manquantes par jour.
- Tableau de fréquences par classes (largeur 0,05 puis 0,025) et effet du choix des intervalles.
- Quantiles, déciles, résumé en cinq nombres, valeurs aberrantes (règle 1,5 × IQR).
- Indices de dispersion : variance, écart-type, étendue, IQR, coefficient de variation.
- Normalisation (variable centrée-réduite), asymétrie (skewness) et aplatissement (kurtosis).
- Graphiques : histogramme, densité, boîte à moustaches.

**Résultats principaux :**
- Moyenne ≈ 0,833, médiane = 0,850, écart-type ≈ 0,086 ; valeurs entre 0,625 et 1,042.
- Classe modale : [0,85 ; 0,90[ avec 1485 jours.
- Aucune valeur aberrante pour USD/EUR (bornes [0,539 ; 1,123]).
- Asymétrie ≈ −0,26 (légèrement à gauche) et aplatissement ≈ −0,94 (distribution plus plate que la normale).
- Pour la livre turque (TRY) et le naira (NGN), de nombreux points sortent des bornes, mais ce sont de vraies dévaluations et non des erreurs : il ne faut pas les supprimer.
- Avec le coefficient de variation, la devise la plus stable est le SGD (5,7 %) et les plus dispersées sont la TRY (130 %) et le NGN (104 %).

---

## PARTIE 3 – Analyse temporelle (`Date`)

### Objectif

Exploiter la variable `Date` pour étudier l'évolution du taux USD/EUR dans le temps, en complétant les deux premières parties par une dimension temporelle.

### Création des variables temporelles

À partir de la colonne `Date`, quatre nouvelles variables sont créées :

| Variable | Description | Type |
|---|---|---|
| `annee` | Année de l'observation (2006 à 2025) | Temporelle discrète |
| `mois_num` | Numéro du mois (1 à 12) | Quantitative discrète |
| `mois` | Nom du mois (Janvier à Décembre) | Qualitative ordinale |
| `jour` | Jour du mois (1 à 31) | Quantitative discrète |

### Questions et analyses

| Question | Analyse | Graphique |
|---|---|---|
| Q3.1 | Création des variables temporelles et vérification avec `glimpse()` | – |
| Q3.2 | Nombre d'observations par année, fréquences relatives et pourcentages | Diagramme en barres |
| Q3.3 | Par année : effectif, moyenne, médiane, écart-type, minimum, maximum | Courbe avec points (moyenne annuelle) |
| Q3.4 | Distribution du taux USD/EUR par année (médiane, dispersion, valeurs extrêmes) | Boxplot |
| Q3.5 | Mêmes statistiques par mois, toutes années confondues | Diagramme en barres (moyenne par mois) |
| Q3.6 | Moyenne pour chaque combinaison année-mois | Courbes multiples (une couleur par année) |
| Q3.7 | Moyenne pour chaque jour du mois (1 à 31) | Courbe avec points |

### Remarque

Les années 2006 et 2025 sont incomplètes. De plus, les comparaisons mensuelles et journalières regroupent plusieurs années et ne suffisent pas, à elles seules, à démontrer un effet saisonnier.

---

## PARTIE 4 – Analyse bivariée : `USD/EUR` et `USD/GBP`

### Objectif

Étudier la relation entre deux variables quantitatives continues : **X = USD/EUR** et **Y = USD/GBP**. Ce sont deux devises d'économies développées, ce qui laisse attendre un lien visible. Le code se trouve dans `TP3_Analyse_bivariee.R`.

### Étape 1 – Préparation des données

- Sélection des colonnes `Date`, `USD/EUR` et `USD/GBP`.
- Suppression des jours où l'une des deux valeurs manque.
- **Résultat : 6540 jours** conservés sur 6722.

### Étape 2 – Résumé univarié de chaque variable

| | Moyenne | Médiane | Écart-type | Min | Max |
|---|---|---|---|---|---|
| USD/EUR | 0,833 | 0,850 | 0,086 | 0,625 | 1,042 |
| USD/GBP | 0,698 | 0,720 | 0,094 | 0,474 | 0,932 |

Dans les deux cas la moyenne est légèrement inférieure à la médiane, ce qui indique une faible asymétrie à gauche.

### Étape 3 – Nuage de points

Représentation de USD/GBP en fonction de USD/EUR, avec la droite de régression (`geom_smooth(method = "lm")`).

**Objectif :** repérer la forme de la relation (linéaire ou non), son sens, la dispersion autour de la droite et d'éventuels groupes de points.

### Étape 4 – Covariance et corrélation

| Mesure | Valeur | Interprétation |
|---|---|---|
| Covariance | 0,00696 | Positive : les deux taux évoluent dans le même sens. Dépend des unités. |
| Corrélation de Pearson | 0,865 | Forte corrélation linéaire positive. |
| Corrélation de Spearman | 0,878 | Lien fort et monotone, légèrement supérieur à Pearson. |
| Test de corrélation | p-value ≈ 0 | Corrélation significativement différente de 0. |

### Étape 5 – Régression linéaire simple

Modèle : `USD/GBP = a + b × USD/EUR`

| Paramètre | Valeur | Interprétation |
|---|---|---|
| Pente | 0,943 | Si USD/EUR augmente de 0,1, USD/GBP augmente en moyenne de 0,094. |
| Ordonnée à l'origine | −0,087 | Peu interprétable (USD/EUR n'est jamais proche de 0). |
| R² | 0,747 | Environ 75 % de la variance de USD/GBP est expliquée par USD/EUR (R² = r²). |
| Écart-type des résidus | 0,047 | Erreur typique de prédiction. |

### Étape 6 – Diagnostic des résidus

Tracé du graphique résidus / valeurs prédites et de l'histogramme des résidus.

**Constat :** l'histogramme n'est pas une cloche symétrique centrée sur 0. Il présente un pic principal vers +0,01 à +0,02, une asymétrie à gauche et une seconde bosse autour de −0,11.

Cette seconde bosse correspond à quelques périodes précises où les résidus sont très négatifs :

| Année | Résidu moyen | Jours avec résidu < −0,07 |
|---|---|---|
| 2006 | −0,120 | 164 |
| 2007 | −0,102 | 229 |
| 2015 | −0,108 | 290 |
| 2016 | −0,024 | 41 |

Sur les autres années, les résidus restent proches de 0 (de −0,02 à +0,05).

### Conclusion de la partie 4

USD/EUR et USD/GBP sont **fortement corrélés** (r = 0,865, R² = 0,747). Le diagnostic des résidus montre cependant que le modèle linéaire simple est **insuffisant** : le lien entre l'euro et la livre **n'est pas stable dans le temps**, avec des écarts importants en 2006-2007 et en 2015.

---

## 5. Limites générales

- **Séries temporelles** : les observations d'un jour sont proches de celles du jour suivant. L'hypothèse d'indépendance des résidus n'est donc pas respectée, et deux séries qui évoluent lentement ont souvent une forte corrélation « mécanique ».
- **Référence commune** : tous les taux sont exprimés par rapport au dollar, donc une partie du lien entre deux devises vient de la force ou de la faiblesse du USD lui-même.
- **Valeurs manquantes** : leur nombre varie fortement selon la devise (de 0 pour le CHF à 1279 pour le VND), ce qui limite la comparaison entre devises.
- **Années incomplètes** : 2006 et 2025.
- **Corrélation n'est pas causalité.**