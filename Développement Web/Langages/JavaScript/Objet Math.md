# Objet math

Toutes les propriétés et méthodes de cet objet sont accessibles directement sans aucune instanciation

`floor(number)` : retourne l'arrondi à l'entier inférieur

`ceil(number)` : retourne l'arrondi à l'entier supérieur

`round(number)` : retourne l'arrondi à l'entier le plus proche

```jsx
console.log(Math.floor(1.2)); // 1
console.log(Math.floor(1.8)); // 1

console.log(Math.ceil(1.2)); // 2
console.log(Math.ceil(1.8)); // 2

console.log(Math.round(1.2)); // 1
console.log(Math.round(1.8)); // 2
console.log(Math.round(1.5)); // 2
console.log(Math.round(1.49)); // 1
```

`max(liste)` : retourne la valeur maximum d'une liste de nombre

`min(liste)` : retour la valeur minimum d'une liste de nombre

```
Math.max(42, 4, 38, 1337, 105); //  1337
Math.min(42, 4, 38, 1337, 105); // 4
```

`pow(nombre, exposant)` : calcul une puissance

`sqrt(nombre)` : calcul une racine carré

```
console.log(Math.pow(5, 3)); // 5^3 = 125
console.log(Math.sqrt(9)); // 3
```

`Math.random()` : retourne un nombre aléatoire compris entre 0 (inclus) et 1 (exclus)

Pour utiliser une autre intervalle il faut faire quelques calculs

```jsx
var min = 1;
var max = 10; 

// nombre decimal compris entre min (inclus) et max (exclus)
var decimal = Math.random() * (max - min) + min;

// nombre entier compris entre min(inclus) et max (exclus)
var entierMaxExclus = Math.floor(Math.random() * (max - min)) + min;

//nombre entier compris entre min(inclus) et max (inclus)
var entierMaxInclus = Math.floor(Math.random() * (max - min +1)) + min;
```
