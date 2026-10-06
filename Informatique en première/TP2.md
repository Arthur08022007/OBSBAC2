Rappel à présenter avant ce TP : [[Rappel théorique]].

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
