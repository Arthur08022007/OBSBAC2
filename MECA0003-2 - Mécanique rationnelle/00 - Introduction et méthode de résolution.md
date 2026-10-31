---
tags:
  - mécanique-rationnelle
  - méthode
---

# Introduction et méthode de résolution

## 1. Modèles mécaniques

La mécanique rationnelle décrit le mouvement de systèmes matériels à partir de modèles idéalisés. Le modèle utilisé conditionne les équations disponibles.

### Point matériel

Un point matériel est un objet dont les dimensions sont négligeables devant les longueurs caractéristiques du mouvement. Sa rotation propre n'est pas étudiée. Le système est alors décrit par un seul vecteur position :

$$
\mathbf{s}(t)=\overrightarrow{OP}(t)
$$

Ce modèle est adapté à un projectile, une bille dont la rotation n'intervient pas, ou un satellite assimilé à un point.

### Système de points matériels

Un système comporte $N$ points $P_i$, de masses $m_i$ et de positions $\mathbf{s}_i$. Les lois de Newton sont écrites pour chaque point, puis additionnées. Cette approche fait apparaître le centre d'inertie et les grandeurs résultantes.

## 2. Référentiel et repère

Un référentiel est le système physique par rapport auquel le mouvement est observé. Un repère est la base mathématique utilisée pour exprimer les vecteurs.

Les théorèmes usuels sont écrits dans un **repère inertiel** (ou galiléen). Dans ce repère, un point isolé est au repos ou en mouvement rectiligne uniforme :

$$
\mathbf{F}=\mathbf{0}\quad\Longrightarrow\quad\ddot{\mathbf{s}}=\mathbf{0}.
$$

Pour les exercices proches de la surface terrestre, on assimile généralement le référentiel terrestre à un repère inertiel.

## 3. Méthode générale

### Étape 1 — Définir le système

Préciser le point matériel ou l'ensemble de points étudié. Une même situation peut demander plusieurs systèmes différents : un mobile seul, le mobile et son support, ou l'ensemble mobile–ressort.

### Étape 2 — Choisir le repère

Le repère doit exploiter les symétries et les contraintes :

- cartésien $(\mathbf e_x,\mathbf e_y,\mathbf e_z)$ pour une force constante ou un mouvement rectiligne ;
- polaire $(\mathbf e_r,\mathbf e_\theta)$ pour un mouvement plan autour d'un point ;
- cylindrique $(\mathbf e_r,\mathbf e_\theta,\mathbf e_z)$ pour un mouvement sur une surface de révolution ;
- base de Frenet $(\mathbf e_t,\mathbf e_n,\mathbf e_b)$ pour une trajectoire connue.

Voir [[Notations et cinématique du point matériel]].

### Étape 3 — Faire l'inventaire des forces

Séparer :

1. les forces appliquées, qui produisent le mouvement ;
2. les forces de liaison, imposées par une contrainte géométrique ;
3. les forces internes, seulement pour un système comportant plusieurs points.

Voir [[Forces, liaisons et projections]].

### Étape 4 — Écrire la loi fondamentale

Pour un point matériel de masse constante :

$$
m\ddot{\mathbf{s}}=\sum_i\mathbf F_i.
$$

Il faut ensuite projeter dans la base choisie. Une équation vectorielle équivaut à trois équations scalaires en 3D, mais certaines projections peuvent éliminer directement une réaction de liaison.

### Étape 5 — Exploiter les intégrales premières

Une intégrale première est une relation contenant moins de dérivées que l'équation initiale. On l'obtient souvent en :

- projetant Newton selon une direction judicieuse ;
- multipliant scalairement par $\dot{\mathbf{s}}$ ;
- multipliant vectoriellement par $\mathbf{s}$ ;
- identifiant une dérivée totale.

Une fois obtenue, il faut lui donner une interprétation physique et déterminer sa constante avec les conditions initiales.

### Étape 6 — Utiliser les conditions initiales et les contraintes

Les conditions initiales déterminent les constantes d'intégration :

$$
\mathbf{s}(0)=\mathbf{s}_0,\qquad
\dot{\mathbf{s}}(0)=\mathbf v_0.
$$

Les contraintes complètent le problème :

- courbe : une coordonnée indépendante en mouvement plan ;
- surface : deux coordonnées indépendantes ;
- liaison rigide ou corde : relation géométrique entre les coordonnées.

### Étape 7 — Vérifier

Contrôler systématiquement :

- les dimensions physiques ;
- les signes et orientations ;
- les cas limites ($t=0$, frottement nul, gravité nulle, etc.) ;
- la compatibilité avec la liaison ;
- le caractère réaliste de la réaction calculée.

## 4. Fiche réflexe

> **Système → repère → forces → Newton → projection/intégrale première → conditions initiales → interprétation.**

Pour une procédure détaillée selon le type d'exercice, consulter [[01 - Dynamique du point matériel]] et [[03 - Analyse du mouvement du point matériel]].
