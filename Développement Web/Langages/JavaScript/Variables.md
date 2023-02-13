# Variables

## Déclaration et affectation

Une variable déclarée mais non initialisée a pour valeur `undefined`

L' utilisation d'une variable non déclarée provoque une erreur `ReferenceError`

### Avec le mot clé var (ancienne syntaxe)

`var variable = valeur;`

### Avec le mot clé let (nouvelle syntaxe es6)

`let variable = valeur;`

Les variables déclarées avec `var` dans une structure de contrôle (condition ou boucle) ont une portée globale ce qui pour entrainer des effets de bords

Le mot clé `let` (spécification ES6) permet de déclarer une variable locale à un bloc

```jsx
// variable i globale
for (var i = 0; i <= 3; i++) {
    console.log(i); // 0 1 2 3 
}
console.log(i); // 4

// variable j locale
for (let j = 0; j <= 3; j++) {
    console.log(j); // 0 1 2 3
}
// console.log(j); => ReferenceError :  j is not defined
```

### Constantes (spécification ES6)

Une constante ne pas être réaffectée, c'est à dire que la référence vers la valeur ne peut pas être changée. Par contre la valeur en elle même peut être modifiée. Par conséquent si on affecte un tableau ou un objet à une constante, on pourra toujours modifier son contenu (changer les propriétés, etc…).

L'affection d'une valeur est obligatoire pour les constantes.

`const contante = valeur;`

La réaffectation d'une constante provoque une erreur : `TypeError`

Remarque : il est recommandé d'utiliser en priorité le mot clé `const` pour déclarer une variable, sauf si on a absolument besoin de réaffecter une valeur à celle-ci. (La bonne pratique étant de limiter au maximum les réaffectations de variable)

### Recommandations

- Ne plus utiliser `var`
- Toujours utiliser le `const`
- Si on a besoin de réassigner une valeur, changer le `const`pour un `let`

### Règles de nommage

- Peut comporter uniquement des lettres, des chiffres et les caractères underscore ( _ ) et dollars ( $ )
- Ne peut pas commencer par un chiffre

Convention de nommage :

- camelCase
- nom au pluriel pour les tableaux

## Types de variables

Le JavaScript est un langage typé dynamiquement

### Types primitifs

