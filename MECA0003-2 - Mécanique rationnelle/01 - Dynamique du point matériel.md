---
tags:
  - mécanique-rationnelle
  - dynamique
  - point-matériel
---

# Dynamique du point matériel

## 1. Loi fondamentale de Newton

Dans un repère inertiel, pour un point matériel de masse constante $m$ :

$$
\boxed{m\ddot{\mathbf{s}}=\sum_i\mathbf F_i}
$$

avec $\mathbf{s}=\overrightarrow{OP}$, $\dot{\mathbf{s}}=\mathbf v$ et $\ddot{\mathbf{s}}=\mathbf a$.

La loi est vectorielle. Elle doit être projetée dans le repère choisi après avoir exprimé toutes les forces dans la même base.

### Action et réaction

Deux points matériels exercent l'un sur l'autre des forces de même norme, opposées et portées par la droite qui les joint. Dans un système, les forces internes s'annulent dans la résultante, mais elles ne s'annulent pas nécessairement dans l'énergie cinétique.

## 2. Forces usuelles

### Pesanteur

Près de la surface terrestre :

$$
\mathbf F_g=m\mathbf g,\qquad \|\mathbf g\|\simeq 9{,}81\ \mathrm{m\,s^{-2}}.
$$

La force est verticale et dirigée vers le bas. Il faut fixer le sens de $\mathbf e_z$ avant d'écrire son signe.

Dans un champ gravitationnel central :

$$
\widehat{\mathbf F}(\mathbf s)=-\frac{\mu}{s^3}\mathbf s,
\qquad s=\|\mathbf s\|,\quad \mu>0.
$$

La force est dirigée vers le centre $O$.

### Ressort linéaire

Pour un ressort de longueur naturelle $l_0$, de longueur instantanée $l$ et de direction $\mathbf e$ :

$$
\mathbf F_r=-k(l-l_0)\mathbf e,\qquad k>0.
$$

La forme $\mathbf F_r=-k\mathbf s$ est utilisée lorsque $\mathbf s$ mesure directement l'allongement par rapport à la position d'équilibre.

### Ressort de torsion

$$
\mathbf C=-k_\theta(\theta-\theta_0)\mathbf e.
$$

Le couple tend à ramener l'angle vers $\theta_0$.

### Frottement fluide

$$
\mathbf F_f=-c\dot{\mathbf s},\qquad c>0.
$$

La force est opposée à la vitesse. Pour une rotation amortie :

$$
\mathbf C=-c_\theta\dot\theta\,\mathbf e.
$$

Voir [[Oscillateurs et frottements]].

### Frottement sec

En présence d'une réaction normale $N$, le frottement tangent vérifie :

$$
\mathbf T=-\mu |N|\,\operatorname{sgn}(\dot x)\mathbf e_x.
$$

Le modèle est par morceaux : le signe de $\dot x$ doit être connu sur chaque phase.

### Force de Lorentz

Pour une charge $q$ dans un champ électrique $\mathbf E$ et magnétique $\mathbf B$ :

$$
\mathbf F=q(\mathbf E+\dot{\mathbf s}\wedge\mathbf B).
$$

Le champ magnétique ne travaille pas car $\dot{\mathbf s}\cdot(\dot{\mathbf s}\wedge\mathbf B)=0$.

## 3. Chute libre et projectile

Dans le vide, l'équation est :

$$
m\ddot{\mathbf s}=m\mathbf g
\quad\Longrightarrow\quad
\ddot{\mathbf s}=\mathbf g.
$$

Pour $\mathbf g=-g\mathbf e_z$, $\mathbf s(0)=\mathbf s_0$ et $\dot{\mathbf s}(0)=\mathbf v_0$ :

$$
\mathbf s(t)=\mathbf s_0+\mathbf v_0t+\frac12\mathbf gt^2,
\qquad
\dot{\mathbf s}(t)=\mathbf v_0+\mathbf gt.
$$

En coordonnées cartésiennes :

$$
x(t)=x_0+v_{0x}t,\qquad
z(t)=z_0+v_{0z}t-\frac12gt^2.
$$

Pour obtenir la trajectoire, éliminer $t$ entre $x(t)$ et $z(t)$. Pour une hauteur maximale, résoudre $\dot z(t)=0$. Pour le temps de vol, imposer la condition géométrique d'impact, souvent $z(\tau)=0$.

## 4. Chute avec frottement fluide

Avec $\mathbf F_f=-c\dot{\mathbf s}$ :

$$
m\ddot{\mathbf s}+c\dot{\mathbf s}=m\mathbf g.
$$

La solution est la somme d'une solution homogène et d'une solution particulière :

$$
\mathbf s=\mathbf s_h+\mathbf s_p.
$$

La vitesse tend vers la vitesse limite obtenue en annulant l'accélération :

$$
c\mathbf v_\infty=m\mathbf g
\quad\Longrightarrow\quad
\mathbf v_\infty=\frac{m}{c}\mathbf g.
$$

Cette limite est une vérification physique utile : elle doit être atteinte asymptotiquement, sans divergence.

## 5. Oscillateur harmonique

Pour une masse reliée à un ressort, sans amortissement :

$$
m\ddot x+kx=0
\quad\Longrightarrow\quad
\ddot x+\omega_0^2x=0,
\qquad
\omega_0=\sqrt{\frac{k}{m}}.
$$

La solution peut s'écrire :

$$
x(t)=A\cos(\omega_0t)+B\sin(\omega_0t)
=X\cos(\omega_0t-\varphi).
$$

La période et la fréquence sont :

$$
T=\frac{2\pi}{\omega_0},\qquad f=\frac{\omega_0}{2\pi}.
$$

## 6. Oscillateur amorti

Avec un amortisseur fluide :

$$
m\ddot x+c\dot x+kx=0.
$$

On introduit le facteur d'amortissement :

$$
\zeta=\frac{c}{2\sqrt{km}}.
$$

- $0<\zeta<1$ : régime sous-critique, oscillations d'amplitude décroissante ;
- $\zeta=1$ : régime critique, retour sans oscillation le plus rapide ;
- $\zeta>1$ : régime sur-critique, retour sans oscillation plus lent.

Pour chaque régime, les constantes sont obtenues avec $x(0)$ et $\dot x(0)$. Le choix de la solution doit être cohérent avec le signe du discriminant de l'équation caractéristique.

## 7. Procédure pour un exercice de dynamique

1. Isoler le point et dessiner les forces.
2. Choisir les axes selon les forces ou la liaison.
3. Écrire $m\ddot{\mathbf s}=\sum_i\mathbf F_i$.
4. Projeter et identifier les équations différentielles.
5. Résoudre avec les conditions initiales.
6. Calculer les grandeurs demandées : trajectoire, portée, hauteur, période ou réaction.
7. Vérifier les unités et les cas limites.

Pages liées : [[Forces, liaisons et projections]], [[Oscillateurs et frottements]], [[Notations et cinématique du point matériel]].
