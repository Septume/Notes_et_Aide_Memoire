# Media queries

L’attribut `media` de `<link>` permet de charger un fichier CSS spécifique à un média

```html
<link rel="stylesheet" media="screen and (max-width: 1280px)" href="file.css" />
```

On indique aussi une feuille CSS standard sans media qui sera utilisé par défaut

On peut également utiliser les media queries au sein du même fichier avec le mot clé `@media`

```css
@media screen and (max-width: 1280px) {
	/* propriétés CSS  */
}
```

Les règles disponibles :

- `screen`
- `print`
- `speech` (Synthèse vocale)
- `all`
- `width` et `height`
- `device-width` et `device-height`
- `aspect-ratio`: Ratio entre la largeur et la hauteur du viewport (ex : 8/5)
- `orientation`
	- `portait`
	- `landscape`

On peut rajouter le préfixe `min-` ou `max-` devant la plupart des règles

Les règles peuvent être combinées à l’aide ds mot clé `only` , `and` et `not`

Breaking-points : Point de rupture. Différents paliers, qui une fois franchis, “cassent” le design de la page. En général, on retrouve 4 breaking-points

- Écran smartphone (< 768 px)
- Tablettes (768 px - 991 px)
- Ordinateurs (992 px - 1199 px)
- Grands écrans d’ordinateurs et télévisions (> 1199 px)
