# Routes

Création d'une route = permet d'envoyer une réponse lors d'une requête

## Requête GET

On utilise la méthode `get()` qui prend en argument le path vers lequel est effectué la requête et une fonction callback pour traiter la requête. 
Cette fonction prend deux objets en argument : 
- `res` => représente la réponse. La méthode `send()` permet d'envoyer la réponse et de terminer le traitement.
- `req` => représente la requête

```js
app.get("/", (req, res) => {
  // traitements
});
```


### Retourner les données

#### Retourner une chaine de caractères

```js
app.get("/", (req, res) => {
  res.send("<h1>Hello World</h1>");
});
```

#### Retourner des données au format JSON

On utilise la méthode `res.json()` qui prend en paramètre un objet JavaScript  à convertir en JSON. La méthode se charge ensuite d'envoyer les données

```js
app.get('/', (req, res) => {
  res.json(data);
});
```

#### Retourner un fichier HTML

On utilise la méthode `sendFile()` qui prend en paramètre le chemin absolu du fichier HTML

Pour obtenir le chemin absolu on peut utiliser : 
- La variable `__direname` qui permet d'obtenir le chemin racine  
- La méthode `path.join()` qui permet créer un chemin complet

```js

const path = require('path'); // pour utiliser path.join()
app.get("/page", (req, res) => {
 
  // Utilisation d'une concaténation pour constuire le path (déconseillé)
  // res.sendFile(__dirname + "/public/page1.html");

  // Utilisation de path.join(). permet d'être sur d'avoir une URL correctement formatée même si on un '/' en trop ou manquant
  res.sendFile(path.join(__dirname, "public/page.html"));
});
```


### Utilisation de paramètres

#### Routes dynamiques  

Utilisation de paramètres indiqués sous la forme `:paramName`  
La propriété`req.params` retourne un objet qui contient tous les paramètres passé à l'URL et la valeur associée

```js
// si on entre l'url http://localhost:3000/bonjour/jane/doe
app.get("/bonjour/:prenom/:nom", (req, res) => {
	console.log(req.params); // affiche { prenom: 'jaine', nom: 'doe' }
	const message = `bonjour ${req.params.prenom} ${req.params.nom}`;
	res.send(message);

});
```

Remarque : Les paramètres retournés sont toujours des chaines de caractères

### Paramètres d'URL 

#todo/completer

## Requête POST

#todo/completer 
#todo/verifier


On utilise la méthode `post()`  
La propriété `req.body` retourne un objet contenant les données du formulaire (attributs `name` et valeur associée)

```js
// Obligatoire pour le traitement des formulaires
app.use(express.urlencoded({ extended: true }));


// on indique comme path celui qui est indiqué dans l'attribut action du form 
app.post("/form", (req, res) => {
  console.log(req.body); // objet qui contient les infos envoyés par le form 
  
});
```

Pour convertir les données du body en JSON sur toutes les routes on peut utiliser  le middleware `body-parser` 
Installation : `npm install body-parser`

```js
const bodyParser = require('body-parser');
//***

app.use(bodyParser.json());
```

## Réponse par défaut

Réponse envoyer si aucune route est trouvé

```js
app.use((req, res) => {
	res.status(404).send("Page non trouvée");
});
```
