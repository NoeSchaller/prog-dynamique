# Introduction


```{warning}
* installer l'extension https://sphinxcontrib-spelling.readthedocs.io/en/latest/install.html pour vérifier l'orthographe.

```

Ce tutoriel présente le programmation dynamique, qui est une stratégie générale
de résolution de problèmes du type "diviser pour régner". Elle est souvent
utilisée pour résoudre de manière exacte des problèmes d'optimisation
combinatoires tels que le problème du sac à dos. 

```{tip}
La programmation dynamique est
généralement perçue comme un sujet difficile. En réalité, cela vient du fait que
les gens ont souvent tendance à vouloir appliquer une recette de cuisine toute
faite, sans trop réfléchir à son fonctionnement. 

Ce travail a pour objectif de présenter la programmation dynamique de manière compréhensible et progressive, pour que le lecteur puisse en comprendre les rouages et pour qu'il soit capable d'identifier les problèmes susceptibles d'être résolus par cette stratégie et de la mettre en œuvre concrètement dans différents contextes.
```

```{admonition} Stratégie de diviser pour régner
---
class: info
---
Le **diviser pour régner** (*Divide and Conquer* en anglais) est une stratégie
très utilisée en informatique pour résoudre des problèmes épineux. En effet, de
très nombreux problèmes peuvent être résolus en commençant par résoudre une
variante plus simple du problème en question.

De manière générale, cette stratégie procède de la manière suivante:

* Décomposer le problème à résoudre en sous-problèmes plus faciles à résoudre
* Continuer à décomposer les sous-problèmes en sous-sous-problèmes, jusqu'à ce que le problème soit trivial à résoudre
* Combiner les solutions des sous-problèmes pour résoudre le problème initial.

Les algorithmes suivants, fort connus, utilisent par exemple cette stratégie:

* Le tri rapide
* La recherche dichotomique
* Le calcul récursif des termes de la suite de Fibonacci
```

Il arrive cependant assez souvent que l'application naïve d'une stratégie de
diviser pour régner débouche sur un algorithme très inefficace dont la
complexité est {math}`\Theta(2^n)` si {math}`n` est la taille de l'entrée. C'est par exemple
le cas si l'on calcule le {math}`n`-ième terme de la suite de Fibonacci de la manière
suivante:

```{literalinclude} scripts/fib-timeit.py
:linenos:
```

L'exécution de ce programme produit la sortie suivante:

```
fib(5) exécuté en 0.001 ms
fib(10) exécuté en 0.011 ms
fib(20) exécuté en 1.086 ms
fib(30) exécuté en 136.887 ms
fib(40) exécuté en 18934.32 ms
```

On voit bien que l'algorithme n'est pas efficace, même pour des valeurs
relativement petites de {math}`n`. L'exécution de l'appel pour {math}`n=50`  est
même tellement lente que le programme ne produit aucune sortie en temps
raisonnable. Nous allons expliquer pourquoi cet algorithme récursif est
tellement inefficace et comment utiliser la **mémoïsation**, une technique
fondamentale à la programmation dynamique, pour rendre une telle stratégie
beaucoup plus efficace en évitant de refaire plusieurs fois des calculs déjà
effectués au préalable.

La programmation dynamique sera appliquée à la résolution de plusieurs problèmes
simples qui permettront de dégager des traits généraux d'implémentation de
programmation dynamique. Nous terminerons par une application à de petites
instances du problème du sac à dos.