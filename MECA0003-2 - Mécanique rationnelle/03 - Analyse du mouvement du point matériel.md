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

$$
\bar r=\frac r{r_0},\qquad
\bar t=\frac t{t_0}.
$$

Le choix de $r_0$, $t_0$ et d'une vitesse caractéristique permet de faire apparaître les paramètres sans dimension qui gouvernent le problème. Cette étape facilite la comparaison entre régimes et la détection d'ordres de grandeur.

## 2. Intégrales premières

### Par projection sur la vitesse

À partir de Newton :

$$
m\ddot{\mathbf s}=\mathbf F,
$$

le produit scalaire par $\dot{\mathbf s}$ donne :

$$
m\dot{\mathbf s}\cdot\ddot{\mathbf s}
=\dot{\mathbf s}\cdot\mathbf F.
$$

Or :

$$
\dot{\mathbf s}\cdot\ddot{\mathbf s}
=\frac d{dt}\left(\frac12\|\dot{\mathbf s}\|^2\right).
$$

Si $\mathbf F=-\nabla V$, alors :

$$
\frac d{dt}\left(\frac12m\|\dot{\mathbf s}\|^2+V\right)=0,
$$

donc :

$$
\boxed{\frac12m\|\dot{\mathbf s}\|^2+V=E}.
$$

### Par moment en $O$

Le produit vectoriel par $\mathbf s$ donne :

$$
m\mathbf s\wedge\ddot{\mathbf s}
=\mathbf s\wedge\mathbf F.
$$

Comme :

$$
\mathbf s\wedge\ddot{\mathbf s}
=\frac d{dt}(\mathbf s\wedge\dot{\mathbf s}),
$$

une force centrale implique la conservation de $\mathbf H_O$.

### Méthode de lecture

Après chaque intégrale première :

1. identifier la grandeur conservée ;
2. déterminer sa constante avec les conditions initiales ;
3. vérifier les unités ;
4. utiliser la relation pour réduire le nombre de variables.

## 3. Mouvement sur une courbe de guidage fixe

Une courbe impose généralement une contrainte et laisse un degré de liberté. En mouvement plan, les forces de liaison sont souvent décomposées en :

$$
\mathbf R_\nu=R_\nu\mathbf e_\nu,
\qquad
\mathbf R_\beta=R_\beta\mathbf e_\beta,
$$

où $\mathbf e_\nu$ est la normale principale dans le plan de la courbe et $\mathbf e_\beta$ la binormale.

La projection selon la tangente élimine les réactions normales et fournit l'équation du mouvement. La projection normale sert ensuite à calculer la réaction si nécessaire.

Pour une courbe polaire :

$$
\mathbf s=r\mathbf e_r,
$$

$$
\dot{\mathbf s}=\dot r\,\mathbf e_r+r\dot\theta\,\mathbf e_\theta,
$$

$$
\ddot{\mathbf s}
=(\ddot r-r\dot\theta^2)\mathbf e_r
+(2\dot r\dot\theta+r\ddot\theta)\mathbf e_\theta.
$$

## 4. Mouvement sur une surface

Une surface impose une contrainte mais laisse souvent deux degrés de liberté. Il faut donc rechercher deux relations indépendantes, par exemple une intégrale d'énergie et une conservation du moment cinétique.

En coordonnées cylindriques :

$$
\mathbf s=r\mathbf e_r+z\mathbf e_z,
$$

$$
\dot{\mathbf s}
=\dot r\,\mathbf e_r+r\dot\theta\,\mathbf e_\theta+\dot z\,\mathbf e_z,
$$

$$
\ddot{\mathbf s}
=(\ddot r-r\dot\theta^2)\mathbf e_r
+(2\dot r\dot\theta+r\ddot\theta)\mathbf e_\theta
+\ddot z\,\mathbf e_z.
$$

Pour éliminer une réaction normale, projeter selon une direction tangente à la surface ou utiliser la puissance de la réaction si elle est perpendiculaire au mouvement.

