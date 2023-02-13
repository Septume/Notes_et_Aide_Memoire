# Grid layout

Module permettant de créer des grilles

## Vocabulaire

- **grid container** : élément parent utilisé pour contenir la grille
- **grid items** : éléments enfants positionnés sur la grille
- **grid line** : lignes constituant la grille.
- **grid track** : plage de grille. Correspond à une colonne (**column**) ou une rangée (**row**)
- **grid cell** : cellule
- **grid area** : zone de la grille délimitée par 4 lignes et comportant n’importe quel nombre de cellules

## Création du container

### Création de la grille

Propriété `display`

- `grid` : créé une grille avec un comportement block
- `inline-grid` : créé une grille avec un comportement inline

Remarque : `column`, `float`, `clear` et `vertical-align` n’ont aucun effet sur un container grid.

### Définition des colonnes et rangées

`grid-template-columns` : Permet de définir les colonnes via une liste de valeurs séparées par un espace

`grid-template-rows` : idem mais pour les rangées

Pour ces deux propriétés on indique plusieurs valeurs, chacune spécifiant la largeur d’une colonne ou la hauteur d’une rangée. On peut indiquer une taille en px, % ou en fr (valeur fractionnaire)

`grid-column-gap` : permet de définir un espacement entre les colonnes (en px ou %)

`grid-row-gap` : idem mais pour les rangées

```css
/* 4 colonnes avec des tailles en px */
grid-template-columns: 400px 200px 200px 100px

/* 2 colonnes avec des tailles en % (par rapport à la largeur du parent)  */
grid-template-columns: 20% 20%

/* 
3 colonnes avec des valeurs fractionnaires.
La largeur disponible est divisée en 5 parts. 
La première colonne fait une part, la seconde 3 parts et la 3ème 2 parts. 
*/
grid-template-columns: 1fr 3fr 2fr;

/*  
2 colonnes avec une valeur en px et une valeur en fr 
La deuxième colonne prend le reste de l'espace disponible 
*/
grid-template-columns: 200px 1fr;
```

## Création des items

### Disposition des éléments

Les éléments vont se placés à partir du premier espace disponible en partant sur la gauche et s’étendent sur une rangée en fonction du nombre de colonnes définies, puis continuent sur la rangée suivante et ainsi de suite.

Le nombre de colonnes et la taille indiquée sont toujours respectés. Ainsi les éléments disposés les uns après les autres sur une rangée ne remplissent pas forcément toute la largeur du parent, de même qu’ils peuvent déborder (créant un scrolling horizontal).

Pour avoir des rangés qui prennent toujours la largeur du parent on utilisera des valeurs fractionnaires

`grid-auto-flow` : permet de spécifier l’orientation dans laquelle sont disposés les éléments

- `row` : les éléments sont disposés par rangée
- `column` : les éléments sont disposés par colonne.

```html
<div class="grid">
	<div class="item1"></div>
	<div class="item2"></div>
</div>
```

```css
.grid {
	display: grid;
	/* grille de 5 colonnes et 4 rangées */
	grid-template-columns: repeat(5, 1fr);
	grid-template-rows : repeat(4, 100px);
	grid-column-gap: 10px;
	grid-row-gap: 10px;
	/* les éléments sont disposés en colonne (les uns sous les autres) */
	grid-auto-flow: column;
}

.item1 {
	background-color: blue;
}

.item2 {
	background-color: green;
}
```

### Positionnement des éléments sur la grille

Les éléments enfants positionnés sont retiré du flux normal et peuvent être superposés. La propriété `z-index` permet de gérer l’ordre d’affichage.

`grid-column-start`: l’élément commence sur le numéro de ligne vertical (lignes des colonnes) indiqué en valeur (correspond au numéro de colonne)

`grid-column-end` : l’élément se termine sur le numéro de ligne vertical (lignes des colonnes) indiqué en valeur (correspond au numéro de colonne - 1)

`grid-row-start` et `grid-row-end` : idem mais pour les rangées

```css
/*
L'élément commence à partir de la 2ème ligne verticale (ligne de colonne) et la 2ème ligne horizontale (ligne de rangée) 
ce qui correspond à la 2ème colonne et la 2ème rangée.
Il s'étend jusqu'à la 5ème ligne verticale et la 4ème ligne horizontale, 
ce qui correspond à la 5ème colonne et la 4ème rangée tout deux non incluses.
En tout ça fait 3 colonnes et 2 rangée soit 6 cellules. 
*/

grid-column-start: 2;
grid-row-start: 2;
grid-column-end: 5;
grid-row-end: 4;
```

`grid-column` et `grid-row` : propriétés raccourcis des précédentes. On sépare les valeurs par un `/`

```css
/*
L'élément est positionné sur la 2ème rangée et s'étend de la 2ème colonne à la 5ème colonne non incluse  (soit 3 colonnes)
 */
grid-column: 2 / 5;
grid-row: 2;
```

