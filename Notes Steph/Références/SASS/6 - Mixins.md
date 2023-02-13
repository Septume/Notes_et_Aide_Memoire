# Mixins

Permet de réutiliser un ensemble de règles

### Définir un mixin

 Pour définir un mixin ou utilise la directive `@mixin` et pour l'appeler la directive `@include`

```scss
@mixin heading-shadow {
  text-shadow: .55rem .55rem #fff;
}

.form {
  &__heading {
      @include heading-shadow;
  }
}

/* résultat CSS */
.form__heading {
  text-shadow: 0.55rem 0.55rem #fff;
}
```

Le corps de la mixin peut aussi contenir des règles CSS

```scss
@mixin no-bullets {
	list-style: none;
	li {
		list-style-image: none;
		list-style-type: none;
		margin-left: 0;
	}
}

ul, ol {
	padding: 0;
	@include no-bullets; 
}

// SCSS intermédaire

ul, ol {
	padding: 0;
	list-style: none;
	li {
		list-style-image: none;
		list-style-type: none;
		margin-left: 0;
	}
}

// Résultat CSS

ul, ol {
	padding: 0;
	list-style: none;
}

ul li, ol li {
	list-style-image: none;
	list-style-type: none;
	margin-left: 0;
}
```

Remarque : Si on apelle plusieurs fois le même mixin dans des selecteurs différents, ces derniers ne seront pas regroupés comme dans le cas de l'héritage. Le code sera juste dupliqué à plusieurs endroit.

### Utilisation d'arguments

```scss
@mixin heading-shadow($colour) {
  text-shadow: .55rem .55rem $colour;
}

.form {
  &__heading {
      @include heading-shadow(#fff);
  }
}
```

### Valeur par défaut

```scss
/* on peut aussi mettre une variable
 comme valeur par défaut */
@mixin heading-shadow($colour: #fff){
  text-shadow: .55rem .55rem $colour;
}

.form {
  &__heading {
			/* l'absence d'argument permet 
			d'utiliser la valeur par défaut */
      @include heading-shadow;
  }
}
```

Remarque : Si on utilise `null` comme valeur par défaut et que l'on passe cet argument à une propriété celle ci sera exclue du fichier CSS lors de la compilation

### Arguments nommés

Permet de ne pas respecter l'ordre des paramètres lors du passage des arguments.

```scss
/* def mixin */
@mixin element($color: dark, $background-color: white) {}

/* inclusion 
$color = dark (défaut)
$background-color = red
*/
@include element($background-color: red);
```

### Liste d'arguments

Certaines propriétés comme `background` peuvent prendre un nombre de valeurs illimités. On doit donc besoin d'utiliser pour le mixin une liste d'arguments dont le nombre n'est pas défini. Pour cela on utile la notion `$args..`.

```scss
@mixin background($backgrounds...) {
	background: $backgrounds;
}
```

Attention : Une liste d'argument doit toujours être déclarée en dernière position.

### Bloc de contenu

Il est également possible de passer un bloc de contenu à un mixin. Pour cela on indique dans le corps de définition de la mixin la directive `@content` . Le contenu passé à la mixin sera inséré à la place du `@content`

```scss
@mixin medium-screen {
	@media (max-width: 950px) {
		@content;
	}
}

h1{
    font-size: 3.5rem;
    @include medium-screen {
				/* contenu inséré à la place du @content */
        font-size: 2.5rem;
    }
}

/*Résultat après compilation */ 

h1 {
    font-size: 3.5rem;
}

@media (max-width: 950px) {
	h1 {
		font-size: 2.5rem;
  }

```
