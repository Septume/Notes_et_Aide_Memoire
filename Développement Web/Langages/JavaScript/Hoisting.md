# Hoisting (hissage)

## Variables

**Attention : Ne concerne que les variables déclarées avec `var`**

JavaScript a la particularité de traiter d'abord les déclarations de variables avec `var` avant le reste du code et ceci quelque soit leurs emplacements. Plus précisément :

- Les déclarations de variable globales sont "remontées" en début de script pour être traité en premier.
- Les déclarations de variables locales à une fonction, sont "remontées" en début de la fonction

```
Ecrire : 
variable = valeur; 
var variable; 

Revient à Ecrire : 
var variable; 
variable = valeur;
```

Attention, l'hoisting ne concerne que la déclaration, pas l'initialisation

```
Écrire :
var variable = "valeur";

Revient à écrire : 
Var variable; 
variable = "valeur"
```

Exemple

```jsx
/* ce code fonctionne
car la déclaration de la variable
est traité en premier */

a = "Hello"; 
console.log(a); // "Hello"; 
var a; 

/* La variable est affichée 
alors qu'elle n'est pas encore initialisée */ 

console.log(b); // undefined
var b = "Hello";

console.log(b); // "Hello"
```

## Fonctions

Les fonctions sont également concernés par le hoisting. Les déclarations de fonctions sont traitées avant le reste du code, ce qui fait qu'il est possible d'appeler une fonction avant sa déclaration

```jsx
// on peut appeler la fonction avant la définition 
resultat = multiplier(5, 7);
console.log(resultat); // affiche : 35

// définition de la fonction
function multiplier(nombre1, nombre2) {
    return nombre1 * nombre2;
}
```

Attention : Le hoisting ne concerne pas les expressions de fonction du type `let variable = function() {}`
