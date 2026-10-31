---
tags:
  - mécanique-rationnelle
  - système
  - centre-d-inertie
---

# Système de points matériels

On considère \(N\) points \(P_i\), de masses \(m_i\), de positions \(\mathbf{s}_i\), de vitesses \(\dot{\mathbf{s}}_i\) et de forces extérieures résultantes \(\mathbf F_i\).

## 1. Grandeurs résultantes

### Masse totale

\[
m=\sum_{i=1}^{N}m_i.
\]

### Moment statique

\[
\mathbf Q_O=\sum_{i=1}^{N}m_i\mathbf s_i.
\]

Le centre d'inertie \(C\) est défini par :

\[
\boxed{\mathbf Q_O=m\mathbf c},
\qquad
\mathbf c=\frac1m\sum_{i=1}^{N}m_i\mathbf s_i.
\]

Pour une distribution uniforme, \(C\) coïncide avec le centre géométrique. Pour un système discret, il est plus proche des masses les plus importantes.

### Quantité de mouvement

\[
\mathbf N_O=\sum_{i=1}^{N}m_i\dot{\mathbf s}_i.
\]

Si la masse totale est constante :

\[
\boxed{\mathbf N_O=m\dot{\mathbf c}}.
\]

### Moment cinétique

\[
\mathbf H_O=\sum_{i=1}^{N}m_i\mathbf s_i\wedge\dot{\mathbf s}_i.
\]

Il décrit la rotation globale du système autour de \(O\).

### Énergie cinétique

\[
T_O=\frac12\sum_{i=1}^{N}m_i\dot{\mathbf s}_i\cdot\dot{\mathbf s}_i.
\]

### Grandeurs dynamiques

Avec \(\mathbf G_{\mathrm{ext}}\) la résultante des forces extérieures et \(\mathbf M_{O,\mathrm{ext}}\) leur moment en \(O\) :

\[
\mathbf G_{\mathrm{ext}}=\sum_i\mathbf F_i,
\qquad
\mathbf M_{O,\mathrm{ext}}=\sum_i\mathbf s_i\wedge\mathbf F_i.
\]

La puissance totale vaut :

\[
P_O=\sum_i\dot{\mathbf s}_i\cdot\mathbf F_i.
\]

## 2. Théorème de la quantité de mouvement

Dans un repère inertiel :

\[
\boxed{\dot{\mathbf N}_O=\mathbf G_{\mathrm{ext}}}.
\]

Les forces internes s'annulent deux à deux dans la somme des forces grâce à l'action-réaction.

En utilisant le centre d'inertie :

\[
\boxed{m\ddot{\mathbf c}=\mathbf G_{\mathrm{ext}}}.
\]

Le centre d'inertie se comporte donc comme un point matériel de masse \(m\), soumis à la résultante extérieure.

### Conservation

Si \(\mathbf G_{\mathrm{ext}}=\mathbf0\), alors :

\[
\mathbf N_O=\text{constante},
\qquad
\dot{\mathbf c}=\text{constante}.
\]

Le centre d'inertie est en mouvement rectiligne uniforme.

## 3. Théorème du moment cinétique

Pour un point \(O\) fixe dans un repère inertiel :

\[
\boxed{\dot{\mathbf H}_O=\mathbf M_{O,\mathrm{ext}}}.
\]

Si le moment extérieur est nul :

\[
\mathbf H_O=\text{constante}.
\]

### Mouvement sous force centrale

Si \(\mathbf F=f(s)\mathbf e_r\), alors \(\mathbf F\) est parallèle à \(\mathbf s\), donc :

\[
\mathbf s\wedge\mathbf F=\mathbf0.
\]

Le moment cinétique est conservé :

\[
\mathbf H_O=m\mathbf s\wedge\dot{\mathbf s}
=\text{constante}.
\]

La trajectoire reste dans le plan orthogonal à \(\mathbf H_O\) et contenant les conditions initiales. Voir [[Mouvement central et lois de Kepler]].

## 4. Théorème de l'énergie cinétique

\[
\boxed{\dot T_O=P_O}.
\]

Les puissances des forces internes ne doivent pas être supprimées automatiquement : elles peuvent modifier l'énergie cinétique, même si les forces internes disparaissent de la quantité de mouvement.

Une force conservative dérive d'un potentiel \(V\) :

\[
\mathbf F=-\nabla V.
\]

Pour un système conservatif :

\[
\boxed{T+V=E=\text{constante}}.
\]

Une force de liaison normale au mouvement peut avoir une puissance nulle sans être conservative. Cette distinction est importante : **ne pas travailler** signifie \(P=0\), tandis qu'être **conservative** signifie dériver d'un potentiel.

## 5. Décomposition autour du centre d'inertie

En posant :

\[
\mathbf s_i=\mathbf c+\boldsymbol\rho_i,
\qquad
\sum_i m_i\boldsymbol\rho_i=\mathbf0,
\]

on sépare le mouvement de translation du centre d'inertie et le mouvement relatif des points :

\[
T_O=\frac12m\dot{\mathbf c}^{\,2}
+\frac12\sum_i m_i\dot{\boldsymbol\rho}_i^{\,2}.
\]

Cette décomposition permet de distinguer l'énergie de translation de l'énergie interne.

## 6. Système à masse variable

Pour un système dont la masse varie :

\[
\boxed{m(t)\ddot{\mathbf s}=\mathbf G+\mathbf P},
\]

où \(\mathbf s\) est la position du centre d'inertie, \(\mathbf G\) la résultante des forces extérieures et \(\mathbf P\) la poussée due au transport de masse.

On note \(\mathbf w\) la vitesse relative de la matière par rapport au système, mesurée avant absorption ou après éjection :

\[
\mathbf P=\mathbf w\,\frac{dm}{dt}.
\]

- absorption : \(dm/dt>0\) ;
- éjection : \(dm/dt<0\).

La vitesse absolue de la matière vérifie :

\[
\mathbf v_a=\dot{\mathbf s}+\mathbf w.
\]

Voir [[Système à masse variable]] pour la convention de signe et la méthode de résolution.
