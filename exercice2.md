# Exercice 2 — Compiler en deux temps, à la main

Commandes exécutées :

```sh
gcc -Wall -Wextra -Werror -c main.c
gcc -Wall -Wextra -Werror -c liste.c
ls -l main.o liste.o
gcc -o demo main.o liste.o
./demo
```

Sortie du programme :

```text
liste     : 50 -> 40 -> 30 -> 20 -> 10 -> NULL
longueur  : 5
contient 30 : oui
liberee
```

| Question | Réponse |
| --- | --- |
| A | On obtient deux fichiers objets : `main.o` et `liste.o`. Il n'y a pas de `liste.h.o` : le contenu du fichier d'en-tête est inclus dans chaque fichier `.c` qui l'utilise, il n'est pas compilé séparément. |
| B | La commande unique recompile les deux fichiers `.c` à chaque fois. Avec les deux étapes, on peut recompiler seulement le fichier modifié, puis refaire le lien en réutilisant l'autre fichier `.o`, si ses dépendances n'ont pas changé. |
