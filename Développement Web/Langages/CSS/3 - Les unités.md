# Les unités

## Unités absolues

Pour une sortie écran : px (pixel)

Pour une sortie impression :

- cm
- mm
- in (inch = pouce = 25.4 mm)
- pt (point = 1/72 de inch)
- pc (pica = 12 points)

## Unités relatives

- % (pourcentage) : relatif aux dimensions de l’élément parent. Exemple : si le parent a une largeur de 200px, un élément enfant avec un `width:50%` aura une largeur de 100px
- `vw` (viewport width) : % de la largeur du viewport (1vw = 1% de la largeur)
- `vh` (viewport height) : % de la hauteur du viewport.
- `vmin` (viewport minimum) : relatif à la dimension la plus petite du viewport.
	- si la largeur du viewport est plus petite que la hauteur : 1 vmin = 1vw.
	- Si c’est la hauteur qui est plus petite : 1vmin = 1vh
- `vmax` ( viewport maximum) : relatif à la dimension la plus grande du viewport
- `em` : relatif à la taille de police de l’élément parent. En plus de `font-size`, on peut l’utiliser avec les propriétés comme `line-height`, `margin-top`, `margin-bottom` etc…pour avoir des dimensions qui s’adaptent automatiquement à la taille du texte.
- `rem` : relatif à la taille de la police de l’élément racine `html`

## Différence pratique entre le em et le rem

Une taille exprimée en `em` se calcule par rapport à la taille de son parent, ce qui entraine des calculs en cascade

Exemple : `body > div > span`

- `body` : 1 em => 16px
- `div` : 0.8 em => 12,8px [0,8 * 16]
- `span` : 0.7 em => 8,96 px [0,7 * 12,8]

Pour éviter cela on peut utiliser à la place le `rem` (root em) qui se calcule par rapport à l’élément `html`

- `body`: 1em => 16px (hérité de l’élément `html`)
- `div`: 0.8 rem => 12,8px [0,8 * 16]
- `span`: 0.7 rem => 11,2px [0,7 * 16]

## Fonction calc()

Permet de faire des calcul

Exemple

```css
width: calc(100% - 20px);
```

**Attention : l ’espace est nécessaire autour du signe d’opération pour que `calc()` fonctionne**

Remarque : On peut utiliser comme valeur des variables CSS ou affecter le résultat d'une fontion `calc()` dans une variable. On peut également imbriquer une fonction `calc()` dans une autre
