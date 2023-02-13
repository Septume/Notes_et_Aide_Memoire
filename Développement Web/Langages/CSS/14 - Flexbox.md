# Flexbox

Module permettant de positionner des éléments de manière "flexible’. Repose sur un élément servant de containeur

## Vocabulaire

- **flex container** : élément parent containeur
- **flex items** : éléments enfants
- **main axis** : axe principal du container sur lequel les items sont disposés. Cet axe peut être horizontal (orientation en ligne) ou vertical (orientation en colonne)
- **main size** : taille du conteneur sur l’axe principal. Il s’agit de la largeur pour une orientation en ligne ou de la hauteur pour une orientation en colonne
- **main-start | main-end** : point de début et de fin entre lesquels se trouvent les éléments sur l’axe principal
- **cross axis** : axe secondaire qui est perpendiculaire à l’axe principal. Sa direction dépend de la direction de l’axe principal.
- **cross size** : taille du conteneur sur l’axe secondaire . Il s’agit de la hauteur pour une orientation en ligne ou de la largeur pour une orientation en colonne
- **cross-start | cross-end** : point de début et de fin entre lesquels se trouvent les éléments sur l’axe secondaire

![](modele_flexbox_01.png)

![](modele_flexbox_02.jpg)

## Propriétés du container

Remarque : Les propriétés pour le multicolonnes n’ont plus d’effet sur un container flex

`display`

- `flex` : créé un conteneur flex avec un comportement block
- `inline-flex` : créé un conteneur flex avec un comportement `inline-block`. Les éléments peuvent s’aligner verticalement avec la propriété `vertical-align`

`flex-direction` : indique la direction de l’axe principal

- `row` : (défaut) sur une ligne de gauche à droite
- `row-reverse` : sur une ligne de droite à gauche (ordre inversé)
- `columm` : sur une colonne de haut en bas
- `column-reverse` : sur une colonne de bas en haut

`flex-wrap` : Défini si les items sont disposés sur une seule ligne (ou colonne)

- `nowrap` : (défaut) pas de retour à la ligne
- `wrap` : les éléments retournent à la ligne s’il n’y a plus de place
- `wrap-reverse` : les éléments retournent à la ligne en sens inverse

Remarque : A la place des propriétés `flex-direction` et `flex-wrap` on peut utiliser la super-propriété `flex-flow`

```css
flex-flow: column wrap;
```

`justify-content` : alignement sur l’axe principal (défini par la direction)

- `flex-start` : au début
- `flex-end :` à la fin
- `center` : au centre
- `space-between` : les éléments s’étirent sur tout l’axe avec des espaces entre eux
- `space-around` : idem mais avec en plus des espaces au extrémités

`align-items` : alignement sur l’axe secondaire

- `stretch` : (defaut) les éléments sont étirés sur tout l’axe
- `flex-start`
- `flex-end`
- `center`
- `baseline` : sur la ligne de base du texte (line-height). Généralement identique à `flex-start` si la taille de police est uniforme

`align-content` : s’utilise uniquement sur un conteneur autorisant le passage à la ligne (`flex-wrap`). Défini l’alignement des rangés de ligne

- `stretch` (défaut) : Les rangées occupent tout l’espace disponible
- `flex-start`
- `flex-end`
- `center`
- `space-between` : les rangées sont séparées avec de l’espace entre elles
- `space-around` : idem, mais il y a aussi de l’espace au début et à la fin

## Propriétés des items

Dès qu’un élément devient un flex-item, il n’est plus considéré comme un block ou un inline classique. Les valeurs de display autre que none ainsi que certaines propriétés comme `float` ou `vertical-align` n’ont plus d’effet sur lui.

### Ordre des éléments

La propriété `order` appliquée à chaque élément permet de modifier leur ordre sans changer le code HTML

La valeur doit être un nombre entier indiquant l’ordre (valeur de la moins forte à la plus forte). La valeur initiale est zéro. On peut utiliser des valeurs negatives (les éléments s’afficheront en priorité). Si plusieurs élément on la même valeur, l’ordre est le même que dans le code HTML

```css
.element:nth-child(1) {
	order: 3;
}
.element:nth-child(2) {
	order: 1;
}
.element:nth-child(3) {
	order: 2;
}
```

