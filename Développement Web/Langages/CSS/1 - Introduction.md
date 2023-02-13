# Introduction

CSS = Cascading Style Sheets

## Syntaxe

![](css_syntaxe.png)

On peut indiquer plusieurs sélecteurs pour une règle en les séparant par des virgules

Pour indiquer des commentaires :`/* commentaire */`

Remarque : Le point virgule n'est pas obligatoire à la fin de la dernière déclaration du bloc de règle, **mais fortement recommandé**

## Lié le css au code html

Lier un fichier CSS

```html
<link rel="stylesheet" href="style.css">
```

Indiquer du code CSS directement dans le `<head>`

```html
<style>/* code CSS */</style>
```

Appliquer directement un style à un élément HTML : Attribut `style` avec pour valeur les déclarations CSS séparées par un point-virgule

```html
<p style="color:red; background-color:yellow">ce texte est en rouge avec un fond jaune </p>
```

## Importer des règles à partir d’une autre fichier css

`@import url liste-requetes-media`

- *url* : absolue ou relative.
- *liste-requetes-media* : Facultatif. Liste de requêtes média séparées par des virgules

Doit être utilisé avant toutes autres règles (à l’exception de`@charset`)

Pour des meilleurs performances il faut privilégier`<link>` à `@import`

```css
@import 'custom.css';
@import url("fineprint.css") print;
@import url('landscape.css') screen and (orientation:landscape);
```

## Encodage

`@charset`

Doit être indiqué quand on utilise des caractères non-ASCII pour certaines propriétés CSS telles que `content`. Doit être le premier élément de la feuille de style

```css
@charset "utf-8";
```

## Héritage

### Arbre dom

Par rapport à un autre élément

- **ancêtres** : éléments situés dans la même branche à un niveau supérieur de la hiérarchie
- **descendants** : éléments situés dans la même branche à un niveau inférieur de la hiérarchie
- **parent** : élément unique situé juste au-dessus dans la hiérarchie
- **enfants** : éléments situés juste en dessous dans la hiérarchie
- **frères** : éléments placés au même niveau dans la même branche.

### Principe de l’héritage

Les éléments descendants héritent des propriétés de leur ancêtres (sauf en cas d’annulation par une nouvelle propriété)

Certaines propriétés ne s’héritent pas (Ex : `margin`,`padding` et autres propriétés de bloc)

L’héritage s’applique aussi à la balise`<a>`. Ses enfants sont les pseudo-classes suivantes :

- `:link`(lien par défaut)
- `:visited` (lien déjà visité)
- `:hover` (lien au survol)
- `:active` (lien actif)

### Valeurs de base

Ces valeurs fonctionnent avec la plupart des propriétés CSS :

- `inherit` : la valeur de la propriété correspond à celle de l’élément parent immédiat = permet de forcer l’héritage pour les propriétés que ne s’héritent pas
- `initial` : valeur par défaut d’une propriété = permet d’annuler l’effet d’un héritage. Exemple de valeurs par défaut :
	- `text-align: left`
	- `display: inline`
	- `font-family: sans-serif`
- `unset` : correspond à `inhérit` si la propriété du parent immédiat s’hérite , sinon à `initial`

