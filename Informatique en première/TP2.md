## Ex1

```c
int main() {
    double n;
    printf("Entrez un entiiier : ");
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
### Ex2

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

```mermaid
graph TD;
    PC-->GitHub;
    GitHub-->Téléphone;
```
