# Exercice 4 — Écrire un premier Makefile

Le fichier `Makefile` contient les règles de compilation et les dépendances de `main.o` et `liste.o`.

## Observations

Après `make clean`, la commande `make` exécute les trois commandes suivantes :

```text
gcc -Wall -Wextra -std=c11 -g -c main.c
gcc -Wall -Wextra -std=c11 -g -c liste.c
gcc -Wall -Wextra -std=c11 -g -o demo main.o liste.o
```

Une seconde exécution de `make` affiche :

```text
make: 'demo' is up to date.
```

| Question | Réponse |
| --- | --- |
| A | `make` compare les dates de modification de la cible et de ses dépendances. Comme `demo`, `main.o` et `liste.o` sont plus récents que les fichiers sources nécessaires, aucune commande n'est relancée. |
| B (message exact) | `Makefile:2: *** missing separator.  Stop.` |

Les commandes d'une règle doivent commencer par une tabulation. Quatre espaces ne sont pas reconnus comme le séparateur attendu par `make`.