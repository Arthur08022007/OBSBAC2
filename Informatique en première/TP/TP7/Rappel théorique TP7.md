# Tableaux et chaînes de caractères en C

Rappel théorique — TP 7  
Synthèse du chapitre 5 du [[info-syllabus-2026.pdf|syllabus]] : *Les tableaux et les chaînes de caractères* (p. 133–160)

---

## Vecteurs : une suite d’éléments de même type

Un **vecteur** (ou tableau unidimensionnel) contient un nombre fixé d’éléments de même type. Les indices commencent à `0` : un tableau de taille `n` a donc des indices de `0` à `n - 1`.

```c
int valeurs[5];                 /* indices : 0 à 4 */
int premiers[] = {2, 3, 5, 7}; /* la taille vaut 4 */
```

On lit ou modifie un élément avec `tableau[indice]` :

```c
valeurs[0] = 12;
valeurs[1] = valeurs[0] + 3;
```

En C, l’accès ne vérifie pas que l’indice est valide. Il faut toujours garantir `0 <= indice < taille`; un accès hors limites produit un comportement indéfini et peut corrompre la mémoire.

La taille d’un tableau déclaré de cette manière est une constante connue à la compilation. `const` peut empêcher la modification de ses éléments :

```c
const int limites[] = {10, 20, 30};
```

## Parcourir un vecteur

La boucle classique visite chaque élément une fois :

```c
for (unsigned i = 0; i < n; i++) {
    /* traiter tab[i] */
}
```

Vérifier soigneusement la borne de la boucle : avec `i < n`, le dernier accès est `tab[n - 1]`. Un tableau vide ne doit pas être indexé.

## Passer un tableau à une fonction

Un paramètre tableau est écrit avec des crochets. La fonction doit recevoir séparément sa taille, car celle-ci n’est pas transmise avec le tableau.

```c
void afficher(const int tab[], unsigned n)
{
    for (unsigned i = 0; i < n; i++)
        printf("%d ", tab[i]);
}
```

Lors d’un appel, le tableau est transmis sous la forme d’un **pointeur vers son premier élément**. La fonction peut donc modifier les éléments du tableau fourni par l’appelant. Utiliser `const` dans le paramètre (par exemple `const int tab[]`) exprime que la fonction ne les modifie pas.

Un décalage de pointeur permet de désigner un sous-vecteur : `tab + k` pointe vers `tab[k]`. Ainsi, une fonction qui traite son argument à partir de l’indice `0` peut recevoir `tab + k` pour commencer à l’élément `k`. Le pointeur fourni doit toujours permettre les accès effectués par la fonction.

## Trier un vecteur

### Tri par insertion

Le tri par insertion maintient un préfixe déjà trié. À chaque étape, il prend l’élément suivant, décale vers la droite les éléments plus grands, puis insère l’élément à sa place.

```c
void tri_insertion(int v[], int n)
{
    for (int k = 1; k < n; k++) {
        int a = v[k];
        int i = k - 1;

        while (i >= 0 && v[i] > a) {
            v[i + 1] = v[i];
            i--;
        }
        v[i + 1] = a;
    }
}
```

- Temps : `O(n²)` dans le pire cas (par exemple, un vecteur initialement trié en ordre décroissant).
- Mémoire supplémentaire : `O(1)`.
- Il est souvent efficace pour de petits tableaux ou des données déjà presque triées.

Le type signé de `i` est nécessaire ici : après le décalage de l’élément d’indice `0`, il vaut `-1`.

### Tri par fusion

Le tri par fusion suit la stratégie **diviser pour régner** :

1. Si le sous-vecteur contient zéro ou un élément, il est déjà trié.
2. Le couper en deux sous-vecteurs.
3. Trier récursivement chaque moitié.
4. **Fusionner** les deux moitiés triées en comparant leurs prochains éléments et en recopiant le plus petit.

La fusion parcourt chaque élément un nombre constant de fois. Le temps total du tri est `O(n log n)` et la mémoire auxiliaire est `O(n)`. Il est plus efficace que le tri par insertion sur de grands tableaux, au prix d’un espace de travail supplémentaire et de la récursivité.

Lors d’une fusion, prévoir un curseur par moitié et un curseur pour le résultat. Quand une moitié est épuisée, recopier directement les éléments restants de l’autre.

## Chaînes de caractères

En C, une chaîne est un tableau de `char` terminé par le caractère nul `\0`. Ce caractère marque la fin de la chaîne et doit lui aussi tenir dans le tableau.

```c
char mot[] = "chat";  /* 'c', 'h', 'a', 't', '\0' : 5 cases */
char message[21];     /* au plus 20 caractères, plus '\0' */
```

La taille de stockage doit donc être au moins la longueur maximale du texte plus un. Une chaîne qui n’est pas terminée par `\0` ne peut pas être parcourue correctement comme une chaîne C.

On peut lire une chaîne caractère par caractère jusqu’au terminateur :

```c
for (unsigned i = 0; s[i] != '\0'; i++) {
    /* traiter s[i] */
}
```

Comme `\0` vaut zéro, la condition `s[i]` est également couramment utilisée. Pour copier une chaîne dans un tableau destination, il faut copier le terminateur et ne jamais dépasser la capacité allouée. Les tableaux ne sont pas affectables en bloc : après leur définition, une instruction comme `mot = "autre";` est invalide; il faut copier les caractères.

Exemple de comptage des chiffres décimaux dans une chaîne :

```c
unsigned nb_chiffres(const char s[])
{
    unsigned n = 0;

    for (unsigned i = 0; s[i] != '\0'; i++)
        if (s[i] >= '0' && s[i] <= '9')
            n++;

    return n;
}
```

## Tableaux multidimensionnels

Les tableaux à plusieurs dimensions se déclarent en ajoutant une paire de crochets par dimension. Les indices de chaque dimension commencent à `0`.

```c
int matrice[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};

matrice[1][2] = 42; /* deuxième ligne, troisième colonne */
```

Pour une matrice de `lignes` lignes et `colonnes` colonnes, les indices valides sont `0 <= i < lignes` et `0 <= j < colonnes`. Les éléments sont rangés ligne par ligne en mémoire.

Dans un paramètre de fonction, la taille de la première dimension peut être omise, mais les dimensions suivantes doivent être indiquées pour que le compilateur puisse calculer l’adresse des éléments :

```c
void afficher_matrice(const int m[][4], unsigned nb_lignes)
{
    for (unsigned i = 0; i < nb_lignes; i++)
        for (unsigned j = 0; j < 4; j++)
            printf("%d ", m[i][j]);
}
```



## À retenir

- Les indices d’un tableau vont de `0` à `taille - 1`; le C ne contrôle pas les accès hors limites.
- Une fonction recevant un tableau doit aussi recevoir sa taille; ses modifications des éléments sont visibles par l’appelant.
- `const` dans un paramètre tableau indique que la fonction ne modifie pas les éléments.
- Un tri par insertion est simple, en place et quadratique au pire 0(n²); un tri par fusion est en `O(n log n)` et utilise `O(n)` mémoire auxiliaire.
- Une chaîne C est un tableau de caractères terminé par `\0`; réserver une case pour ce terminateur.
- Pour une matrice passée à une fonction, toutes les dimensions sauf la première doivent être spécifiées dans le paramètre.
