# iPhone X et le "notch"

Il s'agit de l'encoche sur l'écran de l'appareil (permet d'avoir un espace pour la caméra frontale)

Pour éviter que le contenu soit caché par l'encoche, Safari rajoute des marges. Il est possible de les supprimer en ajoutant `viewport-fit=cover` à la balise `meta viewport`

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
```

  
Cela permet de faire en sorte que la page couvre l'ensemble de l'écran. Il faut toutefois prendre en compte l'encoche qui pourrait cacher le contenu en définissant dans le code CSS une zone de sécurité (_safe area)_

```
body {
	padding-left: env(safe-area-inset-left);
	padding-right: env(safe-area-inset-right);
	padding-top: env(safe-area-inset-top);
	padding-bottom: env(safe-area-inset-bottom);
}