# CSS - centrer des éléments

## Centrer horizontalement

### Centrer horizontalement un élément de type inline ou du texte dans un bloc

```css
/* utiliser sur le parent */
text-align: center
```

### Centrer horizontalement un élément de type bloc ou table par rapport à son parent

```css
margin: auto;
```

Les marges gauche et droite prendront une taille automatique égale ce qui aura pour effet de centrer le bloc

## Centrer verticalement

### Center verticalement un élément dans un container flex

Deux possibilités :

- on indique sur l’élément enfant d'un container Flex un `margin: auto` ce qui permet de centrer à la fois horizontalement et verticalement.
- Sinon on utilise les propriétés Flexbox habituelles pour centrer

### Centrer verticalement une ligne de texte sans Flexbox

Utiliser sur le parent la propriété `line-height` qui doit avoir la même valeur que celle de la propriété `height`

```css
/* hauteur du parent */
height: 20em;
/* hauteur de ligne (identique) */
line-height: 20em;
/* interdiction de passer à la ligne */
white-space: nowrap;
```

Inconvénients : Ne fonctionne que sur une seule ligne et nécessite une hauteur de parent définie  
**Cette méthode est obsolète avec les Flexbox**

## Centrer les éléments en position absolu

Utilisation de la technique `translate`

```css
.container { /* Parent */
	border: 1px solid black;
	width: 500px;
	height: 500px;
	position: relative; /* pour que l'enfant se positionne par rapport à son container et non pas la fenêtre */

}

.box { /* enfant */
	height: 200px;
	width: 200px;
	background-color: red;
	position: absolute;
	/* permet de centrer horizontalement et verticalement dans le container */
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%); /* % par rapport aux dimensions de l'élement enfant */
}
```
