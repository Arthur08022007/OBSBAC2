---
tags:
  - mécanique-rationnelle
  - oscillateur
  - frottement
---

# Oscillateurs et frottements

## Oscillateur harmonique

$$
m\ddot x+kx=0,\qquad \omega_0=\sqrt{\frac km}.
$$

$$
x(t)=A\cos(\omega_0t)+B\sin(\omega_0t).
$$

Les constantes suivent de :

$$
A=x(0),\qquad
B=\frac{\dot x(0)}{\omega_0}.
$$

L'énergie mécanique :

$$
E=\frac12m\dot x^2+\frac12kx^2
$$

est constante.

## Amortissement fluide

$$
m\ddot x+c\dot x+kx=0,
\qquad
\zeta=\frac{c}{2\sqrt{km}}.
$$

La classification est :

| Régime | Condition | Comportement |
|---|---:|---|
| Sous-critique | $0<\zeta<1$ | oscillations amorties |
| Critique | $\zeta=1$ | retour sans oscillation, le plus rapide |
| Sur-critique | $\zeta>1$ | retour sans oscillation, plus lent |

L'amortissement fluide dissipe de l'énergie :

$$
P_f=\mathbf F_f\cdot\dot{\mathbf s}
=-c\|\dot{\mathbf s}\|^2\leq0.
$$

## Frottement sec

Le frottement sec dépend du sens de la vitesse :

$$
\mathbf T=-\mu|N|\operatorname{sgn}(\dot x)\mathbf e_x.
$$

La résolution est donc faite par phases :

1. supposer le signe de $\dot x$ ;
2. remplacer le frottement par une force constante sur la phase ;
3. résoudre l'équation différentielle ;
4. calculer $\dot x(t)$ ;
5. déterminer l'instant où $\dot x=0$ ;
6. vérifier que le ressort peut vaincre le frottement au redémarrage ;
7. passer à la phase suivante ou conclure à l'arrêt.

La condition de redémarrage s'écrit qualitativement :

$$
|F_r|>\mu|N|.
$$

Le frottement sec ne doit pas être traité comme un amortissement linéaire : sa norme ne dépend pas continûment de la vitesse.