[https://codepen.io/Ste-Cy/pen/GRqzXOo](https://codepen.io/Ste-Cy/pen/GRqzXOo)

### Propriété all

Permet de spécifier une valeur de base pour l’ensemble des propriétés d’un élément

```css
.initial {
	all: initial;
}

.unset{ 
	all: unset;
}
```

**Attention : cette propriété étant particulièrement radicale, son usage doit rester très limitée.**

## Spécificité et cascade

### Spécificité des sélecteurs

En cas de conflit entre plusieurs déclarations, la priorité se fait selon le poids du sélecteur. 3 niveaux de spécificité :

1. sélecteur d’identifiant (#)
2. sélecteur de classe, de pseudo-classe et d’attribut
3. sélecteur d’élément et de pseudo élément

Remarque : le sélecteur universel (*) , les combinateurs (+ > ~) et la pseudo-classes de négation (:not) n’ont aucun effet sur le poids.

Exemple de tableau de calcul

![](specificite-selecteurs-css.png)

Attention : La priorité ne concerne que les les déclarations qui sont en conflit et pas l’ensemble de la règle

### Notion de cascade

Cascade = combinaison de différentes sources de styles appliqués à un même document selon un ordre de priorité.

Les sources sont par ordre prioritaire :

1. styles personnels de l’utilisateur
2. styles en ligne, directement appliqués sur les éléments avec l’attribut `style`
3. styles définis dans la balise `<style>` ou/et dans un fichier externe lié avec la balise `<link>`
4. styles du navigateur (dépend de l’éditeur)

La règle de cascade n’est appliquée qu’à spécificité égale des sélecteurs.

### Déclaration prioritaire

mot clé `!important` : Rend une déclaration prioritaire sur les autres quel que soit la source et quel que soit le poids du sélecteur. En cas de conflit entre plusieurs déclarations marquées importantes, la règles habituelle s’applique.

```css
#mydiv {
	color: blue !important;
}
```

## Valeurs css

Une valeur CSS passe par 4 étapes :

1. **Valeur spécifiée (Specified Value)** : Il s'agit de la valeur définie dans le code CSS. Si non définie il s'agit de la valeur héritée du parent ou de la valeur initiale de la propriété
2. **Valeur calculée** (**Computed value**) : Conversion des valeurs relatives en valeurs absolues, conversion des couleurs nommés en valeurs RVB, calcul des valeurs indiquées avec un mot clé, etc.
3. **Valeur utilisée (Used value)** : Valeur calculée qui ont besoin d'être calculée pendant le rendu de la page. Il s'agit des valeurs auto ou relatifs à des parents.
4. **Valeur réelle (Actual value)** : Valeur réellement utilisée pour le rendu, avec différentes approximations en fonction des navigateurs ou supports.

**Valeur résolue** : Valeur récupérée avec la méthode JS `getComputedStyle()`. En règle générale il s'agit de la valeur calculée, mais pour certaines propriétés comme `width` ou `height` il s'agit de la valeur utilisée.

## Compatibilité navigateurs

### Préfixes vendeurs

- `webkit-` : Navigateurs basés sur WebKit => Safari, Chrome, nouvelles versions d’Opera et d' Edge, presque tous les navigateurs IOS (y compris Firefox pour IOS)
- `moz-` : Firefox
- `ms-` : Internet Explorer et anciennes versions d' Edge
- `o-` : Anciennes versions d’ Opera

### Règle @supports

Règle conditionnelle qui sera prise en compte que si la propriété CSS est supportée par le navigateur

`@supports (CONDITION) {CODE CSS}`

La condition doit être une déclaration (couple propriété-valeur). Il est possible de combiner des conditions avec les mots clé `and`, `or` et `not`

```css
// Exemple 1
@supports  (hyphens: auto) {
	p {
		hyphens: auto;
	}
} 

// Exemple 2
@supports  (-webkit-filter: sepia(1)) or (filter: sepia(1)) {
	.sepia {
		-webkit-filter: sepia(1);
		filter: sepia(1);
	}
} 

// Exemple 3
@supports not (height: 100vh) {
	html, body {height: 100%; margin: 0; padding: 0}
	.content {min-height: 100%; display: table}
}

@supports  (height: 100vh) {
	.content {height: 100vh;}
}
```

## Propriétés raccourcies

### Valeur initiale et héritage

une valeur qui n'est pas définie pour la propriété raccourcie sera réinitialisée dans sa valeur initiale.

Exemple

```css
background-color: red;
/* 
	la valeur de color n'étant pas définie
	dans la propriété raccourcie, 
	elle sera réinitialisée. 
	La couleur du fond n'est plus rouge 
	mais transparent
 */
background: url(image.png) no-repeat top right;
```

De plus comme les valeurs absentes sont réinitialisées, il n'est impossible d'hériter des valeurs du parent en les omettant.

### Ordre des valeurs

L'ordre des valeurs à indiquer n'a pas d'importance, sauf dans le cas de valeurs de même type.

Les propriétés raccourcis qui gèrent les bord d'une boite (`border`, `margin`, `padding`,…) utilise le schéma suivant :

- 1 valeur : Correspond à tout les côtés
- 2 valeurs : La première correspond aux côté horizontaux (haut et bas) et la deuxième aux côté verticaux (gauche et droit)
- 3 valeurs : La première correspond au côté haut, la deuxième aux cotés verticaux (gauche et droit ) et la troisième au côté bas.
- 4 valeurs : L'ordre est dans le sens horaire ⇒ haut - droit - bas - gauche

Les propriétés raccourcis qui gèrent les coins d'une boite (`border-radius`) utilise le schéma suivant :

- 1 valeur : Correspond à tout les coins
- 2 valeurs : La première correspond aux coins haut/gauche et bas/droit et la deuxième aux coins haut/droit et bas/gauche
- 3 valeurs : La première correspond au coin haut/gauche , la deuxième aux coins haut/droit et bas/gauche et la troisième au coins bas/droit
- 4 valeurs : L'ordre est dans le sens horaire ⇒ haut/gauche, haut/droit, bas/droit, bas/gauche
