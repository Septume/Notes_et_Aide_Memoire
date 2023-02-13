# Texte et éléments en ligne

## Polices

### Spécifier une police

`font-family` : Nom de la police utilisée. (Les noms de police qui contiennent plusieurs mots doivent être entourés de guillemets). On peut indiquer plusieurs noms de police, séparés par une virgule. Le navigateur utilisera la première police de la liste qui est disponible. Il est recommandé d’indiquer en dernier le nom d’une police générique.

- `serif` : police avec empattement
- `sans-serif` : police sans empattement
- `monospace`: police à chasse fixe (tous les caractères ont la même largeur)

Liste des polices courantes :

- **Serif** : Times New Roman, Georgia
- **Sans-serif** : Arial, Arial Black, Verdana, Trebuchet MS, Impact
- **Monospace** : Courier New, Lucida Console

```css
font-familly: "Times New Roman", Georgia, serif;
```

`font-size` : Taille de la police. La valeur peut être une taille exprimée via une unité (pixel, em, rem, pourcentage) ou un mot clé

- `xx-small`, `x-small`, `small`, `medium`, `large`, `x-large`, `xx-large`: Tailles basées sur la taille par défaut utilisée par le navigateur (qui vaut `medium`)
- `larger`,`smaller` : La taille de la fonte est plus grande (`larger`) ou plus petite (`smaller`) que celle de l’élément parent. Par exemple si le parent a une taille `large` , la taille `smaller` correspond à `medium`

Il recommandé d’utiliser de préférence l’unité `rem` (Taille relative à la taille de la police de l'élément racine `html`)

Remarque :

`font-style` : inclinaison des caractères

- `normal`(défaut)
- `italic`
- `oblique`

Pour la valeur `oblique`, il est possible en plus de spécifier l’angle de la pente en indiquant une valeur en degré (ex : `font-style: oblique 10deg;`)

Si les formes italique et oblique sont absentes de la police, le navigateur peut les synthétiser en penchant les glyphes de la forme normale

`font-weight` : graisse des caractères

- `normal` : Défaut. Équivalent à la valeur `400`
- `bold` : Gras. Équivalent à la valeur `700`
- `bolder`: Graisse augmentée d’un niveau par rapport à celle du parent (Thin -> Normal | Normal -> Bold | Bold -> Black)
- `lighter` : Graisse diminuée d’un niveau par rapport à celle du parent (Normal -> Thin | Bold -> Normal | Black -> Bold)
- Valeurs numériques
	- `100` (Thin)
	- `200` (Extra Light/Ultra Light)
	- `300`(Light)
	- `400` (Normal)
	- `500` (Medium)
	- `600` (Semi Bold)
	- `700` (Bold)
	- `800` (Extra Bold/Ultra Bold)
	- `900` (Black/Heavy)

Si la graisse indiquée n’est pas disponible pour la police, le navigateur choisira la graisse disponible la plus proche.

`font-variant` : Variante de la police

- `normal` (défaut)
- `small-caps` : petites capitales

`font-stretch` : Permet de choisir entre la forme normale, condensée ou étendue d’une police (Si disponible)

- `normal`
- `semi-condensed`, `condensed`, `extra-condensed`, `ultra-condensed`
- `semi-expanded`, `expanded`, `extra-expanded`, `ultra-expanded`

Il est possible d’utiliser la propriété raccourcie `font` en respectant les règles suivantes :

- Doit inclure les valeurs pour `font-size` et `font-family`
- Peut inclure les valeurs pour `font-style`, `font-variant`, `font-weight`, `font-stretch` et `line-height`
- Les valeurs pour `font-style`, `font-variant` et `font-weight` doivent précéder la valeur pour `font-size`
- La valeur pour `line-height` doit immédiatement suivre la valeur pour `font-size`, séparée par une barre oblique (par exemple `16px/3`)
- La valeur pour `font-family` doit être la dernière.

```css
body {
	font: 2em "Open Sans", sans-serif;
	font: italic 2em "Open Sans", sans-serif;
	font: italic small-caps bolder 16px/3 cursive;
	font: italic small-caps bolder condensed 16px/3 cursive;
}
```

### Utiliser des polices personnalisés

La déclaration `@font-face` permet d’intégrer des polices personnalisées. On peut l’utiliser au sein du fichier global ou dans une règle conditionnelle. Les propriétés sont :

- `font-family` : le nom de la police importée
- `src` : URL de de la police importée. On peut indiquer plusieurs URL séparées par des virgules et préciser le format de la police avec la fonction `format()`.

```css
@font-face {
	font-family: 'Police';
	src: url('police.eot') format('eot'),
			 url('police.woff') format('woff'),
			 url('̂police.ttf') format('truetype'),
			 url('police.svg') format('svg');
}

body {
	font-family: Police, sans-serif;
}
```

Formats de police acceptés : `"woff"`, `"woff2"`, `"truetype"`, `"opentype"`, `"embedded-opentype"` et `"svg"`.

Remarque : le `woff2` est le format le plus recommandé car son poids est plus léger

On peut également indiquer des polices spécifiques en précisant les valeurs de `font-style`, `font-stretch`, `font-variant` et `font-weight`

```css
@font-face {
	font-family: garamond;
	src: url('garamond-italic.ttf');
	font-style: italic;
}
```

### Chargement des polices personnalisées

Lorsque la police est téléchargée par le navigateur, son rendu passe par 3 étapes :

1. **Blocage des fontes** : Si le fichier de fontes n'est pas encore chargé, le texte est rendu de manière invisible (tout en occupant l'espace). Seuls les soulignements des liens sont affichés. Dès que le fichier est chargé, la texte apparait normalement dans la police attendue. Cette étape est également appelée **FOIT (Flash Of Invisible Text)**
2. **Échange des fontes** : Au bout d'une certaine période si le fichier n'est pas toujours pas chargé, une police alternative est utilisée le temps que le chargement se termine. Cette étape est également appelée **FOUT (Flash Of Unstyled Text)**
3. **Échec du chargement des fontes** : Si finalement il y a échec du chargement du fichier, c'est la police alternative qui sera utilisée.

