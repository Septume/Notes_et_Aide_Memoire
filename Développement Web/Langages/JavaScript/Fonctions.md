# Fonctions

Rappels :

- Les variables déclarées à l'intérieur d'une fonction sont locales à cette fonction
- Les fonctions ont accès aux variables globales
- Une fonction qui est déclarée à l'intérieur d'une autre fonction a accès aux variables de celle-ci

En javaScript les fonctions sont des objets qui peuvent être :

- affectés à une variable
- utilisés comme argument dans une autre fonction
- retournés comme valeur par une autre fonction

## Définition et appel

```
function nomFonction(param1, param2, ...){
	// instructions; 
return valeur; // facultatif
}
```

Les règles de nommage sont les même que celles des variables

Pour appeler la fonction :  
`nomFonction(argument,…);`

Une fonction peut être appelée avant sa déclaration (hoisting)

```js
// on peut appeler la fonction avant la définition 
resultat = multiplier(5, 7);
console.log(resultat); // affiche : 35

// définition de la fonction
function multiplier(nombre1, nombre2) {
    return nombre1 * nombre2;
}
```

### Valeur de retour

On utilise le mot clé `return` pour retourner une valeur.  
S’il n'y a pas de return, la fonction retourne `undefined`

```js
function message(chaine) {
	console.log(chaine);
}

let valeurRetour = message("Hello world"); // Hello World
console.log(valeurRetour); // undefined 
```

Si on a besoin de retourner plusieurs valeurs on peut utiliser un objet littéral.

```js
function getCoords() {
	return { x: 12, y: 21 }; // objet littéral
}
let coords = getCoords();
alert(coords.x); // 12
alert(coords.y); // 21
```

### Arguments manquants

Si une fonction est appelée avec des arguments manquants, ces derniers auront la valeur `undefined`

```js
function message(texte) {
  alert(texte);
}

message() // Affiche : undefined
message("Bonjour tout le monde")
```

### Valeurs par défaut (spécification es6)

On peut affecter une valeur par défaut à un paramètre de fonction. Cette valeur sera utilisée si lors de l'appel de la fonction l'argument n'est pas indiqué ou explicitement défini à `undefined`

```js
function message(texte = "Hello World"){
  return texte;
}
console.log(message("Salut")); // Salut
console.log(message()); // Hello World
console.log(message(undefined)); // Hello World
```

### Nombre de paramètres indéfini

Il est possible de créer une fonction qui peut prendre autant d'arguments que l'on souhaite.

On utile pour cela un paramètre de reste (Rest parameter) qui va stocker une liste indéfinie de valeur sous forme de tableau. Ce paramètre est sous la forme `…nomParam` et doit absolument être indiqué après les autres paramètres.

```js
function message(...noms){
  for (let i of noms){
    console.log("Bonjour " + i);
  };
}

message("jean","Pierre", "Paul");
```

### Passage des arguments lors de l'appel de fonction

Si l'argument est de type :

- primitif : le passage se fait par valeur => Si la fonction modifie la valeur, cette modification ce fait uniquement au niveau local. Au niveau global la valeur reste inchangée.
- Objet (array, function ou object) : le passage se fait par référence => Si la fonction modifie les propriétés de l'objet, cette modification est répercutée au niveau global.

```js
/***********************************************
	Exemple de passage par valeur (types primitifs) 
***********************************************/

function increment(nb) { 
    return ++nb;
}

let nombre = 1;

console.log(increment(nombre)); 
// affiche 2 (la valeur de la variable nombre incrémentée de 1)

console.log(nombre); 
// affiche 1 (la valeur de la variable nombre n'est pas modifiée)

/*********************************************** 
	Exemple de passage par référence (type Array)
***********************************************/

function modifTab(tab) { 
    // modifie la valeur de la première case d'un tableau
    tab[0] = 2;
}

let tableau = [1, 2];
console.log(tableau); // Array [ 1, 2 ]

modifTab(tableau);
console.log(tableau); // Array [ 2, 2 ] (le tableau a été modifié)
```

## Fonctions anonymes

Fonction qui ne porte pas de nom. En affectant une fonction anonyme à une variable il est possible de l'appeler en utilisant le nom de la variable  
(Dans ce cas la variable contient une référence vers la fonction anonyme et est de type `function`)

```
var variable = function(param1, param2, ...) {
// instructions
};

variable(arg1, arg2,..); 
```

On appelle cette tournure une expression de fonction

Exemple

```js
let message = function (chaine) {
    console.log(chaine);
};

message("Hello World !"); // affiche : Hello World !

Exemple 2
let multiplier = function (nombre1, nombre2) {
    return nombre1 * nombre2;
};

console.log(multiplier(5, 7)); // 35
```

Attention : Dans ce cas il n'est pas possible d'appeler la fonction avant l'instruction concernant l'expression

```js
/* 
Provoque une erreur 
TypeError: message is not a function 
*/

message("Hello World ! ");

let message = function (chaine) {
	console.log(chaine);
};
```

