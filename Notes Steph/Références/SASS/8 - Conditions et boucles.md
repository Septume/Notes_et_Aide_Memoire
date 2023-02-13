# Conditions et boucles

### Opérateurs de comparaison

- `==`
- `!-`
- `<` et `<=`
- `>` et `>=`

Remarque :

- La comparation d'égalité prend en compte le type de donnée (`10 != "10"`)
- La comparation d'égalité entre deux couleurs identiques donne `true` même si la notation est différente
- La comparaison entre les chaine de caractères est sensible à la casse

On peut également utilisé les opérateurs logique `and` et `or`

### Conditions

Pour utiliser les conditions ont utilise les directives `@if`, `@else if` et `@else`

```scss
@mixin heading-shadow($colour: $colour-primary, $size: $heading-shadow-size){
  @if ( lightness($colour) < 25% ) {
      $colour: lighten($colour, 10%);
  }@else{
      $colour: darken($colour, 10%);
  }
  text-shadow: $size $size $colour;
}
```

### Boucles

**Boucle for**

On utile la syntaxe : `@for $i from <number> through <number>`

```scss
@for $i from 1 through 3 {
	.section-#{$i} {
		background-image: url('img/bg-' + $i + '.png');
   }
}
```

**Boucle each**

Permet de parcourir une liste ou une map

Syntaxe :

- Pour une lliste : `@each <$item> in <$list>`
- Pour une map : `@each <$key>, <$item> in <$list>`

```scss

// Exemple avec une liste 

$sections: "presentation", "production", "contact";

@each $section in $sections {
	.section-#{$section} {
			background-image: url('img/bg-' + #{$section} + '.png');
   }
}

// Exemple avec une map 

$medias: (
  small: 1rem,
  medium: 5rem,
  large: 10rem
);

@each $media, $size in $medias {
  .btn--#{$media} {
      font-size: $size;
  }
}
```
