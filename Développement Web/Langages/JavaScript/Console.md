# Console

Offre des méthodes spécifiques

- `console.log()` : Permet d'afficher une chaine de caractères, la valeur d'une variable ou le résultat d'une expression
- `console.info()`: Pour afficher une information. Cette méthode est dépréciée. Utiliser `console.log()` à la place.
- `console.warn()` : pour afficher un message d'avertissement (s'affiche en jaune)
- `console.error()` : pour afficher un message d'erreur (s'affiche en rouge)
- `console.table()` : Permet de présenter sous forme de tableaux les array et objet
- `console.clear()` : Vide la console
- `conseole.assert()` : Permet de faire un test. Prend en argument une condition est une chaine de caractère à envoyer si la condition est `false`
- `console.time()` : Permet de chronométrer une opération. Prend comme argument un nom (au choix) pour le timer
- `console.timeEnd()` : Permet d'arrêter le chronomètre d'une opération et affiche le temp écoulé dans la console. Prend comme argument le nom du timer défini avec `console.time()`

Exemple

```js
console.assert(2  === 3, 'faux');

console.time('temps')
console.log('Hello');
console.timeEnd('temps') // affiche le temps qu'a pris l'affichage du Hello
```

Remarque : Les spécificités de fonctionnement peuvent varier d'un navigateur à l'autre.