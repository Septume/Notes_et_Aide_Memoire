# Imbrication

Le SCSS permet d'imbriquer les sélecteurs afin d'avoir une organisation du code plus hiérachique.

### Imbrication des sélecteurs descendants

```scss
/* code CSS */

.container {
	width: 100%;
  color: grey;
}

.container div { Border: 1px solid black; }
.container div a {
  text-decoration: none;
  color: #f2f2f2;
}

/* Equivalent en code SCSS avec imbrication des sélecteurs */
.container {
  width: 100%;
  color: grey;
	div {
		border: 1px solid black;
		a {
      text-decoration: none;
      color: #f2f2f2;
		}
  }
}
```

### Utilisation des combinateurs

SASS prend en charge les combinateurs `>` , `+` et `~`

```scss
/*code CSS */
h1 ~ pre { margin-top: .5em; }

/*Code SCSS */
h1 {
	~ pre { margin-top: .5em; }
}

```

### Imbrication avec des groupes de selecteurs

Exemple 1

```scss
/* code CSS */
.resume h1, resume h2, resume h3 { color: grey; }

/*code SCSS */
.resume{
	h1,h2,h3 { color: grey; }
}

```

Exemple 2

```scss
/* code CSS */
.resume a, .footer a { text-decoration: none; }

/*code SCSS */
.resume, .footer {
	a { text-decoration: none; }
}
```

### Symbole &

Le symbole `&` permet de faire référence au sélecteur parent de l'imbrication. Lors de la compilation le `&` sera remplacé par le parent

Exemple avec l'utilisation d'une pseudo classe

```scss
/* code CSS */
a { text-decoration: none }
a:hover { text-decoration: underline; }

/* code SCSS */
a {
	text-decoration: none
	&:hover { text-decoration: underline; }
}

/* 
	remarque : si on enlève le & le :hover n'est plus lié à l'élément a lors de la compilation
		a :hover
	Ce qui revient à écrire 
		a *:hover
 */ 

```

Autre exemple d'utilisation

```scss
/*code CSS */

.btn {
	background: gray;
}

.dark-theme .btn {
	backgeround: white;
}

/* code SCSS */

.btn {
	background: gray;
	.dark-theme & {
		backgeround: white;
	}
}
```

Exemple en utilisant la méthode de nommage BEM

```scss
/* code CSS */
.block {
  background-color: #15DEA5;
}
.block__element {
  color: #fff;
}
.block__element--modifier {
  background-color: #001534;
}

/*code SCSS*/

.block{
  background-color: #15DEA5;
  &__element {
		color: #fff;
		&--modifier {
			background-color: #001534;
	  }
  }
}
```

### Imbrication de media queries

```scss
/* code CSS */

h1 {
    font-size: 3.5rem;
}

@media (max-width: 950px) {
	h1 {
		font-size: 2.5rem;
  }

/*code SCSS */

h1{
  font-size: 3.5rem;
  @media (max-width: 950px) {
      font-size: 2.5rem;
  }
}

```

Il est possible d'imbriquer des media queries les un dans les autres. Ces derniers seront combinés via l'opérateur `and`

```scss
.hero {
	width: 960px;
	max-width: 100%;
	min-height: 220px;

	@media only screen {
		@media (min-width: 1400px) {
			width: 1400px;
			max-width: 1400px;
		}

		@media (max-width: 450px) {
			max-height: 300px;
			img {
				max-height : 268px;
			}

		}
}

// résultat CSS

.hero {
	width: 960px;
	max-width: 100%;
	min-height: 220px;
}

@media only screen and (min-width: 1400px) {
	.hero {
		width: 1400px;
		max-width: 1400px;
	}
}

@media only screen and (max-width: 450px) {
	.hero {
		max-height: 300px;
	}
	.hero img {
		max-height : 268px;
	}
}
```

Remarque : Afin d'éviter les effets de bord lié à la cascade, les média queries de même nature ne seront pas regroupés dans le code CSS.

```css
/* les media queries de même type 
ne sont pas regroupés dans le fichier CSS */

@media only screen and (min-width: 600px) {
	.notice {}
}

@media only screen and (min-width: 600px) {
	.error {}
}
```

### Propriétés imbriquées

Il est possible d'utiliser l'imbrication pour les propriétés utilisant le même préfixe.

```scss
/* code CSS */

.baseline {
  font-family: sans-serif;
  font-size: 1em;
  font-weight: bold;
  font-variant: small-caps;
}

/* Code SCSS. Ne pas oublier les deux-points après le préfixe */ 

.baseline {
  font: {
	  family: sans-serif;
	  size: 1em;
	  weight: bold;
	  variant: small-caps;
  }
}
```

### Limite de l'imbrication

L'imbrication donne la possibilité de reproduire la hiérachie des éléments du documents HTML mais ce n'est pas une bonne pratique car :

- Le code CSS est dépendant de la hiérachie du document HTML
- Cela créé des selecteurs CSS trop spécifiques

**Il est fortement recommandé de ne pas utiliser plus de 4 niveaux d'imbrication**
