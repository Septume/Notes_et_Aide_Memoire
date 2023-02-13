# Transformation, transitions et animations

## Transformations

On utilise la propriété `transform` qui prend pour valeur une ou plusieurs fonctions de transformation

2 types de transformations :

- transformations 2D : fonctionne sur 2 axes
	- x : axe horizontal
	- y : axe vertical
- transformations 3D : fonctionne avec un 3ème axe z représentant la profondeur. Pour cela il faut que l’élément soit mis en perspective

### Transformations 2d

`rotate()` : Permet de faire une rotation dans le sens horaire. Prend comme argument une valeur exprimée en `deg` (degré) ou `turn` (1turn = 360 degré). Il est possible d'utiliser une valeur négative permettant d'effectuer une rotation dans le sens anti-horaire.

`scale(x,y)` : Permet de faire un zoom sur l’élément. On indique un nombre correspondant au facteur de zoom effectué sur les deux axes x et y ou deux nombres correspondant chacun à l’axe x et y. On peut également utiliser `scaleX()` et `scaleY()` pour définir le décalage sur une seule axe.

`translate(x,y)` : Permet de décaler sur l’axe x ou/et sur l’axe Y . On peut également utiliser `translateX()` et `translateY()` pour définir le décalage sur une seule axe. On peut utiliser une valeur absolue ou une valeur relative à la taille de l’élément. Il est possible d'utiliser une valeur négative.

`skewX()` et `skewY():` Étire l’élément (remarque : la fonction skew() existait mais a été retirée). on indique une valeur en degré

Le point d’origine est par défaut le centre de l’élément. Il est possible de le changer avec `transform-origin` qui prend deux valeurs (px ou %) correspondant chacun à l’axe vertical et horizontal

```css
/* En bas à droite */
transform-origin: 100% 100%;

/* en haut à 30px du bord gauche */
transform-origin: top 0 left 30px;
```

Il est possible de combiner plusieurs transformations (Remarque : L’ordre des fonctions a de l’importance. Le résultat peut parfois être différent avec un ordre différent)

```css
transform: scale(0.7) rotate(15deg) skewY(10deg);
```

### Transformations 3d

Pour créer un objet 3D on a besoin de deux paramètres :

- la perspective : indique la distance de l’ œil avec la scène. Une perspective faible donne l’impression que l’on est près de l’objet et à l’inverse une perspective élevée donne l’impression que l’on est loin.
- l’origine du point de fuite : le point d’ancrage de la scène, ce qui va donner l’impression qu’on regarde d’un certain côté la scène

Propriétés à utiliser dans un élément conteneur (qui peut être body si toutes les scènes 3D de la page doivent avoir la même perspective )

- `perspective` (en px)
- `perspective-origin` : deux valeurs indiquant l’axe x et y. On peut utiliser les mots clés `top`, `bottom` etc…

Les fonctions :

- `translate3d(x, y, z)` : positionne l’objet sur les 3 axes
- `translateZ(z)` : positionne l’objet sur l’axe z (0, 0, Z)
- `scale3d(x, y, z)`
- `scaleZ(z)`
- `rotate3d(x, y, z)`
- `rotateZ(z)`

## Transitions

Les effets de transition ont lieu lors d'un changement d'état d'un élément. Ce changement d'état peut être provoqué par des pseudo-classes comme `:hover` et `:active` ou du code JavaScript.

`transition-property` : Permet d'indiquer les propriétés de l'élément (séparées par une virgule) sur lesquelles sera appliqué un effet de transition lors d'un changement d'état. La valeur par défaut est `all` (toutes les propriétés sont concernées). On peut aussi utiliser la mot clé `none`

`transition-duration` : Durée de la transition. On indique une valeur en `s` (secondes) ou `ms` (millisecondes). Par défaut la valeur est `0s`, ce qui annule les effets de transition. Il est possible de définir des durées de transition différentes pour chaque propriété. Pour cela on indique plusieurs valeurs (séparées par une virgule) correspondant dans l'ordre aux valeurs définies dans `transition-property`

`transition-delay` : Délais en `s` ou `ms` avant le début de la transition. Il est possible d'indiquer une valeur négative qui lance la transition immédiatement mais à partir d'un état intermédaire (comme si elle avait débuté avant). On peut indiquer plusieurs valeurs pour définir des delais différents pour chaque propriété.

