```js
event.preventDefault()
```
La méthode **`preventDefault()`**, rattachée à l'interface [`Event`](https://developer.mozilla.org/fr/docs/Web/API/Event), indique à l'agent utilisateur que si l'évènement n'est pas explicitement géré, l'action par défaut ne devrait pas être exécutée comme elle l'est normalement.
empeche le **`submite`** de rafrechir la page.

```js
event.stopPropagation()
```

Évite que l'évènement courant ne se propage plus loin dans les phases de capture et de déploiement.