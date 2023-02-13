# Éléments d'interface

`caret-color` : Permet de définir la couleur du curseur pour les champs de saisie. Par défaut la valeur est `auto`

`user-select` : Permettre la sélection ou non du texte par l'utilisateur

- `none` : L'utilisateur ne peut pas sélectionner le texte de l'élément et celui de ses descendants. (Toutefois, l'objet JS `[Selection](<https://developer.mozilla.org/fr/docs/Web/API/Selection)>` pourra contenir ces éléments)

	`text` **:** Le texte peut être sélectionné par l'utilisateur

	`all` Si l'utilisateur fait un double clic ou un clic droit sur l'élément, cela sélectionne l'élément ancêtre le plus haut. Cela permet notamment de sélectionner tout le texte en un clic

- `auto` (A noter que pour les pseudo-éléments `::before` et `::after`, la valeur calculée sera `none`)

Remarque : il est possible de changer le style de la sélection via le pseudo-élément `::selection`

`cursor`: permet de définir la forme du curseur quand le pointeur est au dessus de l'élément

- `auto` : Le navigateur détermine le curseur à afficher en fonction du contexte
- `default` : Le curseur par défaut du système (En général, une flèche)
- `none` : aucun curseur est affiché
- `help` : affichage d'un point d'interrogation
- `pointer` : affichage d'une main
- etc. ([Voir la liste complète sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS/cursor))

Il est possible d'utiliser d'indiquer des images pour créer des curseurs personnalisés. (Voir lien MDN pour en savoir plus)

```css
cursor: url(cursor.png), auto;
```
