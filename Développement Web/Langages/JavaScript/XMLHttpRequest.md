
# Objet XMLHttpRequest

Permet de créer des requêtes HTTP en JavaScript.

4 étapes :
- Création d'un objet `XMLHttpRequest`
- Initialisation de la requête
- Envoi de la requête
- Traitement de la réponse du serveur


## Initialisation et envoi de la requête
on utilise la méthode `open()` qui prend en argument : 
- Le type de requête HTTP : `GET`, `POST` , `PUT` ou `DELETE`
- l'URL cible (chemin relatif ou absolu)
- Facultatif : Un booléen indiquant si la requête est asynchrone. Par défaut `true` (Remarque : les requêtes synchrones sont fortement déconseillées et considérées comme obsolètes)
- On peut également indiquer en 4ème et 5ème argument un nom d'utilisateur et un mot de passe pour l'authentification 

Il faut ensuite spécifie le format dans lequel le serveur doit envoyer la réponse avec la propriété `responseType` . Les valeurs possibles sont  : 
- `""` (Chaine de caractère vide) ou `"text"` : Défaut. La réponse est envoyé sous forme de chaine de caractères
- `"json"` : La réponse est envoyée dans le format JSON
- `"document"` : La réponse est envoyée sous forme de document XML
- `"blob"` : La réponse contient des données binaires (images, vidéos, etc…)

Pour terminer on utilise la méthode `send()` pour envoyer la requête 
- Pour une requête `GET` ou `DELETE` : Ne prend pas d'argument
- Pour une requête `POST` ou `PUT` : Prend comme argument les informations à envoyer au serveur

```js
// création de l'objet
var xhr = new XMLHttpRequest();

// initialisation de la requête
xhr.open('GET', 'https://jsonplaceholder.typicode.com/users');

// type de reponse attendu
xhr.responseType = "json";

// envoi de la requête
xhr.send() 
```


## Traitement de la réponse 

Pour traiter la réponse on se base sur des évènements
- `load` : se déclenche lorsque la requête a bien été effectuée et que le résultat est prêt. 
-  `error` se déclenche lorsque la requête n’a pas pu aboutir
-   `progress` se déclenche à intervalles réguliers e permet de savoir où en est la requête

Il faut prend en compte deux cas d'erreurs : 
- Échec lors de l'envoi de la requête (nom de serveur incorrect, problème réseau, etc.). Déclenche un événement `error` sur la requête
- Échec lors du traitement par le serveur (ressource non trouvée, problème interne du serveur, etc.) : On utilise dans ce cas le code de retour HTTP pour prendre en compte l'erreur.


Pour le traitement on peut utiliser les propriétés : 
-  `response`  : contient la réponse du serveur sous le format spécifié par `responseType` 
- `readyState` : retourne un numéro correspondant à l'état de la requête
	- 0 : Requête non initialisée
	- 1 : Connexion établie
	- 2 : Requête reçue
	- 3 : Requête en cours de traitement
	- 4 : La réponse est prête
- `status` : Code de retour HTTP
- `statusText` : Code retour HTTP sous forme textuel (ex : `200 OK`)



```js
// Si la requête n'a pas abouti

xhr.addEventListener("error", function () {
	console.error("Erreur reseau");
});

// si la requête a abouti

xhr.addEventListener("load", function () {
  // la requête a été traité avec succès 
  if (xhr.status === 200) { 
    // on affiche la réponse
    console.log(xhr.response);
	} else {
		// sinon on affiche les raisons de l'echec 
		console.error("Erreur serveur : " + xhr.status + " - " + xhr.statusText);
	}
});
```

On peut utiliser le gestionnaire d'évènement `onreadystatechange` qui est attaché à un objet XHR et qui est appelé à chaque changement de valeur la propriété `readyState`. On affecte à ce gestionnaire une fonction anonyme chargée d'effectuer les traitements.

```js
xhr.onreadystatechange = function () {
	console.log(xhr.readState);
};
```


## Envoyer des données

### Envoyer des données JSON

Il faut modifier l'entête HTTP `Content-Type` pour indiquer que les données envoyées sont au format JSON

La méthode `setsetRequestHeader()` permet de régler le content-type 

```jsx
// objet 
var personne = {
    nom: "Dupont",
    prenom: "Jean",
    mail: "jean.dupont@monmail.com"
};

// on convertie l'objet au format JSON
var data = JSON.stringify(personne);

var xhr = new XMLHttpRequest();
xhr.open("POST", "http://site.tld/file.php");
/* on indique que les données envoyés sont au format JSON */
xhr.setRequestHeader("Content-Type", "application/json");
xhr.send(data);
```

### **Objet formdata**

Permet de créer un ensemble de paires clé/valeur, représentant les attributs `name` et `value` d'un champ de formulaire. Cet objet peut toutefois être utilisé indépendamment d'un formulaire.

Le constructeur peut prendre comme argument un élément `form` (Facultatif )

La méthode `append(name, value)` permet d'ajouter une paire clé/valeur à l'objet `FormData`

Exemple avec formulaire

```jsx
var form = document.getElementById("form");

form.addEventListener("submit", function (e) {
    e.preventDefault();
    var data = new FormData(form);
		// CODE XHR
		// xhr.send(data);
});
```

Exemple sans formulaire

```jsx
var data = new FormData();
data.append("nom", "Dupont");
data.append("age", "43");

// CODE XHR
// xhr.send(data);
```






