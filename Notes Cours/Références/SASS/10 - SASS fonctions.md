# Sass - fonctions

## Fonctions pour les couleurs

`hue($color)` : Retourne la teinte de la couleur (en degré)

`saturation($color)` : Retourne la saturation de la couleur (en %)

`lightness($color)` : Retourne la luminosité de la couleur (en %)

`invert($color)` : Retourne la couleur inverse

`complement($color)` : Retourne la couleur complémentaire

`grayscale($color)` : Retourne la nuance de gris correspond à la couleur (c'est à dire son équivalent totalement désaturé)  
`mix($color1, $color2, %percent)` : Mélange des deux couleurs. Le 3ème argument est facultatif et permet d'indiquer une proportion entre les deux couleurs (Plus le pourcentage est élevé, plus la première couleur sera présente)

`darken($color, $percent)` : Permet d'assombrir une couleur. On utilise un pourcentage d'assombrissement

`lighten($color, $percent)` : Permet éclaircir une couleur

`saturate($color, $percent)` : Pour saturer une couleur

`desaturate($color, $percent)` : Pour désaturer une couleur. (Remarque : un désaturation de 100% correspond à `grayscale()` )

`opacify($color, $percent)` : Pour rendre une couleur plus opaque  
`transparentize($color, $percent)` : Pour rendre une couleur plus transparente

## Fonctions pour les nombres

`percentage($number)` : permet de retourner le % qui correspond à un nombre sans unité (cela correspond à `$number * 100`)

```
percentage(0.2); // 20%
percentage(200px/960px); // 20,8333%
```

`round($number)` : Retourne la valeur arrondie

```
round(15px/2); // 8px
```
