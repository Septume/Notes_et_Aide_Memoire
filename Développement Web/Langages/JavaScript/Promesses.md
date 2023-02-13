# Promesses

Objet qui représente l'état d'une opération asynchrone

Les états sont :
- Opération en cours ⇒ promesse en attente (*pending*)
- Opération terminée ⇒ promesse acquittée (*settled)*
	- Avec succès ⇒ la promesse est tenue (fulfilled)
	- Avec échec ⇒ la promesse est rompue (*rejected*)

Avantages : 
- possibilité de chainer les opérations asynchrones
- gestion des erreurs simplifiée


## Créer une promesse
Remarque :  dans la plupart il ne sera pas nécessaire de créer ses propres promesses et on utilisera des promesses déjà générées par des fonctions prédéfinies

On créé un objet `Promise` qui prend en argument une fonction callback qui sera exécutée immédiatement (avant que le constructeur renvoie l'objet créé) 

Cette fonction dite "exécutrice" doit effectuer le traitement asynchrone. Elle prend en argument deux fonctions callbacks 
- Un fonction qui sera exécutée en cas de succès de l'opération asynchrone. Cette fonction doit avoir comme argument le résultat de l'opération asynchrone
- Une fonction qui sera exécutée en cas d'échec. Cette fonction doit avoir comme argument la raison de l'échec de l'opération asynchrone (l'erreur renvoyée par l'opération asynchrone)

Une fois le traitement terminé la fonction exécutrice appelle une de ces deux fonctions pour définir l'état final de la promesse : succès ou échec


```js
const promesse = new Promise((resolve, reject) => {
  // tâches asynchrone à réaliser
  // appel de resolve() si la promesse est résolue
  // appel de reject() si la promesses est rompue
});
```


### Utiliser une promesse

Une instance de `Promise` possède les méthodes suivantes :
- `then()` : Prend deux arguments
	- Une fonction callback à qui est transmis le résultat de l'opération si la promesse a été tenue (exécution de `resolve()` ) 
	- Facultatif : Une fonction de callback à qui est transmis la raison de l'échec si la promesse a été rejetée. (exécution de `reject()` ) 
- `catch()` : Prend comme argument une fonction de callback à qui est transmis la raison de l'échec si la promesse a été rejetée. (exécution que `reject()`) 

Exemple 2

```js
xhrGet('https://jsonplaceholder.typicode.com/posts')
.then(response => {console.log(response);})
.catch(error => {console.error(error);})
```

Il est possible de chainer ces méthodes. En effet la méthode `then()` retourne automatiquement une nouvelle promesse

```jsx
// on récupère les données JSON d'un utilisateur
xhrGet('https://jsonplaceholder.typicode.com/users/1')
// si la promesse est tenue on convertit le JSON en objet et on retourne le résultat
.then(response => {return JSON.parse(response);})
// si la promesse est tenue on affiche le nom de l'utilisateur (propriété name de l'objet)
.then(response => {console.log(response.name);})
// si la promesse est tenue on récupère les posts de l'utilisateur
.then(response => {return xhrGet('https://jsonplaceholder.typicode.com/users/1/posts');})
// si la promesse est tenue on convertit le JSON en objet et on affiche le résultat
.then(response => {console.log(JSON.parse(response));})
// sinon on affiche une erreur dès qu'une promesse est rejetée

```

Remarque : Il est possible de continuer à chaîner après une méthode `catch()` , ce qui peut être utile pour effectuer une autre série d'opération (quelque soit le résultat de la première série)

```jsx
xhrGet('https://jsonplaceholder.typicode.com/users/1')
.then(response => {return JSON.parse(response);})
.then(response => {console.log(response.name);})
.then(response => {return xhrGet('https://jsonplaceholder.typicode.com/users/1/posts');})
.then(response => {console.log(JSON.parse(response));})
.catch(error => {console.error(error);})
// on continue sur une autre série d'opérations (même si il y a eu des erreurs précédement)
.then(response => {return xhrGet('https://jsonplaceholder.typicode.com/users/1/todos');})
.then(response => {console.log(JSON.parse(response));})
.catch(error => {console.error(error);})
```

Il existe également la méthode `finally()` qui prend comme argument une fonction de callback qui est appelée lorsque la promesse a été acquittée (qu'elle ait été tenue ou rejetée). Retourne une une nouvelle promesse. Utile pour exécuter du code une fois que la promesse a été traitée, quelque soit le résultat.

```jsx
xhrGet('https://jsonplaceholder.typicode.com/posts')
.then(response => {console.log(response);})
.catch(error => {console.error(error);})
.finally(() => {console.log("Traitement terminé");})
```

### Traiter plusieurs promesses en parallèle

La méthode `Promise.all()` permet de traiter des opérations asynchrones en parallèle. Elle prend comme argument un tableau de promesses et retourne elle-même une promesse. Cette dernière est :

- Résolue: Si toutes les promesses du tableau sont resolues ⇒ Dans ce cas la fonction de succès transmet un tableau de résultats (Même ordre que les promesses correspondantes)
- Rejetée : Si une seule promesse du tableau est rejetées ⇒ Dans ce cas la fonction d'échec transmet l'erreur correspondant à la première promesse rejetée

```jsx
let promesses = [
  xhrGet('https://jsonplaceholder.typicode.com/users/1'),
  xhrGet('https://jsonplaceholder.typicode.com/users/1/posts')
];

let responses = function(responses){
  responses.forEach(
    function(response) {
      console.log(JSON.parse(response));
    }
  );
}

Promise.all(promesses).then(responses).catch(error => {console.error(error);})
```

### Async et await (spécification es8)

Il s'agit de deux mots clés permettant d'utiliser les promesses avec une syntaxe plus intuitive

`async` : Ce mot clé permet de définir une fonction asynchrone qui retourne systématiquement une promesse. Si une erreur est levée pendant l'exécution alors la promesse est rejetée. Sinon si la fonction retourne explicitement une valeur, la promesse est résolue avec cette valeur.

`await` : A utiliser obligatoirement dans une fonction définie avec le mot clé `async`. Permet de mettre en pause l'exécution du code tant qu'une promesse n'est pas acquittée puis retourne le résultat ou l'erreur de la promesse

Remarque :

- Les fonctions `async` utilisent une `Promise` implicite pour retourner un résultat. Même si une promesse n’est pas retournée explicitement, la fonction async fait en sorte que le code soit passé par une promesse.
- `await` bloque l’exécution du code à l’intérieur d’une fonction async. Il permet de s’assurer que la prochaine ligne soit exécutée quand la promesse est résolue. Donc si du code asynchrone est déjà en train de s’exécuter, `await` n’aura pas d’effet sur lui.
- Il peut y avoir plusieurs `await` à l’intérieur d’une fonction async.
- Il faut bien faire attention lors de l’utilisation d’`await` dans une boucle, car le code peut facilement s’exécuter de manière séquentielle au lieu d’être executé en parallèle.
- `await` est toujours utilisé pour une seule promesse.
- L’utilisation d’async/await permet d’améliorer la gestion d’erreur, car il est possible de gérer les erreurs synchrones et asynchrones en même temps (ce qui n’était pas le cas auparavant), notamment grâce à l’utilisation d’un try/catch.




---------------------------


L'un des principes fondamentaux d'une promesse est qu'elle est gérée de manière asynchrone. Cela signifie que vous ne pouvez pas créer une promesse puis utiliser immédiatement son résultat de manière synchrone dans votre code (par exemple, il n'est pas possible de renvoyer le résultat d'une promesse depuis la fonction qui a lancé la promesse).

Ce que vous voudrez probablement faire à la place, c'est **retourner la promesse entière elle-même.** Ensuite, toute fonction qui a besoin de son résultat peut faire appel `.then()`à la promesse, et le résultat sera là lorsque la promesse aura été résolue.


