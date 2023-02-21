# Animation

`show(duree)` : affiche l'élément

`hide(duree)` : masque l'élément

`toggle(duree)` : affiche ou masque l'élément en fonction de son état actuel.

`fadeIn(duree)` : fait apparaître en fondu l'élément

`fadeOut(duree)` : fait disparaître en fondu l'élément

`fadeTo(duree, opacite)` : amène progressivement l'élément à une opacité donnée. L'opacité doit être un nombre entre 0 et 1

`fadeToggle(duree)`: fait apparaitre/disparaitre en fondu selon l'état actuel de l'élément

`slideUp(duree)` : masque l'élément avec un défilement vers le haut.

`slideDown(duree)` : masque l'élément avec un défilement vers le bas

`slideToggle(duree)` : affiche ou masque l'élément avec un défilement en fonction de son état actuel

Par défaut les animations ont une durée de 400 ms. On peut spécifier une autre durée en indiquant un nombre en argument ou une chaine de caractère indiquant une certaine durée :

- `'slow'` : durée de 600 ms
- `'fast'` : durée de 200 ms

On peut également indiquer en deuxième argument une fonction à appeler une fois l'animation terminée

```jsx
/* fait disparaitre la div quand on clique dessus
avec un fondu de 800 ms */

$('div').on('click', function () {
    $(this).fadeOut(800);
});
```
