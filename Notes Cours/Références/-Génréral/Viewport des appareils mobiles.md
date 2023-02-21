# Viewport des appareils mobiles
Sur les mobiles, le viewport est généralement supérieur à la surface physique, afin de pouvoir y caler n’importe quelle page web en lui affectant un niveau de (dé)zoom.

De plus la valeur initiale du viewport ne dépend pas du terminal, mais du navigateur mobile utilisé

## Niveau de zoom initial
Les pages web s’affichent par défaut de manière à ce que toute la surface entre dans celle de l’écran.

Cela correspond au `device-width` (largeur en pixel CSS) de l’appareil divisé par le viewport du navigateur (La surface réelle n’est pas prise en compte dans le calcul)

Exemple avec l' iPhone 5 : Le viewport de Safari est de 980 px. L’appareil considère que sa largeur de 320px alors que celle-ci est physiquement de 640 px. Le niveau de zoom initial sera de 320 / 980, soit environ 0.326x, ce qui peut rendre le contenu illisible.

## La balise meta viewport
Permet d’imposer une largeur pour le viewport. Idéalement on fixe pour valeur la taille de `device-width` (ce qui permet d’avoir un niveau de zoom de 1)

```html
<meta name="viewport" content="width=device-width">
```
  
On peut également fixer le niveau de zoom initial avec la valeur `initial-scale`

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
  
On peut aussi utiliser les valeurs
-   `minimum-scale` : niveau de zoom minimal
-   `maximum-scale` : niveau de zoom maximal (Attention, la valeur “1.0” interdit le zoom = déconseillé)
-   `user-scalable` : autorise l’utilisateur de zoomer
	-   `yes`
	- `no` (déconseillé)