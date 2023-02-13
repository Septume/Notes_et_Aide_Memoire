# Modèle de boite et display

## Composants d’une boite

- `margin` : marge externe
- `border` : bordure
- `padding` : marge interne
- `content` : contenu

![](modele_boite.png)

## Les marges

`margin-top`, `margin-bottom`, `margin-left`, `margin-right`

`padding-top`, `padding-bottom`, `padding-left`, `padding-right`

Les propriétés raccourcies `margin` et `padding` peuvent être utilisés avec une à quatre valeurs

- 1 valeur : s’applique sur les 4 côtés
- 2 valeurs : haut/bas - gauche/droit
- 3 valeurs : haut - gauche/droit - bas
- 4 valeurs : haut - droit - bas - gauche (sens horaire)

Remarque : il est possible d’utiliser des valeurs négatives

```css
/* On applique la même valeur aux quatre côtés */
margin: 1em;
/*  haut et bas | gauche et droit */
margin: 5% 10%;
/* haut | gauche et droit | bas */
padding: 1em 2em 2em; 
/* haut | droit | bas | gauche */
padding: 5px 1em 0 2em;
```

## Display

Type de rendu d’une boite. Chaque éléments HTML ont un display par défaut

- `block` :
	- On peut modifier les dimensions.
	- Si aucune largeur est définie, prend toute la largeur de son élément parent.
	- Si aucune hauteur est définie, prend la hauteur nécessaire pour contenir ses éléments enfants.
	- Ignore la propriété `vertical-align`.
	- Les éléments blocks se positionnent toujours les uns sous les autres, même redimensionnés.
- `inline` :
	- S’inscrit dans le flux du texte et se positionne sur la même ligne que les autres éléments inline.
	- Ne peut pas être redimensionné.
	- Prend la largeur dont il a besoin pour s’afficher.
	- Ignore `margin-top` et `margin-bottom`
	- Accepte la propriété `vertical-align`
- `inline-block`:
	- Les éléments se positionne sur la même ligne mais peuvent être redimensionnés comme des blocs et avoir des valeurs `margin-top` et `margin-bottom`
	- Accepte la propriété `vertical-align`
- `list-item` :
	- Les éléments se comportent comme des éléments `li`
	- Se positionnent les uns en dessous des autres
	- Occupent toute la largeur disponible de leur parent
	- Peuvent être redimensionnés
	- Peuvent bénéficier des propriétés CSS liées aux puces (`list-style`, `list-style-type`,`list-style-image`, `list-style-position`, …)
- `table` :
	- L’élément se comporte comme un élément `table`
	- Prend la largeur de son contenu
	- Accepte la propriété`vertical-align`
- `inline-table` : l’élément se comporte comme un élément `table>` de type en ligne
- `table-row` :
	- L’élément se comporte comme un élément`tr` (rangée de cellules)
	- Accepte la propriété `vertical-align`
- `table-cell`
	- L’élément se comporte comme un élément `td` ou`th` (cellules de tableau)
	- Les éléments s’affichent les uns à côté des autres pour remplir toute la largeur du parent
	- La hauteur s’adapte de manière équilibrée entre les éléments
	- Accepte la propriété `vertical-align`
- `table-row-group` : L’élément se comporte comme un élément `tbody` (groupe de plusieurs rangées)
- `table-header-group` : L’élément se comporte comme un élément `thead` (groupe de rangées toujours affiché avant toutes les autres rangées et groupes)
- `table-footer-group` : L’élément se comporte comme un élément `tfoo>` (groupe de rangées toujours affiché après toutes les autres rangées et groupes)
- `table-column` : L’élément se comporte comme un élément `col` (colonne de cellules)
- `table-column-group` : L’élément se comporte comme un élément `colgroup` (groupe de colonnes)
- `table-caption` : L’élément se comporte comme un élément `caption` (légende de tableau)
- `flex` : active le module Flexbox
- `grid` : active le module Grid Layout
- `none` : L’élément est retiré du flux standard et n’est plus affiché. Les propriétés tel que `margin`, `padding` `width`, `height` sont annulés et les propriétés `position` et `float` sont sans effets. Attention, ne pas confondre `display:none` avec `visibility: hidden` qui se contente juste de masquer l’élément, ce qui peut laisser des espaces vides.

Attention : Lors qu'un élément est en position absolu, fixe ou flottant, sa valeur de `display` est automatiquement calculée à `block` ou `table` (si le display spécifié est `inline-table`). Il est donc impossible de forcer le display d’un élément utilisant ces modes de positionnement,
