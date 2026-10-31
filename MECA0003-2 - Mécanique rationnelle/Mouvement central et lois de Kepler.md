---
tags:
  - mécanique-rationnelle
  - force-centrale
  - kepler
---

# Mouvement central et lois de Kepler

## 1. Définition

Une force centrale est de la forme :

\[
\mathbf F=f(r)\mathbf e_r
=f(r)\frac{\mathbf s}{r}.
\]

Elle est toujours portée par la droite \(O P\).

## 2. Mouvement plan

Le moment de la force en \(O\) est nul :

\[
\mathbf s\wedge\mathbf F=\mathbf0.
\]

Donc :

\[
\dot{\mathbf H}_O=\mathbf0,
\qquad
\mathbf H_O=m\mathbf s\wedge\dot{\mathbf s}=\mathbf h.
\]

Le vecteur \(\mathbf h\) est constant. La trajectoire reste dans le plan perpendiculaire à \(\mathbf h\), contenant \(\mathbf s(0)\) et \(\dot{\mathbf s}(0)\).

## 3. Coordonnées polaires

\[
\mathbf s=r\mathbf e_r,
\]

\[
\dot{\mathbf s}=\dot r\mathbf e_r+r\dot\theta\mathbf e_\theta,
\]

\[
\ddot{\mathbf s}
=(\ddot r-r\dot\theta^2)\mathbf e_r
+(2\dot r\dot\theta+r\ddot\theta)\mathbf e_\theta.
\]

La projection tangentielle donne :

\[
m(r\ddot\theta+2\dot r\dot\theta)=0
\quad\Longrightarrow\quad
\frac d{dt}(mr^2\dot\theta)=0.
\]

Ainsi :

\[
\boxed{h=mr^2\dot\theta=\text{constante}}.
\]

## 4. Loi des aires

L'aire balayée pendant \(dt\) est :

\[
dA=\frac12r^2d\theta.
\]

Donc :

\[
\frac{dA}{dt}=\frac12r^2\dot\theta
=\frac h{2m}
=\text{constante}.
\]

Le rayon vecteur balaie des aires égales pendant des temps égaux.

## 5. Gravitation newtonienne

Pour une attraction gravitationnelle :

\[
\mathbf F=-\frac{\mu m}{r^2}\mathbf e_r,
\qquad
V(r)=-\frac{\mu m}{r}.
\]

L'énergie est :

\[
E=\frac12m\dot r^2+\frac{h^2}{2mr^2}-\frac{\mu m}{r}.
\]

Selon \(E\), les trajectoires sont des coniques :

- \(E<0\) : orbite liée, ellipse ;
- \(E=0\) : parabole limite ;
- \(E>0\) : hyperbole.

## 6. Lois de Kepler

1. Les planètes décrivent des ellipses dont le Soleil occupe un foyer.
2. Le rayon vecteur balaie des aires égales pendant des temps égaux.
3. Le carré de la période est proportionnel au cube du demi-grand axe :

\[
T^2\propto a^3.
\]

Ces lois découlent du caractère central de la gravitation et de la conservation du moment cinétique et de l'énergie.
