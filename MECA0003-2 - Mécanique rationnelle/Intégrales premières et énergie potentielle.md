---
tags:
  - mécanique-rationnelle
  - énergie
  - potentiel
---

# Intégrales premières et énergie potentielle

## Définition

Une intégrale première est une relation constante le long du mouvement. Elle provient d'une symétrie, d'une projection ou d'une dérivée totale.

## Énergie

Pour un point matériel :

$$
T=\frac12m\|\dot{\mathbf s}\|^2.
$$

Si $\mathbf F=-\nabla V$, alors :

$$
\frac d{dt}(T+V)=0,
\qquad
T+V=E.
$$

Exemples :

- pesanteur uniforme : $V=mgz$ si $z$ est orienté vers le haut ;
- ressort : $V=\frac12kx^2$ ;
- gravitation centrale : $V=-\frac{\mu m}{r}$.

## Potentiel effectif

Pour un mouvement central, le moment cinétique impose :

$$
h=mr^2\dot\theta.
$$

L'énergie s'écrit alors :

$$
E=\frac12m\dot r^2+
\underbrace{\frac{h^2}{2mr^2}+V(r)}_{V_{\mathrm{eff}}(r)}.
$$

Le terme $h^2/(2mr^2)$ est le potentiel centrifuge. Il permet d'analyser le mouvement radial comme un mouvement à un degré de liberté.

## Lecture graphique

$$
\frac12m\dot r^2=E-V_{\mathrm{eff}}(r)\geq0.
$$

Les régions accessibles satisfont $E\geq V_{\mathrm{eff}}$. Les points de retournement sont les intersections $E=V_{\mathrm{eff}}$. Une orbite circulaire correspond à :

$$
V_{\mathrm{eff}}'(r_*)=0.
$$

Elle est stable si $V_{\mathrm{eff}}''(r_*)>0$.
