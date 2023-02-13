# Éléments block

## Dimensions

- `width` , `min-width`, `max-width` (Largeur)
- `height` , `min-height`, `max-height` (Hauteur)

Par défaut `width` et `height` concerne le taille de la boite `content`. La taille de la marge intérieure (padding) et celle de la bordure s’ajoute à cette taille initiale.

Il est possible de changer ce comportement avec la propriété `box-sizing`

- `content-box` : (défaut) les dimensions sont par rapport à la boite content
- `border-box` : les dimensions prennent en compte la marge intérieure et la bordure

Remarque : il est recommandé d’utiliser `border-box` pour l’ensemble des éléments

```css
/* A indiquer au début du fichier */
*, *:before, *:after {
	box-sizing: border-box;
}
```

`resize`: permet de rendre l’élément redimensionnable par l’utilisateur

- `none`: Pas de redimensionnement possible. Celle valeur est utile pour enlever le redimensionnement d’un élément `<textarea>`
- `both`L’élément peut être redimensionné horizontalement et verticalement. Pour que le mécanisme de redimensionnement s’affiche il faut mettre la propriété `overflow` à la valeur `scroll`
- `horizontal` : L’élément peut être redimensionné seulement à l’horizontal
- `vertical` : L’élément peut être redimensionné seulement à la vertical

## Fusion des marges

Concerne les marges verticales (haut et bas) des éléments de rendu block :

- Deux éléments block qui se suivent : la marge inférieure du premier fusionne avec la marge supérieure du deuxième. C’est la marge la plus grande qui est conservée.
- blocks enfants : une fusion avec les marges verticales du parent se produit pour la marge supérieure du premier enfant et la marge inférieure du dernier enfant . **Attention, si le parent contient du texte au début ou à la fin, la fusion des marges ne se produit pas**

La fusion peut se faire à plusieurs niveaux .

pour empêcher la fusion des marges entre parents et enfants :

- mettre du padding sur le parent (`padding: 1px 0`)
- utiliser des bordures sur le parent
- utiliser un contexte de formatage block (`overflow` en `auto` ou `hidden`)

Remarque : Les marges des éléments flottants, ou positionnés en absolu ou en fixe, ne fusionnement pas

## Largeur et hauteur de 100 %

### Largeur de 100 %

Par défaut la largeur d’un bloc est définie à `auto` , ce qui correspond à la largeur du viewport. Une largeur exprimée en `%` fait référence à la largeur de l’élément parent. Si la largeur du parent n’est pas définie, elle est considéré comme `auto`. Dans ce cas la largeur exprimé en pourcentage fera référence au viewport. Par ex : un élément avec une largeur définie à 50% qui est enfant d’un élément dont la largeur n’est pas définie aura une largeur correspondant à 50% du viewport.

### Hauteur de 100 %

Pour la propriété `height` la valeur `auto` correspond à la hauteur nécessaire pour que le contenu ne dépasse pas de la boite. Cette valeur est donc indéfnie car dépendante de plusieurs facteurs comme la longueur du contenu ou la largeur de la boite.

Une hauteur exprimée en `%` fait également référence à l’élément parent. Or si ce dernier n’a pas de largeur défini, il possède une valeur `auto` qui est indéfinie et donc à laquelle il est impossible de faire référence. La propriété height exprimée en % ne peut donc pas fonctionner.

La solution est de fixé la largeur du parent en fonction de la largeur du viewport.

```css
.container { height: 100vh;}
```

## Centrer horizontalement un block

Il faut préciser une largeur et indiquer une valeur auto aux marges externes gauche et droite

Exemple :