## 5. Diagramme de potentiel

Pour un mouvement à un degré de liberté $q$ :

$$
\frac12m_{\mathrm{eff}}\dot q^{\,2}+V(q)=E.
$$

Cette relation sépare l'énergie mécanique en deux contributions :

- $V(q)$ est l'énergie potentielle, qui dépend uniquement de la position ;
- $T(q)=\frac12m_{\mathrm{eff}}\dot q^{\,2}$ est l'énergie cinétique ;
- $E$ est l'énergie mécanique totale, constante si le système est conservatif.

On peut isoler la vitesse :

$$
\dot q=\pm\sqrt{\frac{2\bigl(E-V(q)\bigr)}{m_{\mathrm{eff}}}}.
$$

Le signe $+$ correspond au mouvement dans le sens des $q$ croissants et le signe $-$ au mouvement dans l'autre sens. La vitesse est réelle uniquement si :

$$
E-V(q)\geq0.
$$

Sur un diagramme où l'on trace $V(q)$ en fonction de $q$, il suffit donc d'ajouter une droite horizontale d'altitude $E$ :
 
- lorsque $E>V(q)$, la région est accessible et la particule possède une énergie cinétique positive ;
- lorsque $E=V(q)$, la vitesse s'annule : c'est un point d'arrêt ou un point de retournement ;
- lorsque $E<V(q)$, la région est interdite classiquement, car elle demanderait une énergie cinétique négative.

La pente du graphe donne aussi le sens de la force :

$$
F(q)=-\frac{\mathrm dV}{\mathrm dq}.
$$

La particule est donc accélérée vers les valeurs de $q$ où le potentiel diminue. Elle ralentit en montant une pente de potentiel et accélère en la descendant. La vitesse est maximale dans les zones où $V(q)$ est minimal, puisque :

$$
T=E-V(q).
$$

### Lire concrètement un diagramme

Pour analyser un diagramme de potentiel, on peut suivre cette méthode :

1. tracer ou identifier la courbe $V(q)$ ;
2. placer la ligne horizontale correspondant à l'énergie $E$ ;
3. repérer les intersections $E=V(q)$, qui sont les points d'arrêt ;
4. conserver uniquement les intervalles où $V(q)\leq E$ ;
5. déterminer si ces intervalles sont bornés ou non ;
6. repérer les minima et maxima de $V$, car ils indiquent respectivement les équilibres stables et instables.

Un intervalle accessible borné correspond généralement à une oscillation. Un intervalle qui s'étend jusqu'à l'infini correspond à un mouvement d'échappement ou de passage, selon la forme du potentiel. Une barrière de potentiel ne peut être franchie que si l'énergie totale est au moins égale à la hauteur de cette barrière.

### Exemple 1 : oscillateur harmonique

Pour un ressort de raideur $k$ :

$$
V(q)=\frac12kq^2.
$$

La courbe est une parabole dont le minimum est en $q=0$. Pour une énergie $E>0$, les points d'arrêt sont obtenus avec :

$$
\frac12kq^2=E
\quad\Longrightarrow\quad
q_\pm=\pm\sqrt{\frac{2E}{k}}.
$$

La région accessible est donc :

$$
-\sqrt{\frac{2E}{k}}\leq q\leq\sqrt{\frac{2E}{k}}.
$$

Le mouvement est nécessairement borné : la masse oscille entre $q_-$ et $q_+$. Au centre $q=0$, le potentiel est minimal, donc la vitesse est maximale :

$$
\frac12m_{\mathrm{eff}}\dot q_{\max}^{\,2}=E.
$$

Aux deux extrémités, toute l'énergie est potentielle et $\dot q=0$. Le minimum de la parabole est un équilibre stable : si la masse est légèrement déplacée, elle est ramenée vers $q=0$.

### Exemple 2 : potentiel avec une barrière

Considérons un potentiel présentant deux minima séparés par un maximum, par exemple :

