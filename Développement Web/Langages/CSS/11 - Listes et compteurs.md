# Listes et compteurs

## Styles pour les listes

`list-style-position` : position de la puce ou du marqueur de l’élément

- `inside` : à l’intérieur du bloc de l’élément
- `outside` : à l’extérieur du bloc de l’élément (Défaut)

![](liste_position.png)

`list-style-type` : style de la puce ou de la numérotation

- Pour les listes à puce
	- `disc` : disque plein (par défaut)
	- `circle` : cercle vide
	- `square` : carré plein
	- `none`
- Pour les listes ordonnées :
	- `decimal` : nombres (défaut)
	- `decimal-leading-zero` : nombres commençant par zéro (01, 02 …)
	- `upper-roman` : numérotation romaine, en majuscules
	- `lower-roman` : numérotation romaine, en minuscules
	- `upper-alpha` : numérotation alphabétique, en majuscules
	- `lower-alpha` : numérotation alphabétique, en minuscules

`list-style-image` : permet d’indiquer une image personnalisée de puce. L’image doit avoir une taille d’environ 15x15 px (Si elle est trop grande, elle risque d’être coupée). La valeur `none` permet d’indiquer aucune image.

```css
list-style-image: url("image.png")
```

`list-style` : Propriété raccourcie. Peut prendre un, deux ou trois mots-clés, dans n’importe quel ordre. . Si `list-style-type` et `list-style-image`sont tous les deux définis, `list-style-type` sera utilisé si l’image est indisponible

Remarque : on peut également utiliser le pseudo élément `::before` pour générer un puce personnalisée et la positionner comme on le souhaite

```css
li:before {
	content: "→ ";
}
```

## Compteurs css

Permet de créer une numérotation automatisée

`counter-reset`: créer ou réinitialiser un compteur CSS (actif à partir de l’élément où il est déclaré). On indique comme valeur un nom pour le compteur. On peut également indiquer comme deuxième valeur facultative un nombre entier (positif ou négatif) correspondant à valeur d’initialisation du compteur (Par défaut `0`). Si on a besoin de créer plusieurs compteurs il faut indiquer en valeur plusieurs noms suivis on non d’une valeur initialisation

```css
/* un compteur "foo" qui est initialisé à 1 et un compteur "bar" qui est initialisé à 0 */
counter-reset: foo 1 bar;
```

`counter-increment`: incrémenter un compteur dont le nom est indiqué en valeur. On peut également indiquer comme deuxième valeur facultative un nombre entier (positif ou négatif) correspondant à valeur d’incrémentation (Par défaut `1`). Si besoin on peut indiquer plusieurs compteurs.

```css
/* le compteur "foo" est incrémenté de 1 et le compteur "bar" de 2 */
counter-increment: foo bar 2;
```

Pour récupérer la valeur d’un compteur on utilise la fonction `counter()` qui prend en paramètre le nom du compteur. On peut également indiquer en deuxième paramètre le style du compteur. La valeur retournée par la fonction doit être affichée avec la propriété `content`

Exemple 1

```html
<h1>Titre principal</h1>

<h2>Titre</h2>
<h3>Sous titre</h3>
<h3>Sous titre</h3>

<h2>Titre</h2>
<h3>Sous titre</h3>
<h3>Sous titre</h3>
```

```css
body {
	counter-reset: titles;
}

h2 {
	counter-reset: subtitles;
}

h2::before {
	counter-increment: titles;
	content: counter(titles) ". "
}

h3::before {
	counter-increment: subtitles;
	content: counter(titles) "."counter(subtitles) ") ";
}
```

![](compteur.png)

Exemple 2

```html
<ol>

	<li>item
		<ol>
			<li>item</li>
			<li>item</li>
			<li>item</li>
		</ol>
	</li>

	<li>item
		<ol>
			<li>item</li>
			<li>item</li>
			<li>item</li>
		</ol>
	</li>

</ol>
```

```css
ol {
	list-style-type: none;
	counter-reset: numerotation;
}
```

![](compteur_2.png)

En plus de la fonction `counter()` il existe la fonction `counters()`. Cette dernière permet dans le cadre d’éléments avec des niveaux imbriqués, d’ajouter la numérotation des niveaux supérieurs. Cette fonction doit prendre en deuxième paramètre une chaine de caractère servant de séparateur entre les compteurs. On peut également indiquer un troisième paramètre facultatif pour préciser le style des compteurs

Exemple

```html
<ol>
	<li>item
		<ol>
			<li>item
				<ol>
					<li>item</li>
					<li>item</li>
				</ol>
			</li>
			<li>item
				<ol>
					<li>item</li>
					<li>item</li>
				</ol>
			</li>
		</ol>
	</li>
	<li>item
		<ol>
			<li>item
				<ol>
					<li>item</li>
					<li>item</li>
				</ol>
			</li>
			<li>item
				<ol>
					<li>item</li>
					<li>item</li>
				</ol>
			</li>
		</ol>
	</li>
</ol>
```

```css
ol {
	list-style-type: none;
	counter-reset: numerotation;
}

li::before {
	counter-increment: numerotation;
	content: counters(numerotation, ".") " - ";
}
```

![](compteur_3.png)
