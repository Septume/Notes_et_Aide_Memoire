# CSS - Choisir une méthode de positionnement

- `Grid Layout`  : Pour créer le layout de la page.
- `Flexbox`  : Pour la disposition des contenus sur la page
- `position: absolute`  : Pour superposer n'importe où sur la page des éléments dont la taille a été fixée. Exemple : infobulle, titre superposé sur une image, popup.
- `display:inline-block`  A utiliser pour des cas très spécifiques avec un contexte linéaire. Ex : Afficher un bouton "voir plus" à la suite d'un bloc de texte.
- `float`  : A utiliser uniquement pour faire flotter un élément au sein d'un bloc de texte


## Flexbox vs Grid layout

Flexbox : C'est les enfants du containeur qui déterminent comment vont être placés les éléments via les propriétés `flex` et `width`

Grid Layout : c'est le containeur qui détermine comment vont être placés les éléments via la propriété `grid-template-columns`

Dans le cas d'une grille, Grid layout est plus approprié. Si on change le nombre de colonne dans le cas du responsive design, les éléments vont automatiquement s'adapter

[https://www.youtube.com/watch?v=DmFkrYbnFwY](https://www.youtube.com/watch?v=DmFkrYbnFwY)
