# Requêtes et réponses HTTP

Mécanisme :

1. Le client envoie une requête au serveur (via une connexion TCP sur le port 80)
2. le serveur prépare la réponse
3. le serveur envoie la réponse au client

## Requêtes

Une requête comprend les éléments suivants :

- Une ligne indiquant :
	- La méthode HTTP utilisée
	- L' URL de la ressource concernée
	- La version du protocole HTTP utilisé
- Éventuellement un ou plusieurs entêtes HTTP
- Pour les méthodes `POST` et `PUT` un corps contenant les données envoyées.

Exemple de requête :

```
 GET / index.html HTTP/2.0
 Host: www.google.com
 User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:60.0)Gecko/20100101 Firefox/60.0
 Accept-Language: fr
```

Les méthodes de requête HTTP :
- `GET` : Pour récupérer une ressource sur le serveur
- `HEAD` : Similaire à `GET` mais permet de récupérer que les entêtes (Le corps ne sera pas envoyé par le serveur)
- `POST` : Pour envoyer des données sur le serveur qui seront traités dans le but de créer ou modifier une ressource. Le type du corps de la requête est indiqué par l'en-tête `Content-Type`.  Si les données sont envoyés via un formulaire HTML le type est : 
  - `application/x-www-form-urlencoded` 
  - `multipart/form-data`  (Pour les formulaires avec envoie de données binaires) 
- `PUT` : Pour créer ou remplacer une ressource. La différente avec `POST` est que `PUT` modifie directement la ressource sans passer par une ressource intermédiaire chargée du traitement. Si la ressource existe à L'URL indiquée elle sera remplacée sinon elle sera créé. 
`PUT` est idempotent => si on effectue plusieurs fois la même requête cela n'entrainera pas d'effet de bord comme la création de plusieurs ressources identiques mais avec des URL distinct. 
- `PATCH` : Pour modifier partiellement une ressource
- `DELETE` : Pour supprimer une ressource

Opérations CRUD 
- `Create` => `PUT` ou `POST` 
- `Read` => `GET` 
- `Update` => `PUT` ou `PATCH` 
- `Delete` => `DELETE` 

## Réponses

Une réponse comprend les éléments suivants :

- Une ligne indiquant :
	- La version du protocole HTTP utilisé
	- Le code de statut
	- Le message de statut
- Éventuellement des entêtes HTTP
- En fonction du type de requête : un corps contenant les données reçus

Exemple de réponse :

```
 HTTP/2.0 200 OK
 date: Mon, 28 May 2018 10:42:41 GMT
 Server: Apache/2.2.29
 content-type: text/html
```

Codes de statut :

- 2xx : Succès
	- `200 OK` : La requête a réussi
	- `201 Created` : La requête a réussi et une nouvelle ressource a été créée (Requête `PUT`). L'entête `Location` précise l'URL de la ressource
	- `202 Accepted` : La demande de création de ressource a été prise en compte et en cours de traitement (Requête `POST`). Le contenu de la réponse décrit l'état du traitement.
- 3xx : Redirection
	- `301 Moved Permanently` : Indique que la ressource a été définitivement déplacée à l'adresse indiquée dans l'entête `Location`. (Le navigateur redirigera automatiquement vers la nouvelle adresse et les moteurs de recherche mettront à jour leur index )
	- `302 Found` : Indique que la ressource a été temporairement déplacée à l'adresse indiquée dans l'entête `Location`. (Le navigateur redirigera automatiquement vers la nouvelle adresse par contre les moteurs de recherche ne mettront à jour leur index )
- 4xx : Erreurs du client
	- `400 Bad Request` : Syntaxe de la requête invalide
	- `401 Unauthorized` : Une authentification est requise
	- `403 Forbidden` : Accès interdit
	- `404 Not Found` : Ressource non trouvée (lien brisé)
	- `408 Request Timeout` : Temps d’attente d’une requête client écoulé
	- `409 Conflict` : La requête entre en conflit avec l'état actuel du serveur ( Les conflits se produisent généralement en réponse à une requête `PUT`)
- 5xx : Erreurs du serveur
	- `500 Internal Server Error` : Le serveur a rencontré un problème l'empêchant de répondre à la requête.
	- `502 Bad Gateway` : Le serveur est utilisé comme passerelle et à reçu une réponse invalide depuis le serveur en amont.
	- `503 Service Unavailable` : Le service est temporairement indisponible (La requête ne peut pas être traitée)
	- `504 Gateway Timeout` : Le serveur est utilisé comme passerelle et temps d'attente de la réponse du serveur en amont est écoulé.