`transition-timing-function` : Variation de la vitesse de la transition. On peut indiquer plusieurs valeurs pour définir des variations différentes pour chaque propriété.

- `ease` : Défaut. La vitesse augmente au millieu de la transition et ralenti à la fin. Correspond à `cubic-bezier(0.25, 0.1, 0.25, 1.0)`
- `linear` : Vitesse constante. Correspond à `cubic-bezier(0.0, 0.0, 1.0, 1.0)`
- `ease-in` : Démarre doucement et accélère vers la fin. Correspond à `cubic-bezier(0.42, 0, 1.0, 1.0)`
- `ease-out` : Démarre rapidement et ralenti vers la fin. Correspond à `cubic-bezier(0, 0, 0.58, 1.0)`
- `ease-in-out` : Démarre doucement, accélère puis ralenti à nouveau vers la fin. Correspond à `cubic-bezier(0.42, 0, 0.58, 1.0)`
- `cubic-bezier()` : Utilisation d'une courbe de bezier qui prend 4 coefficients entre 0 et 1. (Voir [ce site](https://cubic-bezier.com) pour en créer une)

```css
.box {
  width: 200px;
  height: 200px;
  background-color: lightgray;
 
  transition-property: border-radius, background-color;
  transition-duration : 1s;
  transition-delay: 0s, 1s;
  transition-timing-function: ease-in;
}

.box:hover {
  background-color: gray;
  border-radius : 50%;
}
```

`transition` : Propriété raccourcie. On peut indiquer les valeurs dans n'importe quelle ordre sauf pour la valeur de `transition-duration` qui doit se trouver avant celle de `transition-delay`.

```css
.box {
  width: 200px;
  height: 200px;
  background-color: lightgray;
 transition: border-radius 1s 0s ease-in, background-color 1s 1s ease-in;

}

.box:hover {
  background-color: gray;
  border-radius : 50%;
}
```

Les pseudoclasses les plus couramment utilisées pour déclencher des transitions sont :

- `:hover`
- `:active`
- `:focus`
- `:valid`
- `:invalid`
- `:not()`
- `:checked`
- `:enabled`
- `:disabled`

## Animations

Pour créer une animation il faut :

1. Définir une animation
2. Appliquer l'animation définie à un élément

L'animation pourra être jouée au chargement de la page sans intervention de l'utilisateur.

### Définir une animation

On utile la directive `@keyframes` suivi d'un nom pour l'animation

```css
@keyframes mon-animation {}
```

Le bloc décrit les étapes de l'animation. Le mot clé `from` correspond à l'état initial de l'animation et le mot clé `to` à l'état final.

```css
@keyframes mon-animation {
	from { transform: translateX(0px);}
	to { transform: translateX(800px);}
}
```

Il est est possible d'indiquer plus de deux états à une animation. Les étapes intermédiaires sont indiquées via un pourcentage (Par rapport à la durée de l'animation). A noter que les mots clés `from` et `to` sont en fait des alias pour indiquer `O%` et `100%`

```css
@keyframes mon-animation {
	0% { transform: translateX(0);}
	20% { transform: translateX(-50px);}
	/* Le décalage de 800px se fait par rapport à la position précédente, c'est à dire -50px */
	100% { transform: translateX(800px);}
}
```

### Application de l'animation

Sur l'élément à animer ou utilise ces propriétés.

`animation-name` : Le nom de l’animation qui a été défini via le `@keyframes`. On peut indiquer plusieurs noms d'animation (séparés par une virgule)

`animation-duration` : Durée de l’animation

`animation-delay` : Délai avant le début de l'animation

`animation-timing-function` : Variation de la vitesse de l’animation. En plus d'une fonction `cubic-bezier()` et des mots clés associés (`ease`, `linear`, …) Il est également possible d’utiliser la fonction `steps()` qui permet de créer un effet sacadé.

