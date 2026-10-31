---
tags:
  - mécanique-rationnelle
  - masse-variable
  - propulsion
---

# Système à masse variable

## Équation de base

Lorsque la masse du système étudié varie :

\[
\boxed{m(t)\ddot{\mathbf s}=\mathbf G+\mathbf P}.
\]

\(\mathbf s\) est la position du centre d'inertie du système, \(\mathbf G\) la résultante des forces extérieures et \(\mathbf P\) la poussée résultant du flux de masse.

## Convention sur la vitesse relative

On note \(\mathbf w\) la vitesse de la matière par rapport au système :

- pour une absorption, elle est mesurée juste avant l'entrée ;
- pour une éjection, elle est mesurée juste après la sortie.

La vitesse absolue de la matière est :

\[
\mathbf v_a=\dot{\mathbf s}+\mathbf w.
\]

La poussée s'écrit :

\[
\mathbf P=\mathbf w\frac{dm}{dt}.
\]

La convention \(dm/dt<0\) en cas d'éjection rend naturellement le signe de la poussée dépendant de l'orientation de \(\mathbf w\).

## Méthode de résolution

1. Déterminer \(m(t)\) et \(dm/dt\).
2. Définir précisément le système matériel retenu.
3. Identifier \(\mathbf G\).
4. Définir \(\mathbf w\) avec la convention entrée/sortie.
5. Écrire \(m(t)\ddot{\mathbf s}=\mathbf G+\mathbf w\,dm/dt\).
6. Projeter selon les axes utiles.
7. Résoudre avec les conditions initiales.

## Pièges fréquents

- utiliser la vitesse absolue à la place de la vitesse relative ;
- oublier que \(dm/dt<0\) lors d'une éjection ;
- modifier le système étudié en cours de calcul ;
- inclure deux fois l'effet du flux de masse comme force extérieure.

La masse variable est une application directe du théorème de la quantité de mouvement, mais elle exige une convention de signe cohérente du début à la fin.
