---
tags:
  - mécanique-rationnelle
  - forces
  - liaisons
---

# Forces, liaisons et projections

## Forces appliquées et forces de liaison

Une force appliquée est imposée par l'interaction physique étudiée : poids, ressort, frottement, force électrique ou magnétique.

Une force de liaison garantit une contrainte géométrique : réaction d'un support, tension d'une corde, réaction normale d'une courbe ou d'une surface.

Le but n'est pas toujours de calculer toutes les forces. Pour obtenir le mouvement, on cherche souvent à éliminer les réactions de liaison par une projection adaptée.

## Décomposition d'une réaction

Pour un mouvement sur une courbe plane :

\[
\mathbf R=R_\nu\mathbf e_\nu+R_\beta\mathbf e_\beta.
\]

La réaction normale est orthogonale à la vitesse si la liaison est idéale et sans frottement :

\[
\mathbf R\cdot\dot{\mathbf s}=0.
\]

Elle ne travaille donc pas. Cela ne signifie pas qu'elle est conservative.

## Projections utiles

### Projection sur la vitesse

Multiplier Newton par \(\dot{\mathbf s}\) donne :

\[
m\dot{\mathbf s}\cdot\ddot{\mathbf s}
=\dot{\mathbf s}\cdot\sum_i\mathbf F_i.
\]

Les forces perpendiculaires au mouvement disparaissent. On obtient souvent l'énergie cinétique ou une intégrale première.

### Produit vectoriel par la position

Multiplier Newton par \(\mathbf s\) :

\[
m\mathbf s\wedge\ddot{\mathbf s}
=\mathbf s\wedge\sum_i\mathbf F_i.
\]

Les forces passant par \(O\) ont un moment nul en \(O\). Cette projection est le réflexe pour une force centrale ou un mouvement à symétrie de rotation.

### Projection tangentielle

Pour une trajectoire connue, la projection selon \(\mathbf e_t\) élimine les réactions normales :

\[
m\mathbf a\cdot\mathbf e_t
=\sum_i\mathbf F_i\cdot\mathbf e_t.
\]

La projection normale permet ensuite de déterminer la réaction ou de vérifier le contact.

## Ordre de résolution recommandé

1. Dessiner le diagramme des forces.
2. Identifier les directions de liaison.
3. Choisir la projection qui annule les réactions inconnues.
4. Résoudre l'équation tangentielle.
5. Revenir aux projections normales seulement si une réaction est demandée.

Pages liées : [[01 - Dynamique du point matériel]], [[03 - Analyse du mouvement du point matériel]], [[Intégrales premières et énergie potentielle]].