Les délais entre les étapes peuvent variés selon le navigateur.

 `font-display` : Permet de gérer les étapes du rendu pendant le chargement de la police.

- `auto` : Stratégie définie par le navigateur
- `block` : Période de blocage courte (environ 3s), suivi d'une période d'échange infinie. (Correspond au FOIT). Utile pour les polices d'icônes car cela évite d'afficher des caractères incongrus.
- `swap` : Période de blocage très courte (environ 100ms), suivi d'une période d'échange infinie ( (Correspond au FOUT). Utile pour le texte qui doit s'afficher le plus rapidement possible, quitte à utiliser une police alternative.
- `fallback` : Période de blocage très courte (environ 100ms), suivi par une courte période d'échange (environ 3s)
- `optional` : Période de blocage très courte (environ 100ms) et pas de période d'échange. Cela permet d'afficher la police que si elle est immédiatement disponible (par exemple dans le cache) ou dans le cas contraire afficher une police alternative. Utile pour les polices personnalisées non essentielles, comme par exemple les polices exotiques à usage purement esthétique.

Remarque : Dans le code HTML, on peut aussi utiliser la relation `preload` qui permet de pré-charger des ressources comme les fontes.

### Adaptation des polices

`font-size-adjust` : Permet de spécifiée la hauteur x de la police. Cela est utile pour faire en sorte qu'une police de substitution ai la même hauteur x que la police de premier choix, afin de garantir la lisibilité.

```jsx
font-size: 20px;
font-size-adjust: 0.6; 
/* la hauteur d'x sera de 12 px (0.6 * 20px)
O.6 correspond au ratio de la police de premier choix */
```

## Hauteur de ligne

`ligne-height` : Permet de fixer une hauteur de la boite d'une ligne. Si utiliser sur un élément de type bloc, indique la hauteur minimale des lignes au sein de l'élément. On peut indiquer comme valeurs :

- Un nombre indiquant un facteur multiplicateur par rapport à la taille de la police
- Une taille spécifiée en px (non recommandé)
- Une taille spécifiée en em ou % (relatif à la taille de la police)
- `normal` : C'est le navigateur qui décide de la hauteur (En général il utilise le facteur multiplicateur `1.2` )

**Attention** : `line-height` est une valeur héritée. Par conséquent un élément enfant aura la même valeur calculée de `line-height` que son parent ( et donc relative à la taille de police du parent). Il est donc recommandé d'utiliser une valeur sans unité (facteur multiplicateur) , cette dernière sera utilisée par les éléments enfants pour calculer la valeur de `line-height` à partir de leur propre taille.

Remarque : Il est possible d'utiliser une taille plus petite que celle de la police. Dans ce cas la boite de ligne sera plus petite que la zone de contenu.

## Alignement vertical

`vertical-align` : Permet de définir l’alignement vertical du texte ou d’un élément inline par rapport à la ligne à laquelle il appartient ou le contenu d’une cellule de tableau

- `baseline` : (Défaut) aligne la ligne de base de l’élément, ou le bord inférieur pour un élément remplacé, avec la ligne de base de l'élément parent
- `super` : aligne la ligne de base de l’élément ou le bord inférieur sur la ligne des exposants du parent
- `sub` : aligne la ligne de base de l’élément ou le bord inférieur sur la ligne des indices du parent
- `text-top` : aligne le haut de l'élément avec le haut du texte du parent
- `text-bottom` : aligne le bas de l'élément avec le bas du texte du parent
- `middle` : aligne le milieu de l'élément à une hauteur par rapport à la ligne de base du parent qui correspond à la moitié d'hauteur x de la police du parent
- une taille en px : même chose mais avec une hauteur indiquée. On peut indiquer une valeur négative
- un pourcentage : même chose. Le pourcentage se fait par rapport à la valeur `line-height`
- `top` : le bord supérieur de la boite de l'élément est aligné avec le bord supérieur de la boite de ligne
- `bottom` : le bord inférieur de la boite de l'élément est aligné avec le bord inferieur de la boite de ligne

![](vertical-align-1.png)

**Pour les cellules de tableau**

- `baseline` : aligne la ligne de base de la cellule avec celle de toutes les autres cellules de la rangée. (l'alignement se fait par rapport à la première ligne de texte. La ligne de base de la rangée est définie par la ligne de base de cellule initiale la plus base)
- `bottom` : aligne le bord inferieur du contenu de la cellule avec le bord inférieur de la rangée
- `top` : aligne le bord supérieur du contenu de la cellule avec le bord supérieur de la rangée
- `middle` : aligne le milieu du contenu de la cellule avec le milieu de la rangée

Remarque : Les autres valeurs de la propriété (`text-top`, …) seront ignorées et c'est la valeur `baseline` qui sera appliquée.

## Styles de texte

### Décorations de texte

`text-decoration-line`: ajoute une ligne de décoration

- `none` : Aucune décoration
- `underline`: ligne en dessous
- `overligne` : ligne au dessus
- `line-through`: barré

On peut indiquer plusieurs valeurs

```css
.text {
	text-decoration: underline overline;
}
```

`text-decoration-color` : Couleur de la ligne de décoration

`text-decoration-style` : Style de la ligne de décoration

- `solid`
- `double`
- `dotted` (Points)
- `dashed`(tirets)
- `wavy` (ondulations)

On peut également utiliser la propriété raccourcie `text-decoration`

```css
.text {
		text-decoration: underline red wavy;
}
```

**Attention** : Ces propriétés se propagent sur les éléments enfants sans qu’il soit possible de les désactiver avec la valeur `none`. Il n’est pas possible non plus de changer pour un enfant la couleur (`text-decoration-color`) ou le style (`text-decoration-style`) d’une ligne de décoration définie sur le parent. Si on définie une nouvelle ligne de décoration sur l’enfant (avec `text-decoration-line`), cette dernière sera cumulée avec la ligne de décoration du parent (Cette nouvelle ligne de décoration peut avoir son propre style ou/et couleur)

```html
<p class="parent">Lorem ipsum dolor sit amet, <span class="enfant">consectetur adipisicing elit</span></p>
```

```css
.parent {
	text-decoration: underline red;
}

.enfant {
	text-decoration: overline blue double;
}
```

`text-underline-position` : Position du soulignement lorsque `text-decoration` vaut `underline`

- `auto`
- `under` : le soulignent se situe sous la ligne de base, à une position où il ne traversera pas de jambage.

### Ombrage

`text-shadow` : Ombre sur le texte. Les valeurs sont :

- Le décalage horizontal de l’ombre (Une valeur négative permet de placer l’ombre à gauche de l’élément)
- Le décalage vertical de l’ombre (Une valeur négative permet de placer l’ombre en haut de l’élément
- (Facultatif) Rayon du flou (blur) Plus la valeur est haute, plus le flou de l’ombre sera diffus. Valeur positive seulement. Si non indiqué, sa valeur est 0.
- (Facultatif) La couleur de l’ombre. (la valeur peut être indiquée avant ou après les valeurs de décalage). Si non indiqué c’est le navigateur qui décide de la couleur à appliquer (cela peut-être la couleur du texte)

Remarque :

- Une valeur de 0 pour un des décalages place l'ombre au dessus du texte.
- Une valeur de 0 pour les deux décalages place l'ombre en dessous du texte. Cette dernière peut être visible en fonction de la valeur du rayon du flou.

Il est possibles de spécifier plusieurs ombres, en séparant les valeurs par une virgule

```css
/* créé une ombre portée simple */

.text1 {
  font-size : 50px;
  color: green;
  text-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);

}

/*créé un effet de bordure de texte */

.text2 {
  font-size: 50px;
  color: white;
  text-shadow: -1px 0 0 rgba(0, 0, 0, 0.8),
    1px 0 0 rgba(0, 0, 0, 0.8),
    0 -1px 0 rgba(0, 0, 0, 0.8),
    0 1px 0 rgba(0, 0, 0, 0.8);
}
```

### Autres styles de texte

`text-transform` : permet de changer la case

- `none (défaut)`
- `uppercase`
- `lowercase`
- `capitalize` (première lettre de chaque mot en majuscule)

`text-align` : alignement du texte

- `left` ( défaut)
- `center`
- `right`
- `justify` : texte justifié (prend toute la largeur possible sans laisser d’espace blanc à la fin des lignes)

`text-justify` : Précise le type de justification à appliquer quand `text-align` vaut `justify`

- `none` : Pas de justification.
- `auto` (défaut)
- `inter-word` : Le texte est justifié en en ajustant les espaces entre les mots
- `inter-character` : Le texte est justifié en ajustant les espaces entre les caractères

`text-align-last` : alignement de la dernière ligne d’un bloc de texte.

- `left`
- `right`
- `center`

`text-indent` : taille de l’ indentation de la première ligne d’un bloc de texte. Il est possible d’indiquer une valeur négative.

`word-spacing` : taille de l’espacement entre les mots. La valeur par défaut est `normal`, ce qui permet au navigateur de gérer l’espacement en fonction de la police utilisée. Si on précise une taille, celle ci s’ajoute à l’espacement par défaut. Une valeur négative, diminue l’espacement normal.

`letter-spacing` : taille de l’ espacement entre les caractères. La valeur par défaut est `normal`. Même fonctionnement que `word-spacing`

`quotes` : Style des marques de citation

- `none` : pas de marque
- `initial` : par défaut
- Utilisation de paires de chaines de caractères permettant de spécifier la marque ouvrante et fermante. Si on indique plusieurs paires, la première correspond aux citations de plus haut niveau, la deuxième aux citations imbriquées dans une autre citation, et ainsi de suite.

Exemple

```css
/* utilisation des guillemets français */
quotes: "«" "»";

/* Marques pour deux niveaux de citation */
quotes: "«" "»" "‹" "›";
```