`animation-iteration-count` : Nombre de répétitions de l’animation. Par défaut, la valeur est 1. On peut indiquer des valeurs décimales qui représentent des fragments de cycle (Ex : 0.5 représente la moitié d'un cycle). Avec le mot clé `infinite` l’animation sera jouée en continu.

`animation-direction`

- `normal`
- `reverse` : Joue l’animation en sens inverse.
- `alternate` : Les cycles de l'animation sont alternés entre le sens normal et le sens inverse. (`animation-iteration-count` doit être supérieur à 1)
- `alternate-reverse` : Idem mais en commençant en sens inverse.

`animation-fill-mode` : Permet de préciser l'état de l'élément avant le début ou/et après la fin de l'exécution de l'animation

- `none` : Défaut. L'élément est dans son état original avant le commencement de l'animation et revient à son état original après que l'animation soit terminée.
- `backwards` L'élément est mis dans l'état de départ de l'animation avant le commencement de celle ci et revient à son état original après que l'animation soit terminée.
- `forwards` : L'élément est dans son état original avant le commencement de l'animation et reste dans l'état de fin de l'animation quand celle ci est terminée.
- `both` : L''élément est mis dans l'état de départ de l'animation avant le commencement de celle ci et reste dans l'état de fin de l'animation quand elle est terminée.

`Animation-play-state` : Indique l'état d' exécution de l'animation

- `running` : L'animation est en cours - Défaut
- `pause` : L'animation est en pause

`Animation` : Propriété raccourcie. La valeur de la durée doit être indiquée avant celle du delais. Le mot clé `none` permet de désactiver une animation.

```css
@keyframes anim{
  0% { transform: translateX(0) rotate(0);}
  100% { transform: translateX(500px) rotate(3turn);}
}

.box {
  width: 100px;
  height: 100px;
  background-image : conic-gradient(red, pink);
  border-radius : 50%;
  animation : anim 4s linear infinite alternate;
}
```

Pour créer un effet sacadé on peut utiliser la fonction `steps()` associé la propriété `animation-timing-function`

```css
@keyframes anim{
  0% { transform: translate(0,0);}
  25% { transform: translate(200px,0);}
  50% { transform: translate(200px,200px);}
  75% { transform: translate(0,200px);}
  100% { transform: translate(0,0);}
}

.box {
  width: 20px;
  height: 20px;
  background-color : lightblue;
  animation : anim 4s infinite steps(1);
  
}
```

Il est possible d'indiquer les valeurs de `animation-timing-function` dans le `@keyframes`

```css
@keyframes mon-animation {
	0% { 
		transform: translateX(0);
		animation-timing-function: ease-in;
		
	}
	50% { 
		transform: translateX(300px);
		animation-timing-function: linear;

	}
	100% { 
		transform: translateX(600px);
	}
}
```

### Performances des transitions et animations

Une animation CSS est affichée en temps réel par le navigateur qui la met à jour à chaque calcul des nouvelles images. Le nombre d'images par seconde de l'animation peut donc être variable.

La plupart des écrans ayant un taux de rafraîchissement de 60 hz, il faut faire en sorte que l'animation soit suffisament optimisée pour afficher au minimum 60 images par seconde (60 FPS) soit 16 ms pour calculer une image

Pour optimiser l'animation, il est recommandé d'animer uniquement les propriétés qui sont calculées lors de l'étape *composite* du rendu du navigateur, ce qui est le cas des propriétés `transform` et `opacity`

En d'autre terme il faut éviter les animations qui redéclanchent les étapes *layout* et *paint* du rendu. Par exemple en animant la propriété `witdh` qui est calculée lors de l'étape du *layout* ou `background-color` lors de l'étape du *paint*

**Analyser la performance de l'animation avec Chrome DevTools**

- Aller dans l'onglet *Performance*
- Cocher la case *ScreenShots*. Cela permet de prendre une capture d'écran de chaque image de l'enregistement
- Dans les paramètres régler l'option *CPU throttling* sur 6x ce qui permet de simuler un processeur 6 fois plus lent.
- Cliquer sur le bouton *Record* pour lancer l'enregistrement. Effectuer les actions sur le site pour déclencher l'animation. Puis terminer l'enregistrement en cliquand sur le bouton *Stop*

Les carrés verts de la section *Frames* représentent chaque image de l'animation et indique au survol de la souris le temps d'affichage en ms et le FPS correspondant (remarque : On peut faire un zoom sur la ligne de temps pour afficher en plus grand)

![](devtools-performances-animation.gif)

La section *main* permet de voir tous les calculs effectués, répartis en catégories identifiées par des codes couleurs

- Violet : Analyse du CSS et calculs de base
- Jaune : Calculs de l'étape *Layout*
- Vert : Calcul des étapes *Paint* et *Composite*. (Passer le curseur de la souris sur le graphisme pour afficher les détails)
