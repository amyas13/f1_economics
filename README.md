# F1 & Business : L'argent fait-il encore la loi ? (Étude 2014-2024)

![Dashboard Power BI – L'économie de la performance en F1](powerbi/dashboard.png)

L'objectif de ce projet, c'est de disséquer le lien entre le portefeuille des écuries et leurs points au championnat. On parle souvent de la F1 comme d'un sport d'ingénieurs, mais c'est surtout un sport de banquiers. J'ai voulu voir si le Cost Cap de 2021 avait vraiment cassé cette dynamique.

## Ce que les chiffres disent (2014-2024)

En compilant 109 lignes de données sur 11 saisons, les conclusions sont assez flagrantes. Avant 2021, on était dans un système quasi féodal : le "Big Three" (Mercedes, Ferrari, Red Bull) claquait entre 280 et 480 M$ par an. En face, les petites écuries essayaient de survivre avec 75 M$. Résultat ? Un écart de 1 à 5 qui se reflétait exactement au classement.

**Le tournant de 2021** : Depuis le plafond budgétaire, c'est une autre histoire. Les budgets convergent enfin (autour de 145-170 M$). Sur mon dashboard Power BI, le graphique "Budget vs Points" montre une bande verticale super étroite après 2021, alors qu'avant c'était l'anarchie totale. On a même vu une rotation au sommet (Mercedes, puis Red Bull, et McLaren en 2024) qui aurait été impensable avec les budgets illimités d'autrefois.

## Le "Cousu main" : ma méthodologie

Pour le côté technique, j'ai dû mixer des sources assez hétérogènes :

- **Sportif** : le dataset Kaggle de Rohan Rao (une mine d'or pour les résultats de 1950 à 2024).
- **Financier** : là, c'est devenu complexe. J'ai dû construire mon propre CSV (`budgets_ecuries.csv`) en recoupant les enquêtes de RaceFans, les rapports de conformité de la FIA et les estimations de Forbes pour 2025. Chaque ligne est annotée avec sa source et son niveau de fiabilité (HAUTE, MOYENNE, FAIBLE).
- **Traitement** : j'ai tout scripté sous Python 3.11 avec pandas, dans le notebook `notebooks/01_exploration.ipynb`. Le plus gros défi ? L'harmonisation. Il a fallu créer une table de correspondance pour que l'algorithme comprenne que Lotus, Renault et Alpine, c'est en fait la même entité à Enstone. Idem pour Force India qui devient Aston Martin.

Le dashboard final est dans `powerbi/f1_economics_dashboard.pbix` (éditable sous Power BI Desktop), avec un export PDF dispo dans le même dossier pour ceux qui n'ont pas Power BI.

## Performance et ROI (le nerf de la guerre)

J'ai calculé une métrique de "Retour sur Investissement" (points par million dépensé). Surprise : si Mercedes domine le rendement historique (1,79), des écuries comme Aston Martin (0,96) s'en sortent mieux que ce que leur réputation suggère. À l'inverse, Williams (0,61) reste dans le dur malgré son prestige.

## Quelques bémols à garder en tête

Je préfère être transparent sur les limites de l'analyse :

1. **Estimation vs réalité** : avant 2021, les écuries étaient des coffres-forts. Les chiffres sont donc des estimations journalistiques (notées en fiabilité "MOYENNE" ou "FAIBLE" dans mes données).
2. **Plafond vs total** : le Cost Cap FIA ne compte pas tout. Les salaires des pilotes et le marketing sont hors budget. Mon dataset fait bien la distinction entre `budget_plafonne` et `budget_total`.
3. **Data 2025** : j'ai déjà intégré les budgets 2025, mais sans les résultats de fin de saison côté Kaggle, ils ne sont pas encore exploités dans les visuels. Mise à jour prévue dès que l'API Ergast/Jolpica sera à jour.

## La suite

C'est le premier projet d'une série. Le prochain sur la grille : appliquer du Machine Learning à la prédiction des résultats F1 (qualifs et courses).