### Alignement propre à un élément

`align-self` : permet d’aligner un élément sur l’axe secondaire de manière différence que les autres éléments frères. Utilise les même valeurs que la propriété `align-items` ainsi que la valeur `auto`qui est la valeur par défaut (l’élément garde l’alignement général)

```css
#conteneur {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
}

.element:nth-child(2)  {
	/* Seul ce bloc sera aligné à la fin */
	background-color: blue;
	align-self: flex-end; 
}
```

### Élargir ou rétrécir un élément

`flex-grow` : élargir l’élément de sorte à ce qu’il occupe l’espace libre restant.

Par défaut la valeur est zéro. L’élément s’élargi si on indique une valeur supérieur.

Il est possible de faire élargir plusieurs éléments qui vont se répartir l’espace restant. La répartition se fait en fonction du facteur d’agrandissement.

```css
/* Les deux éléments s'élargit
en prenant tout l'espace restant */

.element:nth-child(2) {
	flex-grow: 1;
}

/* cet élément prend plus d'espace */
.element:last-child {
	flex-grow: 2;
}
```

`flex-shrink` : rétreci un élément s’il n’y a pas suffisant d’espace au sein du conteneur

La valeur par défaut est 1, ce qui signifie que par défaut les éléments sont automatiquement rétréci.

### Taille d’un élément

`flex-basis` : taille (en px, % …) d’un élément (largeur ou hauteur selon l’axe) lorsque `flex-grow` et `flex-shrink` ont une valeur nulle

- `auto` (défaut) : la taille de l’élément est définie par son contenu

Si la valeur de `flex-grow` n’est pas nulle, la taille indiquée représente une taille minimale.

Si la valeur de `flex-shrink` n’est pas nulle, la taille indiquée représente une taille maximale

### Super propriété flex

Regroupe les propriétés `flex-grow`, `flew-shrink` et `flex-basis`

Par défaut : `flex: 0 1 auto;`

### Les priorités

- `min-width` et `max-width` sont prioritaires par rapport aux propriétés `width`,`flex-grow`, `flex-shrink`, `flex-basis` et `flex-wrap`
- `flex-wrap` est prioritaire sur `flex-shrink`
- `flex-grow` et `flex-shrink` sont prioritaires sur `flex-basis`
- `flex-basis` est prioritaire sur `width`

Classement par ordre de priorité :

1. `min-width`/`min-height`
2. `max-width`/`max-height`
3. `flex-wrap`
4. `flex-grow`/`flex-shrink`
5. `flex-basis`
6. `width`/`height`

## Astuces flexbox

### Deux blocs côte à côte

```css
.container {
	display: flex;
}

.item1 {
	width: 10em;
}

.item2{
	flex-grow: 1; 
}
```

Le premier bloc a une largeur fixé en em. Il s’agit d’une indication de largeur maximale du fait du `flex-shrink` qui a par défaut a une valeur de 1

Le deuxième occupe l’espace restant grace à `flex-grow: 1`

Les deux blocs prennent la même hauteur du fait que `align-items` a pour valeur par défaut `stretch`.

Pour que chaque bloc prennent une hauteur en fonction de leur contenu il faut indiquer dans le conteneur `align-items: flex-start`

### Centrer un élément

Pour centrer un élément au sein de son conteneur on peut lui indiquer des marges automatiques

```css
#conteneur { 
	display: flex;
}
.element {
	margin: auto;
}
```

Cela équivaut à faire

```css
	#conteneur {
	display: flex;
	justify-content: center;
	align-items: center;
}
```

Si le conteneur contient plusieurs éléments et que l’on applique des marges automatiques à chaque élément, cela équivaut à :

```css
#conteneur {
	display: flex;
	justify-content: space-around;
	align-items: center;
}
```

### Pousser un élément

Pousser l’élément vers la droite : `margin-left: auto;`

Vers le haut : `margin-bottom: auto;`

Vers le bas : `margin-top: auto;`

```css
#conteneur { 
	display: flex;
}

.element {
	margin-top: auto;
	margin-left: auto;
}
```

équivaut à :

```css
#conteneur {
	display: flex;
	justify-content: flex-end;
	align-items: flex-end;
}
```

Cela peut être utile par exemple pour pousser un élément `footer` tout en bas de son conteneur
