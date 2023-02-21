## HTTPs

## Utilisation

- Pas de contenus mixes (contenus servis en HTTP sur une page en HTTPs
- Pas de services tiers avec du contenus mixes ou des certificats non valides
- Tout les sous-domaines doivent être en HTTPS

## Redirections vers HTTPs

Il faut mettre en place une redirection de toutes les URL HTTP vers la version HTTPS

Il faut également utiliser le HTTP Strict Transport Security (HSTS)

### HTTP strict transport security (HSTS)

Entête de réponse envoyée par le serveur pour indiquer au navigateur qu'il doit visiter le site uniquement en HTTPS. Le navigateur enregistre cette information et utilisera automatiquement la version sécurisée du site lors des prochaines visites. (même si l'utilisateur y accède via une URL non sécurisée)  
Par mesure de sécurité, cette entête n'est pas envoyée si le navigateur visite le site en HTTP. Ce mécanisme doit donc être combiné avec une redirection http -> https configurée sur le serveur

### Configuration

Exemple :

```
 Strict-Transport-Security: expireTime=31536000; includeSubDomains; preload
```

- `expireTime` : Durée en seconde pendant laquelle le navigateur doit retenir l'information. Passer ce délais, le navigateur pourra à nouveau utiliser une connexion non sécurisée. Cette information est mise à jour à chaque fois que l'entête est envoyée au navigateur, ce qui permet d'éviter de dépasser le délais d'expiration. Si on indique zéro comme valeur, cela permet de désactiver le mécanisme HSTS.
- `includeSubDomains` : Facultatif. Indique que la règle s'applique également à tout les sous domaine
- `preload` : Facultatif. A indiquer si on souhaite enregistrer son site sur la liste HSTS preload

### Liste HSTS preload

Service mis en place par le projet Chromium qui permet de maintenir une liste de sites valides HSTS, avec les obligations suivantes :

- version sécurisée à l'aide d'un certificat valide
- mise en place de redirections 301 de HTTP vers HTTPS
- tout les sous-domaines sont sécurisés
- directive HSTS avec une validité minimale de 31536000 secondes (1 an) + indication des attributs `includeSubDomains` et `preload`

Cette liste est reconnue par les principaux navigateurs (inscription dans un registre interne) et permet d'effectuer automatiquement une connexion HTTPS dès la première visite.

**[Lien pour soumettre son site](https://hstspreload.org/)**