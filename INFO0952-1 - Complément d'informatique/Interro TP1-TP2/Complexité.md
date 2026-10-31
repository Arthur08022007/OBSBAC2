# Complexité

Slides : partie 2, transparents 107 à 119 pour le temps et le grand O. L'espace est traité sur la recherche dichotomique, transparents 137 (récursive, O(log N) à cause de la pile d'appels) et 138 (itérative, O(1)).

La même grille sert pour [[Tau de Kendall]] et pour [[findFirstTrue]].

## Temps

On se place en pire cas, pour une grande taille N. On compte des opérations élémentaires, puis on garde le terme dominant. Une boucle imbriquée sur toutes les paires est O(N²). Une boucle qui coupe l'intervalle en deux à chaque tour est O(log N). Un tri fusion qui fait un travail O(N) à chacun de ses O(log N) niveaux est O(N log N).

Le grand O utilisé en cours est la borne supérieure serrée : on dit O(N²) pour la double boucle, même si O(N³) est aussi une borne supérieure au sens strict de la définition.

## Espace

On compte la mémoire ajoutée par la fonction, en plus de l'entrée.

- Quelques entiers et l'entrée elle-même : O(1).
- Un tableau auxiliaire de N éléments : O(N).
- Une chaîne d'appels récursifs de profondeur P, avec O(1) par appel : O(P).

Le tri fusion appelle une moitié, puis l'autre, puis fusionne. Les deux moitiés ne sont pas en mémoire ensemble. Le tampon de fusion du niveau courant fait au plus N éléments, et la profondeur d'appels est O(log N). Le pic est O(N).

La case O(N log N) correspond au temps du tri fusion, ou à une version qui garderait vivants les tampons de tous les niveaux en même temps. Ce n'est pas l'espace du tri fusion usuel, celui dont le `merge` alloue son tampon et le libère en revenant.

## Les quatre cases de l'interro

| Fonction | Temps | Espace |
| --- | --- | --- |
| `kendallTauSlow` | O(N²) | O(1) |
| `kendallTauFast` | O(N log N) | O(N) |
| `findFirstTrue` dichotomique | O(log N) appels au prédicat | O(1) |
| `findFirstTrue` naïf | O(N) appels au prédicat | O(1) |

La question de l'interro à blanc porte sur l'espace des deux Kendall. Les cases O(N²) et O(N log N) sont leurs temps.
