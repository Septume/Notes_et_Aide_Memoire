## Map()
La méthode  `map()`  permet facilement d'itérer sur des données et de retourner un tableau d'éléments. Comme elle, les méthodes  `forEach()`,  `filter()`,  `reduce()`, etc., qui permettent de manipuler des tableaux, seront également vos alliés en React.
```js
const numbers = [1, 2, 3, 4]
const doubles = numbers.map(x => x * 2) // [2, 4, 6, 8]
```

## reduce()
La méthode `reduce()` applique une fonction qui est un « accumulateur » et qui traite chaque valeur d'une liste (de la gauche vers la droite) afin de la réduire à une seule valeur.
```js
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue
);

console.log(sumWithInitial);
// Expected output: 10
```
### [Paramètres](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#param%C3%A8tres)

`callback`

La fonction à exécuter sur chaque valeur de la liste (sauf le premier si aucune `valeurInitiale` n'est fournie), elle prend quatre arguments en entrée :

`accumulateur`

La valeur précédemment retournée par le dernier appel du callback, ou `valeurInitiale`, si elle est fournie (voir ci-après) (c'est la valeur « accumulée » au fur et à mesure des appels

`valeurCourante`

La valeur de l'élément courant actuellement manipulé dans le tableau.

`index`Facultatif

L'index de l'élément courant actuellement manipulé dans le tableau.

`array`Facultatif

Le tableau sur lequel on a appelé la méthode `reduce()`.

`valeurInitiale`Facultatif

Une valeur utilisée comme premier argument lors du premier appel de la fonction `callback`. Si aucune valeur initiale n'est fournie, le premier élément du tableau est utilisé (et la boucle de traitement ne le parcourera pas). Si on appelle `reduce()` sur un tableau vide sans fournir de valeur initiale, on aura une erreur.

## forEach()
La méthode **`forEach()`** permet d'exécuter une fonction donnée sur chaque élément du tableau.
```js
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// Expected output: "a"
// Expected output: "b"
// Expected output: "c"
```