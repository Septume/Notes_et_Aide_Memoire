# Effets visuels avancés

[Compléter]

## Dégradés

Fonctions :

- `linear-gradient()` : dégradé linéaire (dégradé qui suit une direction sur une ligne)
- `radial-gradient()` : dégradé radial (dégradé qui part d’un point central)
- `conic-gradient()` : dégradé conique (dégradé qui fait le tour d'un cercle)

![](Screenshot_2018-11-29_21.09.19.png)

Ces fonctions retournent un objet CSS `Image` et peuvent être appliquées à n'importe quelle propriété qui accepte comme valeur une image ( `background-image` , `border-image`,…)

On indique les couleurs à utiliser (deux ou plus) en paramètre. On peut utiliser la notation RGBa pour définir une transparence

### Dégradé linéaire

```css
background: linear-gradient(yellow,red);
```

Par défaut la direction du dégradé va du haut vers le bas. Pour changer la direction on indique en premier paramètre une de ces valeurs :

- `to bottom` :180 degré (défaut - haut vers le bas)
- `to top` : 0 degré (bas vers le haut)
- `to right` : 90 degré (gauche vers droite)
- `to left` : 270 degré (droite vers gauche)
- `to top right`: 45 degré
- `to bottom left`
- etc.

```css
background: linear-gradient(to top left, yellow, red);
```

Il est également possible d’indiquer une direction en degré (`deg`). Par défaut l’orientation est de `180deg`

```css
 background: linear-gradient(250deg,yellow, green);
```

### Dégradé radial

```css
background: radial-gradient(yellow,red);
```

On peut rajouter en paramètre la forme que doit prendre le dégradé

- `ellipse` (défaut)
- `circle`

Par défaut le dégradé commence au centre (`center`) . On peut changer le point de départ avec les mots clés `at top`, `at bottom`, ou une valeur en px ou % (même syntaxe que pour `background-position`)

```css
background: radial-gradient(circle at top left, white, green);
```

```css
background: radial-gradient(circle,yellow, red
```

Par défaut, le dégradé s'entend jusqu'au côté de l'élément e plus éloigné, mais on peut le changer avec ces mots clés

- `closest-corner` : jusqu'au coin le plus proche
- `farthest-corner` : jusqu'au coin le plus éloigné
- `closest-side` : jusqu'au côté le plus proche
- `farthest-side` : jusqu'au côté le plus éloigné (défaut)

```css
background: radial-gradient(circle closest-side,yellow, red);
```

### Dégradé conique

```css
background: conic-gradient(red, orange, yellow, green, blue);
```

Par défaut le dégradé commence à 0 degré mais on peut changer l'angle avec le mot clé `from` suivi d'une valeur en `deg`

```css
background: conic-gradient(from 45deg, red, orange, yellow, green, blue);
```

On peut également changer la position de l'ange (par défaut `center`) avec les mots clés `at top`, `at bottom`, ou une valeur en px ou % (même syntaxe que pour `background-position`)

```css
background: conic-gradient(from 45deg at 50px 50px, red, orange, yellow, green, blue);
```

### Définir des "color-stops"

Les *color-stops* sont des points de distance de la ligne de dégradé sur lesquels on arrive à une couleur précise. Par défaut la première couleur est à 0% et la dernière à 100% et les éventuelles couleurs intermédiaires sont reparties uniformément.

Par exemple : Pour un dégradé linéaire de 4 couleurs et d'une distance de 300px

- La 2ème couleur est complètement atteinte à 100px
- La 3ème couleur est complètement atteinte à 200px
- La 4ème couleur est complètement atteinte à 300px

Il est possible de définir des *color-stops* personnalisés, en précisant pour les couleurs concernées une distance en px ou en %. Il est possible d'utiliser une valeur en dehors de l'intervalle du dégradé pour créer certains effets (On peut utiliser une valeur négative).

```css
/* le jaune est complètement atteint à 100px du point d'origine (en partant de la gauche) */
background: linear-gradient(to right, red, yellow 100px);        

/* le jaune est complètement atteint à 25% de la ligne de degradé (en partant de la droite) */
background: linear-gradient(to left, red, yellow 25%);
```

On peut également utiliser les *color-stops* pour faire un effet qui supprime la graduation entre les couleurs

```css
background: linear-gradient(to right,blue 100px, purple 200px, red 200px, red 300px, yellow 300px);
```

Résultat

![](degrade.png)

Pour les dégradés coniques ont utilise une valeur en `deg`

### Répéter un dégradé

Fonctions :

- `repeating-linear-gradient()`
- `repeating-radial-gradient()`
- `repeating-conic-gradient()`

```css
/*dégradé répété tout les 100px*/
background: repeating-linear-gradient(to right, red, yellow 100px);
```

On peut aussi créer certains effets

```css
.box {
  height: 200px;
  width: 200px;
  border: 1px solid black;
  background: repeating-linear-gradient( to bottom right, red, red 25px, yellow 25px,yellow 50px);
}
```

Résultat

![](degrade%201.png)

## Shapes

le module CSS *Shapes* permet de donner une forme géométrique à un élément flottant tout en permettant au contenu intérieur ou extérieur de s'adapter à cette forme.

On peut créer la forme à l'aide d'une fonction

- `circle()` :
- `ellipse()`
- `inset()`
- `polygon()`

## Masques

## Filtres

`filter` : Permet d'appliquer des filtres à un élément afin d'obtenir un effet graphique. Généralement utilisés pour ajuster le rendu d'une image, d'un arrière-plan ou des bordures. Pour cela on utilise une fonction

- `grayscale()` : Effet de noir et blanc. Prend en paramètre un % qui correspond à la force de l'effet. Si la valeur est 100%, l'élément sera complètement en noir et blanc
- `sepia()` : Effet sépia. Même fonctionnement que `grayscale()`
- `invert()` : Inversion des couleurs. Même fonctionnement que `grayscale()` (Une valeur de 100% créé un négatif)
- `blur()` : Applique un fou gaussien. Prend comme paramètre une valeur en px qui correspond au rayon de flou. Plus la valeur est importante, plus le flou sera prononcé.
- `saturate()` : Règle la saturation. Prend comme paramètre une valeur en %. Plus la valeur est basse, plus l'image sera désaturée. A 100% l'image reste inchangée. On peut utiliser une valeur supérieure à 100% pour créer un effet de sursaturation.
- `contrast()` : Règle le contraste . Même fonctionnement que `saturate()`
- `brightness()` : Règle la luminosité. . Même fonctionnement que `saturate()`
- `hue-rotate()` : Modifier les couleurs en se basant sur la roue des couleurs. On indique en paramètre une valeur en `deg` pour appliquer une rotation
- `opacity()` : Règle l'opacité. A 0% l'élément sera complètement transparent. Cette fonction est proche de la propriété opacity, toutefois, avec les filtres, certains navigateurs utilisent l'accélération matérielle.

Il est possible d'appliquer plusieurs filtres

```css
img {
  filter: grayscale(0.5) blur(10px);
}
```

## Blend modes

Permet de créer des mode de fusion entre plusieurs éléments.
