# Couleurs, background et effets visuels

## Couleur d’un élément

Propriété `color`

Les types de valeurs sont :

- Un nom de couleur standard
- une valeur hexadécimale. Par exemple : `#ff0033` (Qui peut également s’écrire `#f03`)
- une valeur RGB. Par exemple : `rgb(255, 0, 51)`
- Une valeur RBGa. Par exemple : `rgba(255, 0, 51, 0.5)`
- une valeur HSL (Pour Hue, Saturation, Lightness => Teinte, Saturation, Luminosité). Par exemple : `hsl(0, 100%, 50%)`
- Une valeur HSLa. Par exemple : `hsla(0, 100%, 50%, 0.5)`
- `transparent`: Couleur totalement transparente, laissant voir la couleur située en arrière plan. (Techniquement cela correspond à `rbga(0,0,0,0)`)
- `currentColor` : Variable qui représente la valeur `color` de l’élément. (Utile pour faire hériter les propriétés de couleur par d’autres propriétés, ou par les propriétés d’un élément enfant qui n’héritent pas par défaut)

## Arrière-plans

**Remarque importante** : Il existe une particularité pour l'élément `body` . Les styles d'arrière plan appliqués à ce dernier sont propagés à l'élément `html` (élément racine) si ce dernier ne possède pas ses propres styles d'arrière plan. Par exemple, si on redimensionne le `body` pour que sa largeur soit plus petite que celle du viewport et qu'on lui applique une couleur de fond, celle ci s'affiche malgré tout sur l'ensemble du viewport du fait que la valeur s'applique également à `html`

`background-color` : Indique une couleur d'arrière plan

`background-image` : Indique une ou plus images d'arrière plan (séparées par une virgule) Chaque image est placée en-dessous de celle qui la précède sur l’axe des z (z-axis)

```css
background-image: url("img/fond.png"), url("img/logo.png");
```

`background-attachment` : Indique si l'image d'arrière plan est fixe ou non.

- `local` l'arrière-plan défile avec le contenu lorsqu'on scroll
- `scroll` : (Défaut) L’arrière plan défile avec le viewport mais reste fixe par rapport à son conteneur
- `fixed` : l'arrière-plan est fixe par rapport au viewport

