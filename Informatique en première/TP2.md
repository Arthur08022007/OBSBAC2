Rappel à présenter avant ce TP : [[Rappel théorique]].

Exercices 1 à 3 de [[Chapitre2_exo.pdf]]. Pour l'exercice 1, `x`, `y` et `z` sont des entiers valant 0 avant chaque instruction.

## Exercice 1

|  | `x` | `y` | `z` |
| --- | --- | --- | --- |
| (a) | 1 | −1 | −1 |
| (b) | 1 | 0 | −2 |
| (c) | 1 | 1 | 1 |
| (d) | 1 | 1 | 1 |
| (e) | 1 | 0 | 0 |

- (a) `z = x++ + --y;` — `x++` vaut 0, puis `x` passe à 1. `--y` fait passer `y` à −1 et vaut −1. La somme vaut −1.
- (b) `z -= x++ && y++ ? 1 : 2;` — `x++` vaut 0, donc `&&` n'évalue pas `y++`. La condition est fausse : on soustrait 2 à `z`.
- (c) `z += ++x && ++y ? 1 : 2;` — `++x` vaut 1, donc `++y` est évalué et vaut 1. La condition est vraie : on ajoute 1 à `z`.
- (d) `z = x > 0 || !++y ? x++ : ++x;` — `x > 0` est faux, donc `++y` est évalué. `y` passe à 1 et `!++y` vaut 0. La condition est fausse : on exécute `++x`, qui vaut 1.
- (e) `z = (x++, x > 0) ? !x : 1 - !x;` — la virgule exécute `x++`, puis teste `x > 0`. Le test est vrai, donc `z` reçoit `!x`, soit 0.

## Exercice 2

(a)

```c
i = 0;
while (i < 1000) {
    j += i;
    i += 10;
}
```

(b) Le corps d'un `do ... while` s'exécute une fois avant le test.

```c
i = j = 0;
j += i;
i += 2;
while (j < k) {
    j += i;
    i += 2;
}
```

(c) `continue` saute `j += i`, mais le `i++` du `for` a quand même lieu.

```c
i = 0;
j = 0;
while (i < 1000) {
    if (!(f(i) > f(j)))
        j += i;
    i++;
}
```

(d)

```c
while (1)
    ;
```

## Exercice 3

(a)

```c
for (i = 2; i < 100000; i *= 2)
    j += i;
```

(b)

```c
for (p = premier(); !est_dernier(p); p = suivant(p))
    traiter(p);
```

(c)

```c
for (; attendre();)
    ;
```

(d) `j >= k` est testé après le corps. Ce test reste donc un `if`, pas la condition du `for`.

```c
for (i = 0, j = 0;;) {
    j += i++;
    if (j >= k)
        break;
}
```

# Ex4
## Ex1

```c
#include <stdio.h>
#include <math.h>

  

int main() {
    double a, b, c, delta;
    double x1, x2;
    double partieReelle, partieImaginaire;

    printf("Entrez a : ");
    scanf("%lf", &a);
  
    printf("Entrez b : ");
    scanf("%lf", &b);
  
    printf("Entrez c : ");
    scanf("%lf", &c);
    
    if (a == 0) {
        printf("Ce n'est pas une equation du second degre.\n");
        return 0;
    }
  
    delta = b * b - 4 * a * c;
  
    if (delta > 0) {
        x1 = (-b - sqrt(delta)) / (2 * a);
        x2 = (-b + sqrt(delta)) / (2 * a);
  
        printf("\nDeux solutions reelles distinctes :\n");
        printf("x1 = %.2lf\n", x1);
        printf("x2 = %.2lf\n", x2);
    }
    else if (delta == 0) {
        x1 = -b / (2 * a);
  
        printf("\nUne solution reelle double :\n");
        printf("x = %.2lf\n", x1);
    }
    else {
        partieReelle = -b / (2 * a);
        partieImaginaire = sqrt(-delta) / (2 * a);
  
        printf("\nDeux solutions complexes conjuguees :\n");
        printf("x1 = %.2lf - %.2lfi\n", partieReelle, partieImaginaire);
        printf("x2 = %.2lf + %.2lfi\n", partieReelle, partieImaginaire);
    }
    return 0;
}
```

## Ex2

```c
#include <stdio.h>
  
int main(){
    int n, k;
    printf("Entrez deux entiers: ");
    scanf("%d %d", &n, &k);
    int result = 1;
    for (;n-k>0;n-=k){
        result *= n;
    }
    printf("Le résultat est: %d\n", result);
    return 0;
}
```
## Ex4

```c
#include <stdio.h>
void main (){
    long long n;
    
    printf("Entrez un entier : ");
    scanf("%lld", &n);
    
    if (n<2){
        printf("%lld n'est pas premier\n", n);
        return;
    }
    if (n==2){
        printf("%lld est premier\n", n);
        return;
    }
    for (long long i=3; i*i <=n; i+=2){
        if (n%i==0){
            printf("%lld n'est pas premier\n", n);
            printf("Il est divisible par %lld\n", i);
            return;
        }
    }
    printf("%lld est premier\n", n);
    return;
}
```

## Ex5

```c
int main() {
    double n;
    printf("Entrez un entier : ");
    scanf("%lf", &n);
    int n_copy = n;
  
    int i=0;
    while (n>=2){
        i++;
        n=n/2;
    }
    printf("La partie entière du logarithme en base 2 de %d est %d\n", n_copy, i);
    return 0;
}
```
