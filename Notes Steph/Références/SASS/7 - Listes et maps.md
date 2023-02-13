# Listes et maps

### Listes

Permet de spécifier plusieurs valeurs pour une variable. Les valeurs peuvent être séparées par des espaces ou des virgules.

`nth($list, $index)` : Fonction qui permet d'accéder à une valeur d'une liste. **Attention : La numérotation de l'index commence à 1.**

```scss
$font-size: 7rem 5rem 4rem 2rem;
.element {
		font-size: nth($font-size, 4); // 2rem
}
```

### Maps

Liste de paire clé/valeur.

Syntaxe : `(key1: value1, key2: value2,…)`

On doit indiquer le contenu de la liste entre parenthèses et les paires doivent être séparées par une virgule.

`map-get($map, key)` : Fonction qui permet d'accéder à une valeur d'une map

```scss
$font-size: (
	logo:7rem,
	heading:5rem, 
	project-heading:4rem,
	label:2rem
);

.element {
		font-size: map-get($font-size, label);
}
```

On peut utiliser des map imbriqués

```scss
$colour-primary: #15DEA5;
$colour-white: #fff;
$colour-invalid: #DB464B;
$txt-input-palette: (
	focus: (
      bg: $colour-primary,
      txt: $colour-white
  ),
  invalid: (
      bg: $colour-invalid,
      txt: $colour-white
  )
);
```