`span` : mot clé permettant d’indiqué le nombre de colonnes ou rangées sur lesquelles s’étend l’élément.

```css
/* Exemple 1 */
grid-column-start: 2;
grid-row-start: 2;
grid-column-end: span 3;
grid-row-end: span 2;

/* Exemple 2 */
grid-column: 2 / span 3;
grid-row: 2;
```

### Colonnes et rangées automatiques

Si un élément est positionné sur une colonne ou une rangée qui n’existe pas, celle-ci est automatiquement créé, dont la taille dépend de la hauteur ou largeur que prend le contenu.

`grid-auto-columns` : permet de spécifier la taille des colonnes automatiques

`grid-auto-rows` : même chose mais pour les rangées

```css
.grid {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	grid-template-rows: repeat(2, 100px);
	grid-auto-columns: 1fr;
	grid-auto-rows: 100px;
}

.item {
	background-color: #ccc;
	grid-column-start: 7;
	grid-row-start: 3;
}
```

### Alignement des boites à l’intérieur d’une cellule ou d’une zone

un élément peut avoir des dimensions différentes que la cellule ou la zone qui le contient

```html
<div class="grid">
	<div class="item"></div>
	<div class="item"></div>
</div>
```

```css
.grid {
	width: 400px;
	height: 200px;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	grid-template-rows: repeat(2, 1fr);
}

.item {
	grid-column: span 2;
	grid-row: span 2;
	width: 60%;
	height: 60%;
	border: 1px solid black;
}
```

Il est possible d’indiquer sur le parent comment doit être aligné les éléments

`justify-items` : alignement sur l’axe principal (par défaut celui des rangées. Peut être changé avec `grid-auto-flow`)

`align-items` : alignement sur l’axe secondaire

Les valeurs sont `start` (défaut), `center` et `end`

```css
.grid {
	width: 400px;
	height: 200px;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	grid-template-rows: repeat(2, 1fr);
	justify-items: center;
	align-items: end;
}

.item {
	grid-column: span 2;
	grid-row: span 2;
	width: 60%;
	height: 60%;
	border: 1px solid black;
}
```

On peut également indiqué un alignement pour chaque enfant avec `justify-self` et `align-self`

```css
.grid {
    width: 400px;
    height: 200px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(2, 1fr);
}

.item {
	grid-column: span 2;
	grid-row: span 2;
	width: 60%;
	height: 60%;
	border: 1px solid black;
}

.item1 {
	justify-self: center;
	align-self: center;
}

.item2 {
	justify-self: end;
}
```

## Nommer des zones de la grille

`grid-template-areas` : permet de définir des zones de grille nommées. compatible avec les autres propriétés ( `grid-column-start`, etc…)

```css
.container {
	display: grid;
	grid-template-areas:
		"header header"
		"content aside"
		"footer footer";
}
```

Un ligne est créée pour chaque chaîne. Une colonne est créée par mot de la chaîne. un mot répété permet d’étendre une cellule sur une ligne ou/et colonne.

Il est nécessaire que ces cellules forment un rectangle, sinon, la déclaration est invalide

On utilise ensuite la propriété `grid-area` sur les éléments enfants pour indiquer la zone de la grille sur laquelle se positionner.

```html
<div class="page">
	<header>En-tête</header>
	<nav>Navigation</nav>
	<main>Zone principale</main>
	<footer>Pied de page</footer>
</div>
```

```css
body {
	margin: 0;
}

.page {
	height: 100vh;
	display: grid;
	grid-template-areas:
		"header header"
		"nav  main"
		"footer footer";
	grid-template-rows: 50px 1fr 50px;
	grid-template-columns: 150px 1fr;
}

header {
	grid-area: header;
	background-color: #8ca0ff;
}

nav {
	grid-area: nav;
	background-color: #ffa08c;
}

main {
	grid-area: main;
	background-color: #ffff64;
}

footer {
	grid-area: footer;
	background-color: #8cffa0;
}
```

## Fonction minmax()

Permet de définir une intervalle de taille pour les propriétés :

- `[grid-template-columns](<https://developer.mozilla.org/fr/docs/Web/CSS/grid-template-columns)>`
- `[grid-template-rows](<https://developer.mozilla.org/fr/docs/Web/CSS/grid-template-rows)>`
- `[grid-auto-columns](<https://developer.mozilla.org/fr/docs/Web/CSS/grid-auto-columns)>`
- `[grid-auto-rows](<https://developer.mozilla.org/fr/docs/Web/CSS/grid-auto-rows)>`

La fonction prend deux valeurs pour indiquer la taille minimale et la taille maximale (toutes deux comprises dans l'intervalle)

Les valeurs peuvent être :

- Une longueur en px, em ou % (relatif à la taille de la grille)
- une unité fractionnaire (fr)
- `max-content`
- `min-content`
- `auto`

Exemple

```css
grid-template-columns: minmax(200px, 50%) 1fr 1fr;
```
