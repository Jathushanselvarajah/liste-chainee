# Exercice 3 — Provoquer les trois erreurs classiques

Les trois cas ont été testés dans des copies temporaires du projet, avec `gcc -Wall -Wextra -c main.c`. Pour le cas 1, cette compilation réussit, puis `gcc -o demo main.o` échoue. Les messages ci-dessous sont ceux obtenus sur ce Mac (arm64).

| Cas | Premier message exact | Compilation ou lien |
| --- | --- | --- |
| 1 — Fichier objet oublié | `Undefined symbols for architecture arm64:` | Lien |
| 2 — Inclusion oubliée | `main.c:5:5: error: use of undeclared identifier 'Maillon'` | Compilation |
| 3 — Garde d'inclusion oubliée | `./liste.h:4:16: error: redefinition of 'Maillon'` | Compilation |

| Question | Réponse |
| --- | --- |
| 1 | Le cas 1 vient de l'éditeur de liens : `main.o` a bien été produit, mais les définitions des fonctions manquent parce que `liste.o` n'est pas fourni. Le message se termine par `ld: symbol(s) not found for architecture arm64`, puis `clang: error: linker command failed with exit code 1 (use -v to see invocation)`. |
| 2 | Le premier message, qui dit que `Maillon` n'est pas déclaré, est celui à traiter en premier. Il indique que le compilateur ne connaît pas le type défini dans `liste.h`. Les autres erreurs viennent aussi de l'inclusion manquante. |
| 3 | Le problème apparaît lorsqu'un même en-tête est inclus plusieurs fois dans un même fichier `.c`, directement ou indirectement. Par exemple, `main.c` inclut `liste.h` et un autre en-tête qui inclut lui aussi `liste.h`. La garde empêche de définir deux fois `Maillon`. Le cas 3 provoque volontairement cette situation avec deux inclusions directes. |

La version correcte du projet a ensuite été recompilée et exécutée avec succès :

```sh
gcc -Wall -Wextra -Werror -c main.c
gcc -Wall -Wextra -Werror -c liste.c
gcc -o demo main.o liste.o
./demo
```

```text
liste     : 50 -> 40 -> 30 -> 20 -> 10 -> NULL
longueur  : 5
contient 30 : oui
liberee
```