- ``margin: 5px auto;`
- `margin: auto;` (Équivalant à `margin: 0 auto` car la valeur `auto` pour les marges haut et bas correspond à la valeur zéro)

## Gestion du dépassement de contenu

`overflow-x` : Gestion du dépassement du contenu sur l’axe horizontal (bords gauche et droit)

`overflow-y` : Gestion du dépassement du contenu sur l’axe vertical (bords haut et bas)

`overflow`: Propriété raccourcie

- `visible` : Le contenu reste visible et peut dépasser du conteneur (Défaut)
- `hidden` : Le contenu est coupé pour ne pas dépasser du conteneur et n’est plus visible dans ce cas.
- `scroll` : Le contenu est coupé pour ne pas dépasser du conteneur. Le navigateur ajoute des barres de défilement pour permettre d’afficher le reste du contenu.
- `auto` : c’est le navigateur qui décide du comportement à adopter

Remarque : Si on définit un premier axe avec `visible` et le deuxième axe avec une valeur différente (`hidden`, `scroll`, `auto`), alors le premier axe sera considéré implicitement comme `auto`

`text-overflow`: Permet de laisser un indice visuel concernant le contenu coupé avec la propriété `overflow`et les valeurs `hidden` ou `scroll` sur l’axe horizontal.

- `clip` : Le contenu est rogné à la bordure de la boite (Défaut)
- `ellipsis` : affiche des points de suspension à l’endroit ou le contenu est rogné. Cela peut-être utile en combinaison de `white-space: nowrap` pour des éléments d'interface qui doivent rester sur une ligne (Texte de bouton, navigation, fil d'Ariane, etc.),

`overflow-wrap`: Permet de définir une césure dans le cas d’une longue chaine dépassant de son conteneur. (Remarque : Cette propriété remplace l’ancienne propriété `word-wrap`)

- `normal` : Pas de césure. Une longue chaine peut dépasser de son conteneur
- `break-word` : Une césure peut être effectuée après n’importe quel caractère pour empêcher le dépassement.

Remarque : il existe également la propriété `word-break` qui est quasi identique, mais qui sera plus utile dans le cadre de l’utilisation d’une langue asiatique comme le chinois

`white-space` : Permet de gérer les espaces blancs et le retour à la ligne automatique (Effectué pour empêcher le dépassement de conteneur sur la largeur)

En CSS les espaces blancs correspond aux caractères suivants :

- espace (U+0020)
- tabulation (U+0009)
- saut de ligne (U+000A)
- retour à la ligne (U+000D)
- saut de page (U+000C)

Les valeurs sont :

- `normal` : Défaut. Les espaces blancs successifs sont fusionnés en un espace unique. Les retours à la ligne dans le texte d’origine (caractères de saut de ligne / retour à la ligne) ne sont pas préservés. (Seule la balise `<br>` permet de créer un retour à la ligne). Un retour à la ligne automatique est effectuée pour ne pas que le contenu dépasse de son conteneur.
- `pre-line` : similaire à `normal` sauf que les retours à la ligne dans le texte d’origine (caractères de saut de ligne / retour à la ligne) sont préservés.
- `nowrap` : similaire à `normal` mais sans retour à a ligne automatique (Le contenu peut dépasser de son conteneur)
- `pre`: Pas de fusion des espaces blancs successifs. Les retours à la ligne dans le texte d’origine (caractères de saut de ligne / retour à la ligne) sont préservés. Pas de retour à la ligne automatique. Il s’agit du style par défaut pour l’élément HTML `<pre>`
- `pre-wrap`: similaire à `pre` mais avec retour à la ligne automatique
- `break-spaces` : Très similaire à `pre-wrap` . La différence est que quand il y a un retour à la ligne automatique pour empêcher le dépassement du conteneur, avec `pre-wrap` les éventuels blancs restant sont supprimés au début de la nouvelle ligne, tandis qu'avec `break-spaces` ils sont conservés.

![](white-space.png)

`hyphens` : Permet de créer une césure "intelligente" qui affiche des traits d'union tout en s'adaptant aux règles typographiques de la langue utilisée.

- `auto` : Les césures sont gérés automatiquement par le navigateur en fonction de la langue de la page ou de l'élément spécifiée via l'attribut HTML `lang`
- `manual` : Les mots peuvent être coupés là où est présent un caractère de césure
	- U+2010 (hyphen) : Affiche un trait d'union même quand le mot n'est pas coupé
	- U+00AD (soft hyphen) : Trait d'union invisible. On peut utiliser l'entité HTML `&shy;` pour insérer ce caractère
- `none` : Pas de césure, y compris là on se trouve des caractères de césure.
