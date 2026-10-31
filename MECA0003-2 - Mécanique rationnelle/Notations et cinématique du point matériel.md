---
tags:
  - mécanique-rationnelle
  - cinématique
  - notation
---

# Notations et cinématique du point matériel

## Grandeurs fondamentales

\[
\mathbf s(t)=\overrightarrow{OP}(t),\qquad
\dot{\mathbf s}(t)=\mathbf v(t),\qquad
\ddot{\mathbf s}(t)=\mathbf a(t).
\]

La dérivation est effectuée dans le repère où le mouvement est observé. En cartésien :

\[
\mathbf s=x\mathbf e_x+y\mathbf e_y+z\mathbf e_z,
\]

\[
\dot{\mathbf s}=\dot x\mathbf e_x+\dot y\mathbf e_y+\dot z\mathbf e_z,
\qquad
\ddot{\mathbf s}=\ddot x\mathbf e_x+\ddot y\mathbf e_y+\ddot z\mathbf e_z.
\]

## Coordonnées polaires

La base \((\mathbf e_r,\mathbf e_\theta)\) tourne avec le point :

\[
\dot{\mathbf e}_r=\dot\theta\mathbf e_\theta,
\qquad
\dot{\mathbf e}_\theta=-\dot\theta\mathbf e_r.
\]

Donc :

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

Le terme \(-r\dot\theta^2\mathbf e_r\) est centripète ; le terme \(2\dot r\dot\theta\mathbf e_\theta\) est souvent appelé terme de Coriolis dans cette décomposition.

## Coordonnées cylindriques

\[
\mathbf s=r\mathbf e_r+z\mathbf e_z,
\]

\[
\dot{\mathbf s}
=\dot r\mathbf e_r+r\dot\theta\mathbf e_\theta+\dot z\mathbf e_z,
\]

\[
\ddot{\mathbf s}
=(\ddot r-r\dot\theta^2)\mathbf e_r
+(2\dot r\dot\theta+r\ddot\theta)\mathbf e_\theta
+\ddot z\mathbf e_z.
\]

## Base de Frenet

Pour une trajectoire paramétrée par l'abscisse curviligne \(s\) :

\[
\mathbf v=v\mathbf e_t,
\qquad
\mathbf a=\dot v\mathbf e_t+\frac{v^2}{R}\mathbf e_n.
\]

La composante tangentielle modifie la norme de la vitesse ; la composante normale modifie sa direction. \(R\) est le rayon de courbure.

## Vecteur de Poisson

Pour une base qui tourne avec le vecteur de rotation \(\boldsymbol\omega\) :

\[
\left(\frac{d\mathbf u}{dt}\right)_{\mathrm{fixe}}
=\left(\frac{d\mathbf u}{dt}\right)_{\mathrm{mobile}}
+\boldsymbol\omega\wedge\mathbf u.
\]

En particulier, pour une rotation plane autour de \(\mathbf e_z\) :

\[
\boldsymbol\omega=\dot\theta\mathbf e_z,
\qquad
\dot{\mathbf e}_r=\boldsymbol\omega\wedge\mathbf e_r.
\]

## Changement de variable

Si \(q=q(t)\) :

\[
\frac d{dt}=\dot q\frac d{dq}.
\]

Par exemple :

\[
\ddot q=\dot q\frac{d\dot q}{dq}.
\]

Cette relation est utile lorsque l'équation ne dépend pas explicitement du temps.
