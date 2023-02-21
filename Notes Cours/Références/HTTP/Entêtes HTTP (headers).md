# Entêtes HTTP (headers)

Informations supplémentaires transmises par le client ou le serveur et indiquées sous la forme `Nom-Entete: valeur`

## Quelques entêtes

Entêtes de requête ou de réponse :
- `Date` : Date et heure du message
- `Cache-Control` : Permet de définir la politique de mise en cache du contenu

Entêtes de requête ou de réponse quand le message contient un corps :
- `Content-Type` : Type MIME et jeu de caractères des données envoyées par le client ou le serveur (ex : `text/html; charset=utf-8`)
- `Content-Encoding` : Encodage des données envoyées par le client ou le serveur
- `Content-Length` : Taille en octets des données envoyées par le client ou le serveur

Entêtes de requête :
- `Host` : Nom d' hôte dans le cas d'un hébergement virtuel (Virtual Host). On peut également précisé le numéro de port sous la forme `host:port`. Cet entête est obligatoire pour des requêtes HTTP 1.1.
- `Accept` : Types de contenu acceptés par le client. La valeur est une liste de types MIME (Ex: `text/html, application/xhtml+xml`)
- `Accept-Charset` : Jeu de caractères souhaité par le client. (Ex: `utf-8`)
- `Accept-Encoding` : Encodage de données accepté par le client (Ex : `gzip, compress, br`)
- `Accept-Language` : Langue du contenu souhaité par le client (Ex : `fr-FR, fr, en-US, en`)
- `Authorization` : Les identifiants de connexion lorsqu'une authentification est requise pour accéder aux ressources du serveur. Le serveur envoie d'abord un message avec le statut `401 Unauthorized`et indique dans l'entête `WWW-Authenticate` la méthode d'authentification à utiliser. La méthode `Basic` est celle qui est le plus souvent utilisée. Elle permet d'encoder l'identifiant et le mot de passe (sous la forme `user:password`) en base64. (Attention : Cette méthode n'étant pas sécurisée la transaction doit se faire en HTTPS). Sur certains clients il est possible de se connecter directement sans passer par une boite de dialogue en utilisant une URL sous la forme `https://user:password@<www.example.tld>`
- `cookie` : Contient les cookies HTTP
- `Referer` : URL de la page précédente sur laquelle l'utilisateur a suivi un lien pour arriver sur la page courante. Par défaut cette information n'est pas envoyée si la page précédente a été reçue en HTTPS et que le requête courante est en HTTP
- `User-Agent` : Signature de l'agent utilisateur. Les informations peuvent être le type d'application, l'éditeur et la version du logiciel, le nom du système d'exploitation, le type d'appareils, etc.

Entêtes de réponse :
- `Server` : Identité du serveur (Nom, version, OS). L'information peut être partielle ou absente pour des raisons de sécurité.
- `Set-Cookie` : Permet d'envoyer des cookies au client
- `Location` : Indique une URL de redirection
- `Expires` : Date d'expiration de la ressource. La valeur `0` signifie que la ressource est expirée. (Sous Apache, ce champ n'est pas géré par défaut, il faut activer le `mod_expires` et le configurer)
- `Last-Modified` : Date de la dernière modification de la ressource. Cette information peut être utilisée par le client pour effectuer des requêtes conditionnelles avec les entêtes `If-Modified-Since` et `If-Unmodified-Since`
- `ETag` : Identifiant pour une version spécifique d'une ressource. Si la ressource et modifiée une nouvelle valeur `Etag` est générée. Cette information peut être utilisée par le client pour effectuer des requêtes conditionnelles avec les entêtes `If-Match` et `If-None-Match`
- `X-Frame-Options` : Permet de régler les autorisations concernant le chargement de la page dans un iframe
	- `DENY` : interdiction
	- `SAMEORIGIN` : autoriser depuis la même origine
	- `ALLOW-FROM <URI>` : autoriser depuis L'URL indiqué
	- `ALLOWALL` : autoriser depuis n'importe quelle origine
- `Referrer-Policy` : Politique concernant le referrer envoyé lors d'une requête

## Configuration sur le serveur

3 moyens de modifier les entêtes de réponse envoyés par le serveur :

- Via la configuration globale du serveur
- En utilisant un fichier `.htaccess` (Sous Apache)
- En utilisant un langage serveur comme PHP

Exemple sous Apache (via `mod_headers`) :

`Header always set X-Frame-Options "SAMEORIGIN"`

## Utilisation avec PHP

Quelques fonctions :

- `header()` : permet de spécifier à la main un en-tête de réponse et éventuellement de changer le code de réponse HTTP
- `headers_sent()` : indique si les en-têtes de la réponse ont déja été envoyés au client ou pas
- `setcookie()` : envoie un entête `Set-Cookie` dans la réponse
- `session_start()` : envoie des entêtes pour la gestion de la session : cache, cookie, etc…
- `headers_list()` : récupère la liste des entêtes à envoyer dans la réponse courante
- `apache_response_headers()` : récupère la liste des en-têtes à envoyer dans la réponse courante, plus précise que `headers_list()`, mais nécessite de tourner sous module apache
- `get_headers()` : récupère les en-têtes de la réponse à une requête fournie

Concernant les en-têtes de la requêtes, PHP en propose un aperçu dans la super globale `$_SERVER`, ou via `apache_request_headers()