# Exercice 5 — La dépendance au fichier d'en-tête

Après `make clean && make`, le projet compile correctement.

| Étape | Ce que make recompile |
| --- | --- |
| 2, avec la dépendance | `main.o` et `liste.o`, puis l'édition de liens de `demo`. |
| 4, sans la dépendance | Seulement `liste.o`, puis l'édition de liens de `demo`. `main.o` reste inchangé. |

Pour rendre l'expérience fiable, `liste.h` a été daté après les fichiers objets avant de relancer `make`.

| Question | Réponse |
| --- | --- |
| A | Avec la dépendance, chaque fichier objet qui inclut `liste.h` est recompilé. Sans la dépendance de `main.o`, `make` ne sait pas que `main.o` dépend aussi de `liste.h` et conserve donc une version potentiellement obsolète. |
| B | L'exécutable contient un `main.o` compilé avec l'ancienne définition de `Maillon` et un `liste.o` compilé avec la nouvelle. Le programme peut donc utiliser des objets incompatibles et produire un comportement incorrect ; il faut recompiler tous les fichiers qui incluent l'en-tête. |

Le `Makefile` a été rétabli avec la règle générique complète :

```makefile
CC     = gcc
CFLAGS = -Wall -Wextra -std=c11 -g
OBJ    = main.o liste.o

demo: $(OBJ)
	$(CC) $(CFLAGS) -o $@ $^

%.o: %.c liste.h
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) demo

.PHONY: clean
```