---
tags:
  - mécanique-rationnelle
  - analyse-du-mouvement
  - stabilité
---

# Analyse du mouvement du point matériel

Cette partie vise à réduire l'équation différentielle et à comprendre qualitativement le mouvement avant de chercher une solution explicite.

## 1. Variables adimensionnelles

Une variable adimensionnelle est obtenue en divisant une grandeur par une échelle caractéristique. Par exemple :

\[
\bar r=\frac r{r_0},\qquad
\bar t=\frac t{t_0}.
\]

Le choix de \(r_0\), \(t_0\) et d'une vitesse caractéristique permet de faire apparaître les paramètres sans dimension qui gouvernent le problème. Cette étape facilite la comparaison entre régimes et la détection d'ordres de grandeur.

## 2. Intégrales premières

### Par projection sur la vitesse

À partir de Newton :

\[
m\ddot{\mathbf s}=\mathbf F,
\]

le produit scalaire par \(\dot{\mathbf s}\) donne :

\[
m\dot{\mathbf s}\cdot\ddot{\mathbf s}
=\dot{\mathbf s}\cdot\mathbf F.
\]

Or :

\[
\dot{\mathbf s}\cdot\ddot{\mathbf s}
=\frac d{dt}\left(\frac12\|\dot{\mathbf s}\|^2\right).
\]

Si \(\mathbf F=-\nabla V\), alors :

\[
\frac d{dt}\left(\frac12m\|\dot{\mathbf s}\|^2+V\right)=0,
\]

donc :

\[
\boxed{\frac12m\|\dot{\mathbf s}\|^2+V=E}.
\]

### Par moment en \(O\)

Le produit vectoriel par \(\mathbf s\) donne :

\[
m\mathbf s\wedge\ddot{\mathbf s}
=\mathbf s\wedge\mathbf F.
\]

Comme :

\[
\mathbf s\wedge\ddot{\mathbf s}
=\frac d{dt}(\mathbf s\wedge\dot{\mathbf s}),
\]

une force centrale implique la conservation de \(\mathbf H_O\).

### Méthode de lecture

Après chaque intégrale première :

1. identifier la grandeur conservée ;
2. déterminer sa constante avec les conditions initiales ;
3. vérifier les unités ;
4. utiliser la relation pour réduire le nombre de variables.

## 3. Mouvement sur une courbe de guidage fixe

Une courbe impose généralement une contrainte et laisse un degré de liberté. En mouvement plan, les forces de liaison sont souvent décomposées en :

\[
\mathbf R_\nu=R_\nu\mathbf e_\nu,
\qquad
\mathbf R_\beta=R_\beta\mathbf e_\beta,
\]

où \(\mathbf e_\nu\) est la normale principale dans le plan de la courbe et \(\mathbf e_\beta\) la binormale.

La projection selon la tangente élimine les réactions normales et fournit l'équation du mouvement. La projection normale sert ensuite à calculer la réaction si nécessaire.

Pour une courbe polaire :

\[
\mathbf s=r\mathbf e_r,
\]

\[
\dot{\mathbf s}=\dot r\,\mathbf e_r+r\dot\theta\,\mathbf e_\theta,
\]

\[
\ddot{\mathbf s}
=(\ddot r-r\dot\theta^2)\mathbf e_r
+(2\dot r\dot\theta+r\ddot\theta)\mathbf e_\theta.
\]

## 4. Mouvement sur une surface

Une surface impose une contrainte mais laisse souvent deux degrés de liberté. Il faut donc rechercher deux relations indépendantes, par exemple une intégrale d'énergie et une conservation du moment cinétique.

En coordonnées cylindriques :

\[
\mathbf s=r\mathbf e_r+z\mathbf e_z,
\]

\[
\dot{\mathbf s}
=\dot r\,\mathbf e_r+r\dot\theta\,\mathbf e_\theta+\dot z\,\mathbf e_z,
\]

\[
\ddot{\mathbf s}
=(\ddot r-r\dot\theta^2)\mathbf e_r
+(2\dot r\dot\theta+r\ddot\theta)\mathbf e_\theta
+\ddot z\,\mathbf e_z.
\]

Pour éliminer une réaction normale, projeter selon une direction tangente à la surface ou utiliser la puissance de la réaction si elle est perpendiculaire au mouvement.

## 5. Diagramme de potentiel

Pour un mouvement à un degré de liberté \(q\) :

\[
\frac12m_{\mathrm{eff}}\dot q^{\,2}+V(q)=E.
\]

Le mouvement n'est possible que dans les régions où :

\[
E-V(q)\geq0.
\]

Les points d'arrêt vérifient \(E=V(q)\). Le diagramme \(V(q)\) permet donc de déterminer les zones accessibles, les oscillations et les franchissements de barrière.

## 6. Équilibre et stabilité

Une position \(q_*\) est un équilibre si :

\[
\dot q=0,\qquad \ddot q=0.
\]

Pour un potentiel régulier :

\[
V'(q_*)=0.
\]

La stabilité locale se lit avec :

- \(V''(q_*)>0\) : minimum, équilibre stable ;
- \(V''(q_*)<0\) : maximum, équilibre instable ;
- \(V''(q_*)=0\) : test inconclusif, développer à l'ordre supérieur.

### Perturbations infinitésimales

Poser :

\[
q=q_*+\eta,\qquad |\eta|\ll1.
\]

Linéariser l'équation au premier ordre. Si l'équation obtenue est :

\[
\ddot\eta+\omega^2\eta=0,
\]

la perturbation reste bornée et l'équilibre est stable. Si elle est de la forme :

\[
\ddot\eta-\lambda^2\eta=0,
\]

la perturbation croît exponentiellement et l'équilibre est instable.

## 7. Sensibilité et bifurcation

Un paramètre de contrôle peut modifier le nombre ou la stabilité des équilibres. Une bifurcation apparaît lorsque la structure des solutions stationnaires change lorsque ce paramètre varie.

La méthode consiste à :

1. écrire l'équation d'équilibre ;
2. résoudre en fonction du paramètre ;
3. repérer les valeurs critiques ;
4. étudier la stabilité de chaque branche ;
5. représenter qualitativement le diagramme paramètre–équilibre.

## 8. Force centrale

Pour \(\mathbf F=f(r)\mathbf e_r\) :

1. montrer que \(\mathbf H_O\) est constant ;
2. en déduire que le mouvement est plan ;
3. écrire l'accélération en polaires ;
4. utiliser l'énergie et le moment cinétique ;
5. analyser le potentiel effectif.

Voir [[Mouvement central et lois de Kepler]].
