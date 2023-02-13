# Traitements asynchrones

`setInterval()` : permet d' exécuter une fonction à intervalle régulier

`setTimeout()` : permet d' exécuter une fonction après un délais

Prend en paramètre une fonction callback et un nombre correspondant à l'intervalle ou délais en ms.

```jsx
/* affiche SetInterval tout les secondes */
setInterval(() => console.log('SetInterval'), 1000);

setTimeout(()=> console.log("5 secondes sont passées"), 5000);
```

Les deux fonctions retournent un entier représentant l'identifiant de l'action. Pour annuler un délais ou une intervalle ou utilise les fonction `clearInterval()` ou `clearTimeout()` qui prend comme argument l'id de la fonction à annuler

```jsx
const interval = setInterval(() => console.log('SetInterval'), 1000);

document.getElementById('stop').addEventListener('click', function(){
  clearInterval(interval);
});
```
