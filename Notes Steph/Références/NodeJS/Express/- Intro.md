# Express

Framework qui facilite la création d'un serveur NodeJS et la gestion des requêtes

Installation dans le projet : `npm install express`

## Exemple code minimal

```js
const express = require('express'); // importation d'express

const app = express(); // création d'une instance d'une application express
const port = 3000; // port d'écoute

// définition d'une route
app.get('/', (req, res) => res.send('Hello World'));

// // démarrage l'application sur le port indiqué (avec message d'information)
app.listen(port, () => {
  console.log(`Serveur lancé sur le port ${port}`);
});
```



## Variables d'environnement

`NODE_ENV` : Permet de spécifier l'environnement dans lequel l'application Express est exécutée 

Par convention on utilise comme valeur : 
- `development` 
- `production` 


Lors de la mise en ligne de l'application il est fortement recommandé de définir cette variable sur `production` pour améliorer les performances

Pour définir une valeur pour `NODE_ENV`  sur le système

```
__Linux et OSX__
export NODE_ENV=production

__Windows__
$env:NODE_ENV = 'production'
```

Il est également possible de définir `NODE_ENV` dans le script de démarrage

```JSON
"scripts": {
  // fonctione que sous Linux et OSX
    "start": "NODE_ENV=production node server.js",
    "dev": "NODE_ENV=development nodemon server.js",
  },
```


Pour accéder à `NODE_ENV` on peut utiliser `process.env` 

```JS
var environment = process.env.NODE_ENV;
 if(environment === 'production') {
   // Code
  }
```