$$
V(q)=\frac{\alpha}{4}(q^2-a^2)^2,
\qquad \alpha>0,\quad a>0.
$$

Les minima sont en $q=-a$ et $q=a$, où $V=0$, tandis que le maximum local est en $q=0$, avec :

$$
V(0)=\frac{\alpha a^4}{4}.
$$

La hauteur de la barrière est donc :

$$
E_{\mathrm b}=\frac{\alpha a^4}{4}.
$$

- Si $0<E<E_{\mathrm b}$, deux domaines accessibles apparaissent autour de $-a$ et de $a$. Une particule placée dans un puits reste dans ce puits : elle ne peut pas passer par $q=0$.
- Si $E=E_{\mathrm b}$, la particule atteint le sommet de la barrière avec une vitesse nulle. Le point $q=0$ est un équilibre instable ; une perturbation, même très petite, décide de quel côté elle repart.
- Si $E>E_{\mathrm b}$, la région centrale devient accessible et la particule peut passer d'un puits à l'autre.

Cet exemple montre que l'énergie ne détermine pas seulement l'amplitude d'une oscillation : elle peut aussi modifier la région de l'espace de configuration dans laquelle le mouvement est possible.

### Exemple 3 : potentiel effectif dans un mouvement central

Dans un mouvement central, la conservation du moment cinétique permet de ramener le mouvement radial à un degré de liberté :

$$
E=\frac12m\dot r^2+V_{\mathrm{eff}}(r),
$$

avec, pour une force gravitationnelle attractive :

$$
V_{\mathrm{eff}}(r)=\frac{h^2}{2mr^2}-\frac{\mu m}{r}.
$$

Le premier terme est la contribution centrifuge, qui tend à empêcher la chute vers $r=0$, tandis que le second est l'attraction gravitationnelle. Le minimum de $V_{\mathrm{eff}}$ correspond à une orbite circulaire stable. Pour une énergie située au-dessus de ce minimum mais en dessous de zéro, le rayon oscille entre deux points d'arrêt : l'orbite est liée. Pour $E=0$, on obtient le cas limite de l'évasion ; pour $E>0$, le mouvement peut atteindre l'infini.

### Résumé des informations données par le graphe

| Élément du diagramme | Interprétation mécanique |
|---|---|
| $V(q)<E$ | mouvement possible, $\dot q\neq0$ |
| $V(q)=E$ | point d'arrêt, $\dot q=0$ |
| $V(q)>E$ | région interdite classiquement |
| minimum de $V$ | équilibre stable, puits de potentiel |
| maximum de $V$ | équilibre instable, sommet de barrière |
| courbe qui monte vers une barrière | franchissement conditionné par l'énergie |
| minimum de $V$ | vitesse maximale pour une énergie $E$ fixée |

## 6. Équilibre et stabilité

Une position $q_*$ est un équilibre si :

$$
\dot q=0,\qquad \ddot q=0.
$$

Pour un potentiel régulier :

$$
V'(q_*)=0.
$$

La stabilité locale se lit avec :

- $V''(q_*)>0$ : minimum, équilibre stable ;
- $V''(q_*)<0$ : maximum, équilibre instable ;
- $V''(q_*)=0$ : test inconclusif, développer à l'ordre supérieur.

### Perturbations infinitésimales

Poser :

$$
q=q_*+\eta,\qquad |\eta|\ll1.
$$

Linéariser l'équation au premier ordre. Si l'équation obtenue est :

$$
\ddot\eta+\omega^2\eta=0,
$$

la perturbation reste bornée et l'équilibre est stable. Si elle est de la forme :

$$
\ddot\eta-\lambda^2\eta=0,
$$

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

Pour $\mathbf F=f(r)\mathbf e_r$ :

1. montrer que $\mathbf H_O$ est constant ;
2. en déduire que le mouvement est plan ;
3. écrire l'accélération en polaires ;
4. utiliser l'énergie et le moment cinétique ;
5. analyser le potentiel effectif.

Voir [[Mouvement central et lois de Kepler]].
