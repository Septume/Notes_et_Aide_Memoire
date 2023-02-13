# Tableaux

## Disposition du tableau

`table-layout`: Permet de définir le modèle d’affichage du tableau

- `auto` : Le contenu des cellules détermine la largeur des colonnes et du tableau.
- `fixed` : Le contenu n’est plus pris en compte pour déterminer la largeur des colonnes et du tableau, ce qui permet de préciser une largeur fixe pour ces éléments. Il faudra traiter éventuellement les problèmes de dépassement de contenu avec les propriétés `overflow` ou/et `overflow-wrap`

## Bordures

`border-collapse` : appliquer à l’élément `table`, permet de fixer le comportement des bordures appliquée aux cellules du tableau.

- `collapse` : les bordures sont fusionnées entre elles
- `separate` : les bordures sont dissociées (défaut)

```css
table {
	border-collapse: collapse;
}

td, th {
	border: 1px solid black;
}
```

Pour des bordures non fusionnées, on peut indiquer la taille de l’espacement entre elles avec la propriété `border-spacing`

```css
table {
	border-spacing: 5px;
}

td, th {
	border: 1px solid black;
}
```

On peut également indiqué si les bordures et l’arrière plan doivent être affichés pour les cellules vides avec la propriété `empty-cells`

- `show` : montrer la bordure et l’arrière plan (par défaut)
- `hide` : cacher la bordure et l’arrière plan

**Attention** : Ne fonctionne pas avec `border-collapse: collapse`

```css
table {
	empty-cells: hide;
}

td, th {
	border: 1px solid black;
}
```

## Taille des cellules

On utilise la propriété `height`

```css
td, th {
	height: 80px;
}
```

## Position de la légende du tableau

`caption-side`:

- `top` (défaut)
- `bottom`
