Pour utiliser CORS dans une application Node.js, vous pouvez suivre ces étapes:

1.  Installer le package middleware "cors" à l'aide de npm (Node Package Manager):
```js
npm install cors
```

2.  Ajouter le middleware "cors" à l'application Node.js:
```js
const express = require('express'); 
const cors = require('cors');  

const app = express();  app.use(cors()); 
```
 
Cela permettra à l'application d'autoriser toutes les requêtes provenant de n'importe quel domaine.

3.  Configurer les options d'autorisation pour les requêtes entrantes:
```js
const express = require('express'); 
const cors = require('cors');  

const app = express();  

app.use(cors({     
	origin: 'http://example.com',     
	optionsSuccessStatus: 200 
}));
```

Cela permettra à l'application d'autoriser les requêtes provenant uniquement de "[http://example.com](http://example.com/)" et de renvoyer une réponse avec un code de statut 200 pour les requêtes pré-vérifiées (OPTIONS).


Il existe plusieurs options que vous pouvez configurer en utilisant le middleware "cors". Consultez la documentation du package "cors" pour en savoir plus.