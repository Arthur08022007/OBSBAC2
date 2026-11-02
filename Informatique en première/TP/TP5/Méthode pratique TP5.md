# Méthode pratique pour le TP5

Pour chaque boucle :

1. préciser ce que représentent les variables juste avant un tour ;
2. formuler une propriété générale, valable pour n'importe quelle valeur de l'indice ;
3. vérifier l'initialisation ;
4. supposer l'invariant vrai, exécuter mentalement le corps et vérifier sa conservation ;
5. utiliser la sortie de boucle pour obtenir la postcondition ;
6. si nécessaire, donner un variant pour justifier la terminaison ;
7. traduire la preuve en commentaires ou en explications courtes, sans raconter chaque tour particulier.

Il faut faire attention aux indices : pour `i` au début du tour, les éléments déjà traités sont souvent ceux d'indices `0` à `i - 1`. Il faut aussi vérifier les préconditions, par exemple `n > 0` pour initialiser un maximum avec `tab[0]`.
