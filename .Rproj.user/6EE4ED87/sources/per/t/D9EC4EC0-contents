library(tidyverse)

histo <- read_csv("Historical Data.csv")
names(histo) <- str_trim(names(histo))
histo <- histo |> mutate(Date = dmy(Date))

biv <- histo |>
  select(Date, eur = `USD/EUR`, gbp = `USD/GBP`) |>
  drop_na(eur, gbp)

nrow(biv)   # 6540
#resume univarie pour chacune des variables
summary(biv$eur); sd(biv$eur)
summary(biv$gbp); sd(biv$gbp)
#les nuages de points
ggplot(biv, aes(x = eur, y = gbp)) +
  geom_point(alpha = 0.3, color = "steelblue") +
  geom_smooth(method = "lm", color = "tomato", se = TRUE) +
  labs(x = "USD/EUR", y = "USD/GBP",
       title = "Relation entre USD/EUR et USD/GBP")
#la courbe est lineair,croissante,une forte disperssion autour d'elle 

#covariance et coorelation 
cov(biv$eur, biv$gbp)                         # 0.00696
cor(biv$eur, biv$gbp)                         # 0.8646  (Pearson)
cor(biv$eur, biv$gbp, method = "spearman")    # 0.8783
cor.test(biv$eur, biv$gbp)                    # p-value < 2.2e-16

#Covariance positive (0,007) : les deux taux évoluent dans le même sens. Sa valeur dépend des unités, elle ne mesure donc pas l'intensité du lien.
#Pearson r = 0,865 : forte corrélation linéaire positive.
#Spearman ρ = 0,878 : légèrement supérieur à Pearson. Le lien est donc fort et monotone, avec une petite part non linéaire.
#p-value ≈ 0 : la corrélation est significativement différente de 0.

#regression lineaire simple
modele <- lm(gbp ~ eur, data = biv)
summary(modele)
#Pente = 0,943 : quand USD/EUR augmente de 0,1, USD/GBP augmente en moyenne de 0,094.
#Ordonnée à l'origine = −0,087 : peu interprétable ici, car USD/EUR n'est jamais proche de 0.
#R² = 0,747 : environ 75 % de la variance de USD/GBP est expliquée par USD/EUR. Comme R² = r², on retrouve 0,8646² = 0,747.
#Écart-type des résidus ≈ 0,047 : erreur typique de prédiction.

#diagnostic des résidus
biv <- biv |> mutate(pred = fitted(modele), res = resid(modele))

ggplot(biv, aes(x = pred, y = res)) +
  geom_point(alpha = 0.3) +
  geom_hline(yintercept = 0, color = "red") +
  labs(x = "Valeurs prédites", y = "Résidus")

ggplot(biv, aes(x = res)) + geom_histogram(bins = 40, fill = "steelblue")

# le modele lineaire est insufisant

