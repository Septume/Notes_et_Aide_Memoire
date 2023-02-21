# NodeJS - Intro

Environnement d'exécution qui permet de développer des applications JavaScript coté serveur.  
Utilise le moteur V8 de Chrome

Avantages :

- Utilisation d'une stack full JavaScript + support natif du JSON
- Rapidité grâce au moteur V8
- Approche évènementielle (event based)
- traitement asynchrones (non bloquant ) => idéal pour les micro-services

Inconvénients :
- avant la version 12 : Mono thread
- Depuis la version 12 : multi-threading possible mais pas natif au langage


## Créer un projet NodeJS 

Créer un fichier _app.js_  => point d'entrée de l'application NodeJS
Pour exécuter ce fichier : `node app.js`

 Fichier _package.json_ : Permet de
-   Indiquer les informations du projet (nom, description, auteur, etc.)
-   lister les dépendances nécessaires
-   mettre en place des scripts  

Pour générer un fichier *package.json* : `npm init`  (Puis répondre aux questions)
Pour installer les dépendances d'un projet (indiqués dans le fichier _package.json_) : `npm install`

## Importer un module

Node utilise le système de module CommonJS qui utilise le mot clé `require` (plutôt que le mot clé `import` utilisé avec la norme ES6) ce qui permet d'importer un module sans avoir besoin de spécifier le chemin exact du fichier.  
Le mot clé `require` permet également d'importer des fichiers.

```js
// Importer un module (depuis le dossier node_modules)
const NomMondule = require('nomModule')

// Importer un fichier (indiquer le chemin relatif)
const nomFichier = require('./path/fichier)
```


## REPL

Read-Eval-Print Loop (Boucle de Lecture-Évaluation-Impression) = > invite de commande interactif de Node  
Pour lancer REPL lancer la commande `node`  
Utiliser les touches fléchées pour naviguer dans l'histoire des commandes et tab pour l'autocomplétion (utiliser deux fois tab pour avoir une liste de commande)
Utiliser `CTRL + C` pour annuler un traitement

Commandes spéciales :

- `.exit` (ou `CTRL + D`)
- `.clear`
- `.help`
- `.break` ou `CTRL + C` : lors de la saisie d'une expression multilignes, interrompt le traitement de cette expression
- `.save <PATH>` : enregistre la session REPL dans un fichier
- `.load <PATH>` : charge un fichier enregistré
- `.editor` : Mode éditeur. `CTRL + D` pour sortir.
- `_` : Afficher la dernière valeur évaluée



## Variables d'environnement

La propriété `process_env` permet d'accéder aux variables d'environnement

## Créer un serveur

```js
/*****  création d'un serveur *****/

const http = require("http");
const server = http.createServer((req, res) => {
  // traitenemnts des requêtes
});

/**** le serveur est en écoute des requetes ****/

// préciser le numéro de port
// utiliser la variable env PORT si définie sinon utiliser 3000
const PORT = process.env.PORT || 3000;
server.listen(port, hostname, () => {
  // la fonction est exécutée que si le serveur a bien démarré
  console.log(`Server is listening on port ${PORT}`);
```



La méthode `createServer()` prend comme argument une fonction qui sera exécutée à chaque requête vers le serveur.
Tout les traitements de requêtes doivent être indiqués dans cette fonction quelque soit le type de requête ou l'URL appelée.


```js
// req => objet request
// res => objet response

const server = http.createServer((req, res) => {
	// Envoyer le code de réponse
	res.statusCode = 200;
	// Envoyer une entête pour régler le content-type
	res.setHeader("Content-Type", "text/plain"); // texte brut
	// pour terminer envoyer la réponse (quelque soit la requête)
	res.end("Hello World"); 
});
```

l'objet `req` permet de gérer les requêtes

```js
const server = http.createServer((req, res) => {
  if (req.url === "/bonjour") { // si l'URL demandé est domaine.tld/bonjour 
    res.end("Bonjour"); // envoie cette réponse
  } else {
    res.end("Hello"); // dans les autres cas envoie cette réponse
  }
});
```

## Event loop

Processus qui est lancé lors de l'exécution d'un script et qui s'occupe de gérer les traitements asynchrones
