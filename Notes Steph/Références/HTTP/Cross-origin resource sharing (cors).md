# Cross-origin resource sharing (CORS)

Entêtes HTTP qui permet d'autoriser les requêtes multi-origines pour accéder à des ressources qui par défaut obéissent à la règles du [[Same-origin policy]]

## Fonctionnement

Une page hébergée sur `https://example.com` a besoin de faire une requête HTTP cross-origin pour récupérer des données sur le serveur `https://data.source.org`  
=> le navigateur envoie une requête préliminaire avec l'entête `Origin` qui contient l'URL `http://example.com`  
=> le serveur répond avec l'entête `Access-Control-Allow-Origin`. La valeur doit correspondre à l'origine indiquée dans l'entête `origin` pour autoriser la requête

`Access-Control-Allow-Origin` : permet de spécifier l'origine autorisée à effectuer une requête cross-origin. Il faut indiquer une URL (Il n'est pas possible d'en indiquer plusieurs). Il est possible d'utiliser le caractère `*` comme joker (utiliser seul permet de spécifier n'importe quelle origine)

Exemples :

```
 Access-Control-Allow-Origin: https://example.com
 Access-Control-Allow-Origin: *.example.com
 Access-Control-Allow-Origin: *
```

## Requêtes complexes

Une requête est complexe si :
- Une méthodes autres que `GET`, `HEAD` ou `POST` est utilisée
- L'entête `Content-Type` contient un type MIME qui ne correspond pas à `application/x-www-form-urlencoded`, `multipart/form-data` ou `text/plain`

Ce type de requête nécessite que le navigateur envoie d'abord une requête de contrôle préliminaire (preflight request) afin de demander au serveur des permissions supplémentaires

Cette requête de contrôle utilise la méthode HTTP `OPTIONS` et contient les entêtes :
- `access-control-request-method` : pour demander la permission d'utiliser pour la requête les méthodes HTTP indiquées
- `access-control-request-headers` : pour demander la permission d'utiliser pour la requête les entêtes supplémentaires indiquées

Le serveur répond avec les entêtes :
`Access-Control-Allow-Headers` : indique les en-têtes supplémentaires acceptées (valeurs séparées par des virgule)  
`Access-Control-Allow-Methods` : indique les méthodes acceptées (valeurs séparées par des virgule)

Les valeurs de ces entêtes doivent correspondre à celles envoyées par le navigateur pour que la requête soit acceptée.

Exemple :

```
 Access-Control-Allow-Headers: accept,content-type
 Access-Control-Allow-Methods: DELETE,GET,HEAD,PATCH,POST,PUT
```

`Access-Control-Max-Age`: permet de demander au navigateur de mettre en cache la requête de contrôle pendant une durée indiquée en secondes (Améliore les performance)

Exemple :

```
 Access-Control-Max-Age: 3600
```

## Entêtes de réponses personnalisées

Ce type d'entête ne peut pas être lue par le client sans une autorisation explicite du serveur

`Access-Control-Expose-Headers` : permet d'indiquer les entêtes personnalisées autorisées

Exemple :

```
 Access-Control-Expose-Headers: X-App-Version
```

## Cookies et authentification

Par défaut, les requêtes cross-origin ne permettent pas l'authentification HTTP et l'utilisation de cookies lors d'appel Ajax avec `XMLHttpRequest` ou `Fetch`

Pour l'autoriser il faut utiliser sur le serveur l'entête `Access-Control-Allow-Credentials` qui aura pour valeur `true` et la valeur de `Access-Control-Allow-Origin` ne doit pas être le joker ``

```
 Access-Control-Allow-Credentials: true
 Access-Control-Allow-Origin: https://example.com
```

Coté client il faut également indiqué dans le code l'autorisation des cookies et de l'authentification lors 'une requête cross-origin . Par exemple avec `XMLHttpRequest`, il faut utiliser la propriété `withCredentials` qui doit avoir pour valeur `true`

```
 var req = new XMLHttpRequest();
 req.open("GET", "https://data.source.org");
 req.withCredentials = true;
```

## En résumé 

**headers client** : 
- `Origin` : Le domaine d'origine voulant accéder à la ressource
- `Access-Control-Request-Method` : les méthodes HTTP utilisées (dans le cas d'un pré-contrôle)
- `Access-Control-Request-Headers` : Les headers utilisés (dans le cas d'un pré-contrôle)

**headers serveur :** 
- `Access-Control-Allow-Origin` : Les origines autorisées à accéder à la ressource.
- `Access-Control-Allow-Methods` : Les méthodes HTTP autorisées pour les origines
- `Access-Control-Allow-Headers` : Les entêtes autorisés pour les origines (Authorization etc …)