[https://codepen.io/Ste-Cy/pen/OJXdEaw](https://codepen.io/Ste-Cy/pen/OJXdEaw)

`background-repeat` : Indique si l'image de fond doit être répétée ou non

- `repeat` : (défaut) L'image est répété horizontalement et verticalement de sorte à couvrir toute la zone de l'arrière plan. La dernière image est rognée si nécessaire
- `no-repeat` : L'image n'est pas répétée et est donc unique sur la page
- `repeat-x` : L'image est répétée uniquement sur la première ligne, horizontalement
- `repeat-y` : L'image est répétée uniquement sur la première colonne, verticalement.
- `space` : L'image est répétée sans qu'il n(y ait de rognage. La première et la dernière image sont collées aux bords de l'élément et les espaces entre sont repartis de façon égale de sorte à couvrir toute la zone d'arrière plan.
- `round` L'image est répétée de sorte à ce qu'il n'y ait ni rognage ni espace restant. Par conséquent les images peuvent être étirées pour remplir tout l'espace, ou au contraire rétrécies pour que la dernière image puisse entrer sans être rognée

`background-clip` : Permet de définir les limites de la zone d'arrière plan

- `border-box` (défaut) : La zone d'arrière plan s'étend jusqu'à la limite externe de la bordure (L'arrière plan se situe sous la bordure)
- `padding-box` : La zone d'arrière plan se limite à la marge interne (padding)
- `content-box` : La zone d'arrière-plan se limite au contenu

`background-origin` : Détermine le point d'origine de l'image d'arrière plan. Attention, cette propriété est ignorée si `background-attachment` est de valeur `fixed`

- `padding-box` : (Défaut) Le point d'origine de l'image est situé par rapport à la marge interne (padding)
- `border-box` : Le point d'origine de l'image est situé par rapport à la bordure et se positionne sous celle-ci.
- `content-box` : Le point d'origine de l'image est situé par rapport au contenu

`background-position` : Position de l’image de l'arrière plan par rapport aux bords haut et gauche du conteneur. (On peut indiquer les positions de plusieurs images en les séparant par une virgule). Cette position peut être indiquée via une ou plusieurs valeurs spécifiant les coordonnée XY de l'image. On peut utiliser une longueur (exprimée en px ou em), un % (relatif au conteneur) ou un mot clé ( `top`, `bottom`, `left`, `center` et `righ`).  
Quelques exemples :

```css
/* L'image est positionnée en haut au millieu (sur l'axe horizontal) */
background-position: top; 
/* L'image est positionnée à gauche au millieu (sur l'axe vertical) */
background-position: left;
/* L'image est positionnée en haut à gauche */
background-position : top left;
/* L'image est centrée */
background-position: center;
background-position: 50%;

/* Décalée de 5px par rapport à la gauche et de 10px par rapport au haut */
background-position: 5px 10px;
/* Décalée de 5px par rapport à la droite et de 10px par rapport au bas */
background-position: right 5px bottom 10px;
/* L'image est positionnée en haut et est décalée de 20px par rapport à la gauche */
background-position: top left 20px;
/* Décalée de 10% par rapport à la gauche et de 30% par rapport au haut */
background-position : 10% 30%;

/* La première image est positionnée en haut au millieu 
et la seconde est décalée de 5px par rapport à la droite et de 10px par rapport au bas */
background-position : top, right 5px bottom 10px;
```

Formule pour le calcul avec les %

```
(largeur conteneur - largeur image) * (position en %) = (décalage horizontal)
(hauteur conteneur - hauteur image) * (position en %) = (décalage vertical)
```

`background-size` : Permet de spécifier la taille de l'image d'arrière plan. les valeurs possibles sont :

- Des dimensions indiquées sous la forme `x y` , correspondant à largeur et à la hauteur de l’image. On peut indiquer une valeur en % (Attention, c'est par rapport aux dimensions de la zone d'arrière plan et non celles de l'image) ou la valeur `auto` (la dimension correspondante sera automatiquement calculé pour que l’image garde ses proportions d’origine)
- `contain` : L'image est redimensionnée de sorte à ce qu'elle couvre le plus possible toute la zone d'arrière plan mais en conservant ses proportions. Si il reste de l'espace libre, il est rempli par la couleur d'arrière plan. Par défaut l'image est centrée sauf si `background-position` a été modifiée
- `cover` : Idem, sauf qu'il y a pas d'espace libre. L'image couvre toute la zone quitte à être rogner pour pouvoir conserver ses proportions.

`background` : propriété raccourcie des 8 propriétés précédentes. Les valeurs non indiquées sont réinitialisées aux valeurs initiales. On peut indiquer plusieurs arrière plan séparés par des virgules. Attention :

- La valeur de `background-size` peut uniquement être utilisée directement après une valeur `background-position` suivie d'une barre oblique (par exemple "`center/80%`")
- Pour `background-origin` et `background-clip` : Si il y qu'une seule valeur indiquée elle est appliquée au deux propriétés. Sinon la première occurrence s'applique à `background-origin` et la deuxième à `background-clip`

Quelques exemples :

```css
/*définition de deux arrière plan */
background: url("image1.jpg") repeat-x, url("image2.jpg") no-repeat right 20px bottom 30px;

/* La valeur de background-position (suivi d'une barre oblique) est obligatoire pour indiquer la valeur de background-size
Ici on met 0 pour conserver la valeur initiale */
background: url("image.jpg") no-repeat 0/contain;

/* La valeur border-box concerne background-origin et background-clip  (car indiqué qu'une seule fois) */
background: url("image.jpg") no-repeat border-box;
```

## Sprites css

Technique qui permet d’afficher plusieurs images qui sont regroupées dans un seule et même fichier. Le fichier aura un poids plus important que l’ensemble des images réunis mais l’avantage est qu’une seule requête http sera nécessaire pour afficher toutes les images.

On utilise `background-image` pour récupérer l’image et on fixe une position et une dimension pour n’afficher qu’une partie du sprite.

```css
.flags-canada, .flags-mexico, .flags-usa {
	background-image: url(’../images/flags.png’);
	background-repeat: no-repeat;
}

.flags-canada {
	height: 128px;
	background-position: -5px -5px;
}

.flags-usa {
	height: 135px;
	background-position: -5px -143px;
}

	.flags-mexico {
	height: 147px;
	background-position: -5px -288px;
}
```

## Transparence

`opacity` : on indique une valeur entre 0 (transparence totale) et 1 (opacité totale) pour indiquer le niveau de transparence.

`Opacity` ne concerne pas que les couleurs mais tout les éléments HTML (image, texte…)

```css
.light {
	opacity: 0.2;
}
```

## Bordures

`border-width` : Largeur de la bordure. On peut utiliser des mots clés

- `thin` : Bordure fine
- `medium` : Bordure moyenne
- `thick` : Bordure épaisse

`border-color` : Couleur de la bordure.

`border-style` : Style de la bordure

- `none` : (par défaut) Pas de bordure. La valeur de `border-width` sera de 0, même si une autre valeur est indiquée)
- `hidden` : Pas de bordure affichée. La valeur de `border-width` sera de 0, sauf si un arrière-plan a été défini.
- `solid` : un trait simple
- `dotted` : pointillés
- `dashed` : tirets
- `double` : trait double (la somme des épaisseurs correspond à la valeur de `border-width`
- `groove` : Effet 3D avec impression de gravure
- `ridge` : Effet 3D avec impression que la bordure ressort du document.
- `inset` : effet 3D avec impression d'une bordure enfonc
- `outset` : effet 3D avec impression d'une bordure surélevé

Remarque : `border-width` , `border-color`, et `border-style` sont des propriétés raccourcies de propriétés telle que `border-top-width` , `border-right-color`,etc.

Pour l'utilisation des propriétés raccourcies, on peut indiquer une à 4 valeurs :

- 1 valeur : Correspond aux 4 côtés de la bordure
- 2 valeurs : La 1ère valeur correspond aux côtés haut/bas et la 2ème valeur aux côtés gauche/droit
- 3 valeurs : La 1ère valeur correspond au côté haut, la deuxième aux côtés gauche/droit et la 3ème au côté bas.
- 4 valeurs : l'ordre est haut-droit-bas-gauche

`border` : propriété raccourci de `border-width`, `border-style` et `border-color` . On peut omettre d'indiquer une valeur de couleur. Dans ce cas elle hérite de celle du texte.

```css
border: 1px solid black;
```

Attention : cette propriété n'accepte qu'une valeur pour chaque propriété détaillée. On ne peut donc l'utiliser que si on souhaite 4 côtés au style identique. Si on souhaite appliquer un style à un côté spécifique ou peut utiliser les propriétés raccourcies `border-top`, `border-bottom`, `border-left` et `border-right`

## Bordure créée avec une image

Remarque : Il est fortement recommandée de définir en plus une bordure de remplacement avec la propriété `border` (Cette propriété doit être définie avant celle de `border-image` )

`border-image-source` : Permet d'indiquer l'URL de l'image. On peut également indiquer un dégradé. Si la valeur est `none` c'est la mise en forme définie par `border-style` qui sera appliquée

`border-image-slice` Permet de découper l'image en 9 régions à l'aide de 4 lignes de découpe

- 4 régions qui correspondra aux 4 coins de la bordure. Les morceaux d'image conserveront leur taille initiale et ne seront pas répétés.
- 4 régions qui correspondra aux cotés de la bordure + 1 région qui pourra éventuellement être utilisée comme image d'arrière plan. Les morceaux d'image pourront être étirés ou/et répétés en fonction des paramètres définis.

![](border-image-slice.jpg)

![](fig32_french.png)

 On indique 1 à 4 valeurs qui correspond au décalage des lignes de découpe par rapport aux bords (même fonctionnement que la propriété `border` )

Les valeurs peuvent être :

- un nombre : qui correspond à une longueur en pixel pour une image matricielles ou à une coordonnée pour une image vectorielle
- Un pourcentage : relatif à la hauteur de l'image pour les axes verticaux et à la largeur pour les axes horizontaux.

Il est recommandé d'utiliser des pourcentages pour les images vectorielles. Les valeurs négatives sont invalides et les valeurs dépassant les bornes sont ramenées à 100%

En plus de ces valeurs ont peut indiquer le clé `fill` qui permet de préciser que l'on souhaite utiliser la région centrale comme image d'arrière plan.

```css
/* 
lignes de decoupe à 
10px des bords haut et bas
20px des bords gauche et droite 
utilisation de la region centrale comme background
*/

border-image-slice: 10 20 fill; 
```

`border-image-width` : Permet de définir la largeur de la bordure (même fonctionnement que `border-width`). Cette propriété écrase la valeur de `border-with` si elle a été définie. Si aucune des deux propriétés n'ont de valeur définie, la valeur par défaut correspond à `border-width: medium`

les valeurs sont :

- `auto` permet d'avoir une largeur qui correspond à celles des régions d'image découpées correspondantes
- une taille en px, em ou % : Si la largeur est plus petite ou plus grande que celle de l'image correspondante, celle-ci sera contractée ou étirée sur sa largeur.
- un nombre : représente un multiple de la valeur de `border-width`

`border-image-outset` : Permet d'agrandir la bordure pour qu'elle déborde dans la marge externe. La valeur peut être une longueur en px, em et % ou un nombre correspondant à un multiple de la valeur de `border-width`. les valeurs négatives sont invalides.

`border-image-reapeat` : Permet de préciser la façon doit les images utilisées pour les bords sont répétées ou mise à l'échelle afin de remplir l'espace de la bordure sur la longueur. On utile 1 à 4 valeurs qui peuvent être :

- `stretch` : l'image est étirée pour remplir l'espace
- `repeat` l'image est répétée pour remplir l'espace. Cela peut entrainer un rognage sur la derrière occurrence de l'image si la longueur de la bordure n'est pas un multiple de la longueur de l'image.
- `round` : l'image est répétée pour remplir l'espace mais ne sera pas rognée ce qui peut entrainer une déformation
- `space` : l'image est répétée pour remplir l'espace, mais sans déformation ni rognage. Pour empêcher cela, des espacements seront créés entre les occurrences de l'image.

`border-image` : propriété raccourcie. Les valeurs de `border-image-slice`, `border-image-witdh` et `border-image-outset`, si indiquée, doivent être séparée par un `/`

```css
border-image: url("/images/border.png") 27 23 / 50px 30px / 1rem round space;
```

## Coins arrondies

Propriété `border-radius`

La courbure de chaque coin est définie avec un ou deux rayons de courbures (valeurs séparées par un slash) qui permettent de définir un arc de cercle ou un arc d'ellipse.

![](border-radius.jpg)

La courbure s'applique à l'arrière-plan (défini avec la propriété `background`) même si l'élément n'a aucune bordure. Le rognage de l'arrière plan s'applique sur la boîte définie par `background-clip`.

La propriété prend 1 à 4 valeurs :  

- 1 valeur : Correspond à tout les coins
- 2 valeurs : La première correspond aux coins haut/gauche et bas/droit et la deuxième aux coins haut/droit et bas/gauche
- 3 valeurs : La première correspond au coin haut/gauche , la deuxième aux coins haut/droit et bas/gauche et la troisième au coins bas/droit
- 4 valeurs : L'ordre est dans le sens horaire ⇒ haut/gauche, haut/droit, bas/droit, bas/gauche

```css
/* taille pour tout les coins */
border-radius: 10px;

/* 
taille différente pour chaque coins 
haut gauche - haut droit - bas droit - bas gauche
*/
border-radius: 10px 5px 10px 5px; 

/*
affine l'arrondi en créant des courbes elliptiques.
on indique deux valeurs séparées par un slash 
*/
border-radius: 20px / 10px;
```

La propriété `border-radius` est une propriété raccourcie de `border-top-left-radius`, `border-top-right-radius`, `border-bottom-right-radius` et `border-bottom-left-radius`.

## Contours

Les contours (outline) sont dessinés à l’extérieur du cadre de l’élément (Ils peuvent donc chevaucher d'autres contenus). Ils n’ont pas d’incidence dans la taille ou la position de l’élément

- `outline-color` : pour indiquer la couleur du outline. On peut utiliser la mot clé `invert` qui aura pour effet d'utiliser une couleur contraire de celle de l'arrière-plan afin de renforcer le contraste.
- `outline-style` : Style du contour
	- `none` : Aucun contour
	- `auto` : Mise en forme automatique
	- `solid`, `dotted`, `dashed`, `double`, `groove`, `ridge`, `inset`, `outset`
- `outline-width` : Taille du contour. Utilise les même valeur que `border-width`
- `outline` : Propriété raccourcie.

Le outline est utilisé pour la visualisation de l’élément qui a le focus. Pour modifier la propriété outine liée il faut utiliser la pseudo-classe :`focus`

```css
/* Désactive le outline des champs de formulaire ayant de focus */
input:focus {
	outline: none;
}
```

## Ombres

`box-shadow` : ajoute une ombre sur les éléments de type block. Les arrondies sont respectées sur l'ombre.

Les valeurs sont :

1. Le décalage horizontal de l’ombre (Une valeur négative permet de placer l’ombre à gauche de l’élément)
2. Le décalage vertical de l’ombre (Une valeur négative permet de placer l’ombre en haut de l’élément)
3. (Facultaitf) Rayon du flou (blur) Plus la valeur est haute, plus le flou de l’ombre sera diffus. Valeur positive seulement.
4. (Facultatif) . Le rayon d’étendue de l’ombre (spread). Agrandi (valeur positive) ou rétréci (valeur négative) l’ombre par rapport à l’élément. Si la valeur est nulle, l’ombre a la même taille que l’élément.
5. (Facultatif) La couleur de l’ombre. Si non indiqué c’est le navigateur qui décide de la couleur à appliquer (cela peut-être la couleur du texte)

- `inset` : (Facultatif) permet de placer l’ombre à l’intérieur du bloc

```css
box-shadow: -25px -20px 8px 10px grey; 
```

Remarque :

- Une valeur de 0 pour un des décalages place l'ombre au dessus de l'élément
- Une valeur de 0 pour les deux décalages place l'ombre en dessous de l'élément. Cette dernière peut être visible en fonction de la valeur du rayon du flou.
- l’entendue totale de l’ombre est égale au décalage + rayon du flou
- Le flou peut être faible (inférieur au décalage), normal (égal au décalage) ou élevé (supérieur au décalage)

Il est possibles de spécifier plusieurs ombres, en séparant les valeurs par une virgule

```css
box-shadow: 0px 20px 20px -20px, 0px -20px 20px -20px; 
```

## Visibilité d’un élément

`visibility`

- `visible` : élément visible (Défaut)
- `hidden` : élément invisible. Attention l’élément reste dans le flux normal et occupe toujours l’espace
- `collapse`: Dans le cadre d’un tableau permet de masquer des lignes, groupes de lignes, colonnes et groupes de colonnes d’un tableau. L’élément n’occupe plus l’espace comme si on avait appliqué `display: none` . Par contre la taille des autres lignes et colonnes continue d’être calculée en prenant en compte les éléments masqués. Cela permet de retirer rapidement des lignes et colonnes sans avoir à recalculer les dimensions pour l’ensemble du tableau.

## Éléments remplacés

`object-fit` : permet de définir la façon donc un élément remplacé (image, vidéo, etc.) doit s'adapter à son conteneur.

- `none` : L'élément garde ses dimension d'origine
- `contain` : L'élément garde son ratio d'origine tout en s'ajustant à la taille de son containeur. L'élément pourra donc être soit agrandi, soit rétréci par rapport à sa taille d'origine.
- `scale-down` : Correspond soit à `none` soit à `contain`. C'est la dimension la plus petite qui sera appliquée.
- `cover` : L'élément garde son ratio d'origine et rempli tout l'espace de son conteneur ce qui peut entrainer un rognage
- `fill` : L'élément rempli tout l'espace de son conteneur sans tenir compte du ratio. Cela peut entrainer une déformation de l'image.

`object-position` : permet de définir la position de l'élément dans son conteneur. Fonctionne comme la propriété `background-position`
