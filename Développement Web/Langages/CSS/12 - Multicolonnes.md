# Multicolonnes

S’utilise sur des éléments de type `block`, `table-cell` et `inline-block` pour répartir équitablement le contenu en plusieurs colonnes

Un conteneur de colonnes ne peut pas servir de référent à des descendants positionnés en `absolute` ou `fixed`

## Création du multicolonnes

`column-width` : largeur optimale des colonnes (px ou em). La largeur réelle peut être plus grande ou plus petite en fonction de l’espace disponible. Valeur par défaut : `auto`

`column-count` : nombre optimal de colonnes. Si `column-width` est fixé, représente le nombre maximal de colonnes. Valeur par défaut : `auto`

`columns` : méga-propriété combinant les deux précédentes

## Gouttières

`column-gap` : espace de séparation entre les colonnes (en px ou en em). Valeur par défaut : `normal`

`column-rule` : liseré de séparation. Propriété raccourcie qui rassemble `column-rule-color`, `column-rule-width`, `column-rule-style` (valeurs : solid, dotted, etc.)

```css
section {
	columns: 4;
	column-gap: 50px;
	column-rule: 1px solid black;
}
```

### Sauts de colonnes

`break-before` : saut de colonne avant le texte

`break-inside` : saut de colonne à l’intérieur du texte

`break-after` : saut de colonne après le texte

Les valeurs sont :

- `auto` : le saut de colonne est autorisé mais n’est pas obligatoire (valeur par défaut)
- `column` : force un saut de colonne
- `avoid-column` : interdit un saut de colonne

### Étendre un élément sur toutes les colonnes

column-span :

- all : l’élément s’étend sur toutes les colonnes
- none : l’élément ne s’étend pas sur toutes les colonnes

**Attention : Ne fonctionne pas sous Firefox**

```css
section {
	columns: 4;
	column-gap: 50px;
	column-rule: 1px solid black;
}

section h1 {
	/* Le titre s'étend sur toutes les colonnes */
	column-span: all;
}
```