Les fonctions anonymes peuvent être utilisées pour les objets, événements, variables statiques, closures etc…

## Fonctions fléchées

Il s'agit d'une autre syntaxe pour les fonctions qui est plus courte et concise

```
let variable = (parametres...) ⇒ { // instructions };
```

Remarque : Les parenthèses sont optionnels si il y a qu'un seul paramètre (mais obligatoires si il y en a aucun)

Exemple

```js
let carre = nombre => {
  return nombre * nombre;
}; 

console.log(carre(3));
```

Si le corps de la fonction ne contient qu'une expression de retour, on peut omettre les accolades et le mot clé `return`

```js
let carre = nombre => nombre * nombre;
console.log(carre(3));

```

Les fonctions fléchée sont donc particulièrement adaptées à ce cas de figure

Attention : les fonctions fléchées ont un comportement différent avec le `this` que les fonctions classiques ( Voir [[Contexte d'exécution et scope]])

## Fonctions avancés

### Fonctions auto-exécutées

**immediately-Invoked Function Expression (IIFE)** : fonction anonyme directement appelées. Pour créer ce type de fonction on utile deux paires de parenthèses :

- une qui entoure la fonction => permet de désigner la fonction
- une qui se trouve après la fonction avant le point-virgule => permet d’exécuter la fonction

```
(function(parametres…) {
	// instructions;
})(arguments…);
```

On peut affecter la fonction à une variable pour récupérer une valeur de retour

```
let variable = (function(paramètres…) {
	// instructions;
})(arguments…);
```

Ce type de fonction peut être utilisée pour isoler une partie du code afin d'éviter les modifications involontaires de variables globales

```js
/***** code isolé ****/
(function () {
    let variable = 5;
    function carre(nombre) {
        return nombre * nombre;
    }
    console.log(carre(variable)); // 25

})();

/*******************/

// reste du code qui n'est pas affecté 
let variable = "salut";
console.log(variable); // salut
```

## Fonctions de rappel (callback)

Fonction passée en argument d'une autre fonction et qui sera appelée à l'intérieur de celle ci

```js
/* définition de fonctions qui seront utilisées comme callback */

function square(number) {
  return number * number;
}

function sum(number) {
  return number + number;
}

function increment(number) {
  return ++number;
}

/* définition d'une fonction qui utilise une callback */

function process(number, callback) {
  let newNumber = callback(number);
  return newNumber;
}

/* on passe la fonction callback en argument sans indiquer de parenthèses car on ne veut pas l'exécuter mais y faire référence */

console.log(process(3, square)); // Affiche: 9;
console.log(process(3, sum)); // Affiche: 6;
console.log(process(3, increment)); // Affiche: 4;

```

On peut utiliser directement une fonction anonyme comme argument

```js
console.log(process(3, (number) => number * number));
console.log(process(3, (number) => number + number));
console.log(process(3, (number) => ++number));
```

Les fonctions callback sont surtout utilisées dans le cadre d'une opération asynchrone ou pour l'utilisation des évènements.

## Fonction comme valeur de retour

Il est possible d'utiliser la déclaration d'une fonction comme valeur de retour (dans ce cas on utilise une fonction anonyme)

```js
function myFunction() {
 return function (number) {
   return number * 2;
 }
}
console.log(myFunction()); // affiche (number) { return number * 2;}
console.log(myFunction()(2)); // afiche 4
```

## Closures

Consiste à créer une fonction interne à une autre fonction, dite externe. La fonction interne a la possibilité d'accéder aux variables de la fonction externe (l'inverse n'est pas possible) **et ceci même après l'exécution de la fonction externe.**

```js
function externe(){
	let i = 0; 
	/* retourne la référence vers une fonction interne anonyme */
	return function(){
		return ++i; 
	};
}

console.log(externe()); // affiche:  () {return ++i;}

/* on affecte le résultat de la fonction externe à une variable,
ce qui revient à affecter la référence vers la fonction interne anonyme */
let resultat = externe();
console.log(resultat); // affiche  () {return ++i;}


/* on appelle ensuite la variable comme une fonction ce qui permet d'éxecuter la fonction interne anonyme */
console.log(resultat()); // Affiche : 1 => La fonction interne a bien incrémentée la variable même si elle a été appelé après la fonction externe
console.log(resultat()); // Affiche : 2; => La fonction interne continue d'incrémenter la variable à chaque exécution 
console.log(resultat()); // Affiche : 3;
```

Les closures ont pour interêts :

- De protéger une variable de l'extérieur (La variable ne peut être modifiée que par la fonction interne)
- De créer des instances d'exécution indépendance de la fonction externe

```js
function compteur(){
  let i = 0; 
  return function(){
    return ++i;
  }
}

let compteur1 = compteur();
console.log(compteur1()); // 1
console.log(compteur1()); // 2
console.log(compteur1()); // 3

/* nouvelle instance */
let compteur2 = compteur();
console.log(compteur2()); // 1
console.log(compteur2()); // 2
console.log(compteur2()); // 3
```
