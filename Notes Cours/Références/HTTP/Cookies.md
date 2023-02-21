# **Cookies**

Les cookies sont utilisés pour :

- La gestion des sessions
- La personnalisation du contenu
- Le suivi de l'utilisateur
- Le stockage de données

Les cookies sont envoyées par le serveur via un ou plusieurs entêtes HTTP `Set-Cookie` dont la valeur a pour forme `nom-du-cookie=valeur-du-cookie`. La même valeur est utilisé par le client lorsqu'il renvoie le cookie via l'entête http `Cookie`

```
 HTTP/1.0 200 OK
 Content-type: text/html
 Set-Cookie: cookie_1=choco
 Set-Cookie: cookie_2=pepites
```

```
 GET /sample.html HTTP/1.1
 Host: www.example.org
 Cookie: cookie_1=choco; cookie_2=pepites
```

Deux types de cookies :

- Cookies de session : supprimés à la fin d'une session (fermeture du client)
- Cookies permanents: Une date d'expiration est définie (cette date est relatif au client et non pas au serveur)

```
 Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

Options pour la sécurité

- `Secure`: Empêche l'envoi du cookie au serveur si la requête n'est pas en HTTPS.
- `HttpOnly` : Interdit l'accès au cookie via JavaScript (méthode `Document.cookie`). Protège du vol de cookies lors d'une attaque de type cross-site scripting (XSS)
- `SameSite` : politique concernant l'envoi du cookie lors de requêtes cross-origin
	- `Strict` : Le cookie est envoyé uniquement si la requête est de même origine.
	- `Lax` : Le cookie peut être envoyé lors d'une requête cross-origin mais uniquement pour les méthodes sures (lecture seule) comme GET. (Si l'utilisateur accède au site depuis un lien externe, cela permet d'envoyer quand même le cookie de session afin que l'utilisateur soit connecté à son compte)

```
 Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly; SameSite=Lax
```

**Attention : Même sécurisés avec HTTPS, il ne faut jamais stocker des informations sensibles dans les cookies**

Portée des cookies

- `Domain` : hôtes autorisés à recevoir le cookie, sous-domaine compris (Si non indiqué, il s'agit par défaut de l'hôte du document courant (`Document.location`) mais en excluant les sous-domaines)
- `Path` : URL où doit être envoyé le cookie, sous-repertoire compris

```
 Set-Cookie: id=a3fWa; Domain=example.org; Path=/docs
```