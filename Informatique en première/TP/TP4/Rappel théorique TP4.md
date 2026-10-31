# Complexité en temps

Rappel théorique — TP 4

Syllabus, chapitre 3, section 3.2

---

# Le constat

Trois programmes résolvent le même problème : trouver les nombres parfaits jusqu’à `n_max`.

Quand `n_max` est multiplié par 10, le temps des deux premiers est multiplié par environ 100. Le troisième change d’allure et reste utilisable bien plus loin.

La deuxième solution est environ deux fois plus rapide que la première. L’allure, elle, est la même.

On veut prédire cette allure sans mesurer, et sans dépendre de la machine ni du compilateur.

---

# Ce qu’on retient du temps d’exécution

La complexité en temps est le temps nécessaire, exprimé en fonction de la taille des paramètres.

Trois restrictions :

- on ne regarde que les **grandes** valeurs des paramètres ;
- on néglige les **constantes** de proportionnalité ;
- s’il existe plusieurs exécutions pour une même taille, on garde la plus lente : le **pire cas**.

La complexité en espace sera vue plus tard.

---

# Compter des opérations

Pour calculer ce temps, on compte des opérations élémentaires.

`n++` peut compter pour 1 opération, pour 3 (lire, incrémenter, écrire), ou pour un nombre k.

Si k reste borné par une valeur **indépendante** des paramètres, la complexité ne change pas.

C’est ce qui rend le résultat insensible au processeur et au compilateur.

---

# La notation grand-O

On peut dire en français, "est asymptotique"

Soient f et g des fonctions de ℕ vers les réels positifs ou nuls. Elles décrivent un temps en fonction de n.

On écrit **f ∈ O(g)** lorsqu’il existe un seuil n₀ et une constante c ≥ 0 tels que

pour tout n > n₀, **f(n) ≤ c · g(n)**.

Au-delà du seuil, f reste sous un multiple de g. On écrit aussi, par abus, f(n) ∈ O(g(n)).

---

# Trois propriétés

- Si f ∈ O(g) et k ≥ 0, alors k · f ∈ O(g).
- Si e ∈ O(g) et f ∈ O(g), alors e + f ∈ O(g).
- Si e ∈ O(g) et f ∈ O(h), alors e · f ∈ O(g · h).

En pratique : des coûts **additionnés**, le plus gros absorbe les autres. Des coûts **multipliés** (une boucle dans une boucle), ils se multiplient.

---

# Polynômes et logarithmes

Un polynôme aₘ nᵐ + … + a₀, avec aₘ > 0, appartient à **O(nᵐ)**.

Seul le terme de plus haut degré compte. Les autres coefficients, même négatifs, disparaissent.

Donc 3n² + 100n + 5 et n²/4 sont tous les deux dans O(n²).

logₐ n ∈ O(logᵦ n) dès que a > 1 et b > 1. La base ne compte pas : on écrit **O(log n)**.

---

# Les classes

De la plus efficace à la moins efficace :

signifie du plus efficace au moins efficaec

O(1) ⊂ O(log n) ⊂ O(n) ⊂ O(n log n) ⊂ O(n²) ⊂ O(n³) ⊂ ⋯ ⊂ O(2ⁿ)

- **O(1)** : le temps reste borné, quelle que soit la valeur de n.
- **O(n)** : linéaire. Avec O(log n) et O(1), ce sont les programmes très efficaces.
- **O(n log n)** : encore utilisable pour de grandes valeurs de n.
- **O(n²), O(n³), …** : complexités polynomiales.
- **O(2ⁿ)** : exponentielle, puis les classes encore plus lentes.

La frontière souvent citée sépare polynomial et exponentiel. Un programme quadratique peut déjà être trop lent.

---

# Comment on calcule

1. Nommer le paramètre : n, `n_max`, la taille d’un tableau.
2. Grouper les instructions selon le nombre de fois où elles s’exécutent.
3. Écrire chaque groupe en O(…).
4. Sommer. Le groupe dominant donne la complexité du programme.
5. Rester au **pire cas**. Une sortie anticipée (`m <= n`, un `break`) ne baisse la borne que si elle empêche **toujours** d’aller au bout de la boucle.

---

# D’où vient le coût

Dans les trois programmes, le coût est celui de la boucle interne, répétée pour chaque n jusqu’à `n_max`.

- Solution 1 : `d < n` — au plus n tours.
- Solution 2 : `d <= n / 2` — au plus n/2 tours.
- Solution 3 : `d * d <= n` — au plus environ √n tours.

Le test `m <= n` peut arrêter plus tôt. Dans le pire cas, on va quand même jusqu’au bout.

---

# Les trois complexités

**Solution 1.** Pour n = 1, 2, …, n_max, la boucle interne fait au plus n tours.

1 + 2 + … + n_max = n_max(n_max + 1) / 2 ∈ **O(n_max²)**.

**Solution 2.** La somme est environ deux fois plus petite, donc encore **O(n_max²)**.

Environ deux fois plus rapide à l’horloge, et la même classe. Le facteur 100, quand `n_max` est multiplié par 10, est celui de n².

**Solution 3.** On additionne des √n. Le total est dans **O(n_max × √n_max)**, c’est-à-dire **O(n_max^1,5)**.

n^1,5 croît moins vite que n² : le programme reste utilisable pour de bien plus grandes valeurs.

---

# Boucles à reconnaître

- `for (i = 0; i < n; i++)`, corps en O(1) → **O(n)**
- la même boucle imbriquée sur i et sur j → **O(n²)**
- `for (i = 1; i < n; i *= 2)` → **O(log n)** tours
- boucle tant que `d * d <= n` → **O(√n)** tours
- instructions à la suite → on additionne, le maximum l’emporte
- `if` / `else` → la branche la plus coûteuse

---

# Ce qui ne change pas la classe

- commencer à 2 plutôt qu’à 1 ;
- s’arrêter à n/2 plutôt qu’à n ;
- un `printf` exécuté au plus n fois, à côté d’une boucle en n² ;
- la fréquence du processeur, ou l’option `-O3` du compilateur.

Ce qui change la classe, c’est un nombre de tours qui dépend **autrement** de n.

Passer de n tours à √n tours fait passer le programme de O(n²) à O(n^1,5).

---

# À retenir

**f ∈ O(g)** : au-delà d’un seuil, f(n) ≤ c · g(n).

Pire cas. Grandes valeurs. Constantes oubliées.

Polynôme : on garde le plus haut degré. Logarithme : la base est libre.

Des boucles imbriquées : on multiplie les nombres de tours.

**O(n² / 2) = O(n²).**
