# Exercice 1 — Découper la liste chaînée en trois fichiers

| Question | Réponse |
| --- | --- |
| A | Le type `Maillon` est utilisé par `main.c` et `liste.c`. Le placer dans `liste.h` permet aux deux fichiers de partager la même définition. Une définition placée uniquement dans `liste.c` ne serait pas visible dans `main.c`, car les fichiers sont compilés séparément. |
| B | Inclure `liste.h` dans `liste.c` donne accès au type `Maillon` et permet au compilateur de vérifier que les définitions des fonctions correspondent à leurs déclarations publiques (types de retour et paramètres). |
