# Héritage

Le mot clé `@extends` permet d'hériter des propriétés d'un selecteur simple (classe, élément,…).

Lors de la compilation les selecteurs seront regroupés avec celui dont ils héritent.

Il est possible de faire de l'héritage en chaine

```scss
/* code SCSS */

.message {
	border: 2px solid black;
}

.alerte {
    @extend .message;
    color: red;
}
.danger {
    @extend .alerte;
    font-size: xx-large;
}

/* résultat CSS */

.message, .alerte, .danger {
	border: 2px solid black;
}

.alerte, .danger {
    color: red;
}
.danger {
    font-size: xx-large;
}
```

### Placeholders

Il s'agit d'un selecteur spécial qui ne sert qu'à l'héritage et qui ne sera pas inclus dans le code CSS

On utilise la syntaxe `%nom-selecteur`

```scss
/* code SCSS */

%message {
	border: 2px solid black;
}

.warning {
		@extend %message;
    background-color: yellow;
}
.danger {
	@extend %message;
	background-color: red;
}

/* résultat CSS */

.warning, .danger {
  border: 2px solid black;
}
.warning {
  background-color: yellow;
}
.danger {
  background-color: red;
}
```

### Limite de l'héritage

L'héritage sera appliquée sur toutes les occurences du selecteur, quel que soit le contexte, ce qui peut créer des selecteurs indésirables pouvant entrainer des effets de bord

```scss
// code SCSS 

.important {
    color: red;
}

.error {
    @extend .important; 
}

/* ici on applique un style à un élément .important contenu dans un élément .success */
.success .important {
    color: green;
}

// Résultat CSS

.important, .error {
  color: red;
}

/* 
SASS génère des selecteurs qui n'ont pas de sens par rapport au code HTML
Un element .error n'est jamais enfant d'un élement .success 
*/

.success .important, .success .error {
  color: green;
}
```

De plus l'héritage fonctionne mal quand on l'utilise avec des media queries pouvant provoquer des erreurs lors de la compilation.

**Il est donc recommandé de ne pas utiliser l'héritage et de privilégier plutôt l'utilisation des mixins**

 margin-top: $size-base * 2;

 margin-bottom: $size-base;
