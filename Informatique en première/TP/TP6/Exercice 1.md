## Enoncé
(a) Écrire une fonction C prenant en arguments deux entiers strictement
positifs n et f , et calculant la multiplicité du facteur f dans n, c’est-à-
dire le plus grand nombre entier m tel que f m divise n. Par exemple, si
n = 324 et f = 9, on a m = 2 car 324 = 92.4.
(b) Par la méthode des invariants, démontrer que la valeur retournée par
cette fonction est correcte

## Résolution a)
```c
unsigned multiplicite_facteur(unsigned n, unsigned f){
	unsigned m;
	for (m = 0; !(n % f); m++)
		n /= f;
	return m;
}
```

## Résolution b)

On ne demande pas de prouver que la fonction termine toujours son
exécution, mais de démontrer que lorsque cette exécution se termine, la
valeur retournée est correcte. Cela revient à prouver le triplet
{n = n0 > 0, f > 0}
for (m = 0; !(n % f); m++)
n /= f;
2
{m = multiplicité de f dans n0},
où n0 dénote la valeur initiale de n. En développant la boucle for, cela
équivaut à démontrer
{n = n0 > 0, f > 0, m = 0}
while (!(n % f))
{
n /= f;
m++;
}
{m = multiplicité de f dans n0}
Cherchons un invariant de boucle I. Celui-ci doit satisfaire les trois
propriétés suivantes :
— I doit être impliqué par la précondition (n = n0 > 0 et f > 0 et
m = 0).
— Si I est vrai avant une itération de la boucle while, alors I doit
également être vrai à la fin de cette itération.
— Après la dernière itération de la boucle, I doit impliquer la postcon-
dition (m = multiplicité de f dans n0).
Ces trois propriétés sont vraies pour l’invariant
I : n > 0 et f > 0 et n0 = n.fm.
En effet :
— Initialement, on a (n = n0 > 0 et f > 0 et m = 0) =⇒ I.
— D’une itération à l’autre de la boucle, on a le triplet
{I, n est divisible par f}
n /= f;
m++;
{I},
qui est bien valide. En effet, si n′ et m′ dénotent respectivement les
valeurs de n et m après l’exécution du fragment de code, on a
n′ = n
f et m′ = m + 1,
3
donc
(I et n est divisible par f)
implique
(n′ > 0 et f > 0 et n0 = n.fm = n′.fm′
).
— En sortie de boucle, on a
(I et n n’est pas divisible par f)
qui implique bien
(m = multiplicité de f dans n0),
car si n0 = n.fm et n n’est pas divisible par f, alors m est la multipli-
cité de f dans n0 (par définition de cette multiplicité).