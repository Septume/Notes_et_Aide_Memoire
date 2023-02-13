# Positionnement et flottants

## Positionnement

Propriété `position` :

- `static` : valeur par défaut. Position normale (Les propriétés `top`, `right`, `bottom`, `left` et `z-index` ne s’appliquent pas)
- `relative` : permet de décaler un élément par rapport à sa position normale
- `absolute` : permet de retirer l’élément de sa position normale (l'élément sort du flux normal) pour le placer n’importe où sur la page
- `fixed` : variante de la position absolue où l’élément reste fixe lors d’un scrolling
- `sticky` : mix entre le positionnement relatif et fixe

### Le positionnement relatif

L’élément est décalé par rapport à son point d’origine en haut à gauche. L’élément déplacé laisse toujours un espace à l’endroit de son emplacement initial, le reste du contenu n’est donc pas ajusté.

Les propriétés `left`, `right`, `top` et `bottom` permettent d’indiquer le décalage

```css
/*  décalage de 10px vers la droite et le bas */
position: relative;
left: 10px;
top: 10px;
```

On utilise le positionnement relatif pour :

- servir de référent à un élément enfant positionné en absolu
- faire de la superpositions d’éléments en utilisant la propriété `z-index`

### Le positionnement absolu et fixe

l’élément sort du flux normal :

- il ne laisse aucun espace à l’endroit de sa position initiale
- il ne dépend plus des autres éléments
- il ne prend plus la largeur de son parent mais celui de son contenu

Le positionnement absolu se fait par rapport au parent si ce dernier est lui-même positionné (en relatif ou absolu), sinon il se fait par rapport au premier ancêtre positionné rencontré ou le cas échéant à la page entière.

Le positionnement fixe est similaire au positionnement absolu sauf que l’élément est positionné par rapport à la fenêtre du navigateur. L’élément reste toujours à la même place si on fait défiler la page

```html
<div id="div1">
	<div id="div2">
		<div id="div3">
		</div>
	</div>
</div>
```

```css
#div1 {
	background-color: black;
	width: 100px;
	height: 100px;
}

#div2 {
	background-color: red;
	width: 100px;
	height: 100px;
	position: relative;
	/* la div est décalé de 20px vers le bas
	et de 20 px vers la droite
	*/
	top: 20px;
	left: 20px;
}

#div3 {
	background-color: blue;
	width: 50px;
	height: 50px;
	position: absolute;
	/* la div est placé à 5px du bas 
	de son conteneur parent 
	et à 5px de la droite */
	bottom: 5px;
	right: 5px;
}
```

Resultat

![](positionnement.png)

### Le positionnement sticky

Dans un premier temps l’élément est positionné de manière relative. Par la suite, lors du défilement de la page (ou du conteneur disposant d’un mécanisme de scrolling ) l’élement prendra une position fixe dès qu’un certain seuil sera franchi. Les propriétés `top`, `left`, `bottom` et `right` permet de fixer ce seuil

```css
/* l'élément devient fixe dès qu'il est à moins de 10 pixels du haut de la page */
#block{  
	position: sticky; 
	top: 10px; 
}
```

Pour que le positionnement sticky fonctionne il faut que le parent :

- ai une taille fixe
- ai un mécanisme de scroll
- soit en position relative ?

## Empilement des éléments

Propriété `z-index` : Permet d’indiquer un ordre d’ empilement

- La valeur doit être un nombre entier et peut être négative
- Les valeurs les plus élevées sont au premier plan, et les plus faibles sont au second plan.

Attention : cette propriété fonctionne uniquement sur un élément positionné (relatif, absolu ou fixe)

```html
<div class="box box1"></div>
<div class="box box2"></div>
```

```html
.box {
	width: 100px;
	height: 100px;
}

.box1 {
	background-color: red;
	position: relative;
	z-index: 1;
}

.box2 {
	background-color: blue;
	position: relative;
	top: -50px;
	left: 50px;
}
```

Résultat

![](z_index.png)

## Flottant

Un élément flottant :

- est retiré du flux normal pour être placé tout à gauche ou à droite de son conteneur
- prend la largeur de son contenu.
- n’existe pas pour son élément parent. Si un élément parent contient que des éléments flottants, il s’effondre comme s’il était vide

Un élément flottant cherchera toujours à se positionner le plus près possible du haut de l’élément parent, mais si un élément frère (de type inline ou block) a été défini préalablement, il repoussera le flottant vers le bas

Les éléments suivants le flottant sont affectés par ce positionnement :

- le texte et les éléments inline entourent l’élément flottant
- Les autres éléments block se repositionnent dans le flux normal pour occuper l’espace rendu libre.

### Rendre un élément flottant

Propriété `float` :

- `left`
- `right`

Cette propriété fonctionne sur un élément de type block. Si l’élément est de type inline ou autre il sera alors automatiquement transformé en block. A noter que float n’a pas d’effet sur un élément flex

### Annuler les effets d’un flottant

Pour que les éléments suivants ne soient plus affectés par le flottant, on utilise la propriété `clear`

- `left` : l’élément se poursuit en-dessous des éléments flottant à gauche
- `right` : l’élément se poursuit en-dessous des éléments flottant à droite
- `both` : l’élément se poursuit en-dessous de éléments flottants à gauche et à droite
- `none` : défaut

```html
<h2>Exemple de float</h2>

<div class="box"></div>

<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolorum expedita ea amet deleniti veritatis quae molestias voluptatem itaque voluptates delectus, impedit ex. Provident deserunt odio, adipisci quas. Dicta neque, nisi!</p>

<h2 class="clear">Autre titre</h2>

<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptates eaque ab, quasi non laudantium expedita vel ducimus inventore dignissimos totam, delectus maxime quidem sit! Voluptas fuga quas obcaecati? Culpa, repellendus. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusantium aliquid adipisci obcaecati vel eos delectus non dolore rerum, repellat ad nobis unde reiciendis vero totam dolorum a eligendi nemo, quasi. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Earum suscipit rem corrupti culpa aliquam distinctio sed dolores ea tempore placeat exercitationem saepe repellendus minus alias deleniti provident, repudiandae, officiis accusantium?</p>
```

```css
box {
	width: 100px;
	height: 100px;
	background-color: red;
	float: left;
	margin: 0 1em 1em 0;
}

/* le deuxième titre et le texte continu sous le flottant */
.clear {
	clear: left;
}
```

### Techniques “clearflix”

Permet de fixer le problème de l’élément parent qui perd sa hauteur.

On peut utiliser un contexte de formatage block en utilisant `overflow: hidden`

Inconvénient: lorsqu’on veut faire dépasser certains éléments du conteneur (par exemple un contenu court ou un élément de décoration), le `overflow:hidden` est gênant car il masque tout ce qui dépasse.

```html
<div class="container">
	<div class="float"></div>
	<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit</p>
</div>
```

```css
.container {
	border: 1px solid black;  
	overflow: hidden; 
}

.float {
	width: 200px;
	height: 200px;
	background: red;
	float: left;
	margin-right: 10px;
}
```

On peut aussi placer un élément vide juste avant la balise fermante du conteneur et on lui applique un `clear:both`

Attention : `Clear` fonctionne qu’avec un élément en display block

```html
<div class="container">
	<div class="float"></div>
	<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit</p>
	<div class="clear"></div>
</div>
```

```css
.container {
	border: 1px solid black;
}

.float {
	width: 100px;
	height: 100px;
	background-color: red;
	float: left;
	margin-right: 10px;
}
.clear {
	clear: both;
}
```

On peut utiliser la précédente technique sans avoir besoin d’ajouter un élément vide dans le code HTML Pour cela on simule cet élément avec le pseudo-élément `::after`

```html
<div class="container">
	<div class="float"></div>
	<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit</p>
</div>
```

```css
.container {
	border: 1px solid black;
}

.container::after {
	content: ""; /* Important, sinon l'élément n'est pas généré. */
	display: block;
	clear: both;
}

.float {
	width: 100px;
	height: 100px;
	background-color: red;
	float: left;
	margin-right: 10px;
}
```
