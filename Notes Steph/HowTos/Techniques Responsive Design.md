# Techniques Responsive Design

## Mobile first 
### Pourquoi faire du mobile-first ?
Sur mobile la structure du site est plus simple ce qui nécessite moins de règle CSS.
Si on commence par le desktop on sera obligé d'écraser beaucoup de règles  lorsqu'on utilisera les media queries pour les plus petits écrans.
En commençant par le mobile, on défini d'abord les règles de base sur lesquelles on n'aura pas besoin de revenir pour la version desktop

### Comment faire du mobile-first
On écrit d'abord les règles pour les mobiles => règles de base
On utiliser les media-queries et `min-width` pour les autres écrans
Remarque : si on souhaite faire du desktop-first on utilisera plutôt `min-width`

## Méthode 1

```css
h1 {
	font-size: 80px;
}
@media screen and (max-width: 1200px) {
	h1 {
		font-size: calc(25px + 3.3vw) 
	/* calcul en fonction du viewport sur les écrans de moins 1200px */
	}
}
```

## Méthode 2

```css
/* Pas d'utilisation des média queries.
La taille de la police va dépendre de la largeur de l'écran grace à l'utilisation de vmin */

:root {
	--res: calc(O.O1 * 10vmin);
}

/* vmin = viewport min => dimension la plus petite */
h1 {
	font-size: calc(64 * var(--res)); /* 64 = valeur de base */
}
```

## Images
```css
img {
	width: 100%; /* l'image prend 100% de la largeur de son parent */
}
```

Remarque: la propriété `height` de l'image est par défaut sur `auto` ce qui permet de l'adapter en fonction de la largeur fixé pour que l'image garde ses proportions.

Si on indique également une hauteur il faut utiliser en plus les propriétés `object-fit` et `object-position` pour indiquer comme doit s'adapter l'image.

Tout de fois cette méthode reste limitée car elle ne permet pas d'avoir des images qui s'adaptent en fonction du contexte (taille de l'écran, résolution...) et du choix artistique associée (cadrage, orientation...)

Pour rendre les images plus adaptatives il faut utilisé :
-   L'attribut `scrset` ⇒ Le navigateur choisira la meilleure image en fonction de caractéristiques techniques tel que la résolution de l'écran ou le débit de la connexion de l'utilisateur
    
-   La balise `<picture>` ⇒ Idéale pour imposer une image en fonction des choix artistiques. Par exemple, utilisation d'une image qui a été recadrée pour que le sujet soit mieux visible sur les petits écrans
