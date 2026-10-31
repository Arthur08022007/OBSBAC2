---
tags:
  - mécanique-rationnelle
  - théorèmes
  - système
---

# Théorèmes généraux et grandeurs résultantes

## Tableau de correspondance

| Grandeur | Définition | Évolution |
|---|---|---|
| Masse | \(m=\sum_i m_i\) | constante si le système est fermé |
| Moment statique | \(\mathbf Q_O=\sum_i m_i\mathbf s_i\) | définit \(\mathbf c\) |
| Quantité de mouvement | \(\mathbf N_O=\sum_i m_i\dot{\mathbf s}_i\) | \(\dot{\mathbf N}_O=\mathbf G_{\mathrm{ext}}\) |
| Moment cinétique | \(\mathbf H_O=\sum_i m_i\mathbf s_i\wedge\dot{\mathbf s}_i\) | \(\dot{\mathbf H}_O=\mathbf M_{O,\mathrm{ext}}\) |
| Énergie cinétique | \(T_O=\frac12\sum_i m_i\dot{\mathbf s}_i^2\) | \(\dot T_O=P_O\) |

## Choisir le bon théorème

- translation globale ou centre d'inertie : quantité de mouvement ;
- rotation autour d'un point ou d'un axe : moment cinétique ;
- vitesse, hauteur, ressort, trajectoire accessible : énergie cinétique ;
- force centrale : moment cinétique puis énergie ;
- masse entrante ou sortante : équation de masse variable.

## Attention aux forces internes

Les forces internes s'annulent dans \(\mathbf G_{\mathrm{ext}}\), mais leur puissance peut être non nulle. Il faut donc :

- exclure les forces internes du théorème de la quantité de mouvement ;
- les conserver dans le bilan énergétique si elles travaillent ;
- vérifier si le système choisi est fermé.

## Centre d'inertie

\[
\mathbf c=\frac1m\sum_i m_i\mathbf s_i,
\qquad
\mathbf N_O=m\dot{\mathbf c}.
\]

Le centre d'inertie est le point naturel pour étudier la translation du système. Les forces internes ne peuvent pas modifier son mouvement.