- `number`
- `string` ( valeur contenu entre apostrophes ou guillemets)
- `boolean` (`true` ou `false`)
- `symbol` (ES6 - Représente une donnée unique et inchangeable. Surtout utilisé pour créer des identifiants pour les propriétés d'un objet)
- `undefined` (variable non initialisée => La variable existe mais aucune valeur lui a été affecté)
- `null` (variable initialisée mais ne pointant sur aucun objet)

Les types primitifs sont copiés par valeur

```js
let x = 1;
console.log(x); // affiche 1
let y = x; // on copie la valeur de x dans y
console.log(y); // affiche 1
x = 2; 
console.log(x); // affiche : 2
console.log(y); // affiche : 1 
```


### Types objets

- `object`
- `array`
- `function`

Les types objet sont copiés par référence 

```js
let x = [1, 2, 3];
console.log(x); // affiche [1,2,3]
let y = x; // on copie la référence de x dans y
console.log(y); // affiche [1,2,3]


/* x et y pointant vers la même référence la modification de la valeur de l'un entraine la modification de la valeur de l'autre */

x.push(4);  
console.log(x); // affiche : [1,2,3,4]
console.log(y); // affiche : [1,2,3,4]

y.push(5);
console.log(x); // affiche : [1,2,3,4,5]
console.log(y); // affiche : [1,2,3,4,5]

x = []; // x pointe vers une nouvelle référence
console.log(x); // affiche : []
console.log(y); // affiche : [1,2,3,4,5]
```

### Tester le type d'une variable

On utilise l'opérateur `typeof`

```jsx
let nombre = 0;
console.log(typeof nombre); // number 

let variable
console.log(typeof variable); // undefined;

console.log(typeof 1); //number
console.log(typeof "Hello world"); // string 
console.log(typeof true); // boolean
console.log(typeof [1,2,3]); // object
console.log(typeof function(){}); //function
```


## Conversion de type

### **Convertir une chaine de caractère en nombre**

`parseInt()` : fonction qui convertie une chaine de caractère en nombre entier. Prend deux arguments :

- la valeur à convertir. Si cette valeur n'est pas de type string, elle sera convertie en chaine de caractères.
- la base numérique utilisée par la valeur représentée par la chaine (Nombre compris entre 2 et 36)

`parseFloat()` : fonction qui convertie une chaine de caractère en nombre flottant. Prend comme argument la valeur à convertir.

Remarque : Si la chaine débute par un ou plusieurs chiffres suivi de caractères non numérique, ces derniers seront supprimés (y compris les éventuels chiffres se trouvant après ces caractères non numériques).  
Par contre si la chaine ne débute pas par un chiffre celle-ci ne pourra être convertie. Dans ce cas la fonction retourne la valeur `NaN` (Not A Number) et ceci malgré le fait que la fonction `typeof()` indique que la variable est de type `number`

`isNaN()` : fonction qui prend en argument une chaine et retourne `true` si elle ne représente pas un nombre.

```jsx
 console.log(parseInt("5.5", 10)); // 5
 console.log(parseInt("10", 2)); // 2
 console.log(parseFloat("5.5")); // 5.5
 console.log(parseInt("10abc4", 10)); // 10
 
 let test = parseInt("abc10", 10);
 console.log(test); // NaN
 console.log(typeof test) // number
 
 console.log(isNaN("toto")); // true
 console.log(isNaN("10abc4")); // true
 console.log(isNaN("abc10")); // true
 console.log(isNaN("10")); // false
 
 
```

### **Convertir un nombre en chaîne de caractères**

Concaténer un nombre avec une chaîne de caractère vide permet de le convertir en chaîne de caractères.  
On peut également utiliser les méthodes :

- `Number.toString()` : converti un nombre en chaine de caractères
- `Number.toFixed()` : converti un nombre en chaine de caractères en limitant le nombre de décimale (indiqué en paramètre)

```jsx
 let a = 5 + "";
 let b = 9.5.toString();
 let c = 3.14159265359.toFixed(2);
 console.log(c); // 3.14
```

## Affectation par décomposition (spécification es6)

L'affectation par décomposition (*destructing*) permet d'extraire des données d'un tableau ou d'un objet pour les affecter à plusieurs variables

### Décomposition d'un tableau

On utile une syntaxe proche de celle des tableaux

```jsx
let tab = ["pim", "pam", "poum"];

/* on créé deux variables qui récupèrent 
les deux premières valeurs du tableau */

let [item1, item2] = tab; 

console.log(item1); // pim
console.log(item2); // pam
```

On peut également affecter le reste des données d'un tableau avec la syntaxe `…`

```jsx
const tab = ["pim", "pam", "poum"];
const [item1, ...item2] = tab; 

console.log(item1); // "pim"
console.log(item2); // ["pam", "poum"]
```

### Décomposition d'un objet

On utile une syntaxe proche d'un objet et des noms de variables qui sont les mêmes que les noms des propriétés de l'objet. On peut aussi utiliser la syntaxe `…` et un nom de variable au choix pour récupérer le reste des données

```jsx
const personne = {
  pseudo : "toto",
  age : 10,
  mail : "toto@mail.tld",
  ville : "Neverland"
}

const {pseudo, mail, pays,  ...rest} = personne;
console.log(pseudo); // "toto"
console.log(mail); // "toto@mail.tld";
console.log(rest); // [object Object] {age: 10, ville: "Neverland" }
console.log(pays); // undefined (car la propriété 'pays' n'existe pas)
```

