
### Générer un package.json
```bash
npm init
```

Répondre au questionnaire et valider avec **"Entrer"**.

### Installer Nodemon
Nodemon permet de relancer le serveur automatiquement à chaque sauvegarde enregistrer.

```bash
npm install -g nodemon
```
 et ajouter 
```js
"start": "node ./server.js"
```
dans `"scripts"` du fichier `package.json` afin de lancer le serveur uniquement avec la commande **npm start**.


### Installer Express
```bash
npm i express
```


### Gitignore
Créer une fichier `.gitignore` et ajouter :
```
node_modules
```

`.gitingnore` permet d'ignorer les fichiers et dossiers nommés pendant les **commits Git** et économiser de la place.

### Serveur
Créer un fichier `server.js` à l'intérieur du dossier `backend` . Il contiendra le premier serveur Node et copier :
```js
const http = require('http');

const server = http.createServer((req, res) => {
    res.end('Voilà la réponse du serveur !');
});

server.listen(process.env.PORT || 3000);
```


### Installer CORS
CORS (Cross-Origin Resource Sharing) est un mécanisme de sécurité côté client qui permet à un navigateur web de restreindre les requêtes HTTP provenant d'un domaine différent de celui du serveur d'origine. En d'autres termes, il permet à un serveur d'autoriser des requêtes provenant d'un domaine différent de celui sur lequel il est exécuté.

```bash
npm install cors
```
