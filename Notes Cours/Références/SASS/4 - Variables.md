# Variables

### Déclaration et utilisation des variables

`$nom-variable: valeur;`

```scss
$primary-color: #324e85;

.element {
	color: $primary-color;
}
```

Une variable peut être déclarée en dehors des règles CSS ⇒ variable globale accessible partout.

Si une variable est déclarée à l'intérieur d'un bloc de règles, elle sera locale à ce bloc, c'est à dire qu'elle ne pourra être utilisée qu'à l'interieur de ce bloc et de ses blocs enfants

**Attention : Si on redéclare une variable la valeur de celle ci sera écrasée par la nouvelle.**

### Interpolation de variables

Il est possible d'utiliser les variables dans n'importe quel chaine de caractères en utilisant la syntaxe `#{nom-variable}`

```scss
$large-screen: "screen and (min-width: 740px)";

@media #{$large-screen} {};
```

### Types de données

- Chaine de caractères
- Nombre : Avec ou sans unité (px, em,…)
- Couleur (nommée, hexadécimale, RGB/RGBa, HSL/HSLa)
- Listes : Ensemble de valeurs (séparées par des virgules ou espaces). Accepte tout type de données, y compris des listes.
- Map : Liste de paire clé/valeur. S'utilise avec la fonction `map-get()`
- Booléen : `true` ou `false`. S'utilise avec les conditions et boucles
- Valeur `null` : La variable est vide. Lorsqu'une propriété reçoit la valeur `null` elle sera ignorée lors de la compilation

### Opérations arithmétiques

Les 5 opérations (dont le modulo) sont supportées

**Utilisation de la division**

Le signe `/` étant déjà présent dans la syntaxe CSS, ce dernier sera interprété comme le signe de division que si :

- Au moins une des opérandes est une variable
- Si l'opération s'effectue au sein d'une autre opération
- Si l'opération est entourée de parenthèses

```scss
p {
	font: 10px/8px;  // Syntaxe CSS. Pas de division
	height : (400px/2); // Division (utilisation de parenthèses)
	width: $width/2; // Division (utilisation de variable)
	margin-left: 5px + 8px/2px; // Division (opération inclus dans une autre)
}
```

A l'inverse si on utilise le `/` avec des variables mais qu'on ne souhaite pas qu'il soit interprété comme le signe de division, il faut dans ce cas interpoler les variables

```scss
p {
	$fs: 10px;
	$lh : 18px; 
	font: #{$fs}/#{$lh}; // empêche la division
}

// code CSS
p {
	font: 10px/8px; 
}
```

**Utilisation avec des unités**

Il est possible de faire une addition ou une soustraction entre unités différentes mais uniquement si elles sont compatibles.

Dans ce cas c'est l'unité de la première opérande qui sera utilisée et toutes les autres unités seront converties

```
16pt + 10px = 23.5pt
10px + 16pt = 31.3333px 
1em + 2em = 4em 

1em + 2rem = error (unités relatives différentes) 
10px + 3em = error (unité relative non compatible avec une unité absolue) 
```

### Concaténation

Le signe `+` permet de concaténer des chaines de caractères avec tout type de données

```
"Century" + " " + "Gothic" = "Century Gothic"

20 + 10 = 30
2O + "10" = 2010
```
