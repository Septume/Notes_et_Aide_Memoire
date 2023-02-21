# Cache HTTP

Permet de stocker une copie des données dans le but d'éviter le re-téléchargement de celles-ci afin d'économiser la bande passante et les ressources serveur.

Deux types de cache :

- Caches privés : cache du client (navigateur, agent utilisateur)
- caches publics partagés : proxy Web

Le cache en fonction des méthodes de requête :

- `GET` : La réponse est mise en cache par défaut (sauf configuration contraire via les entêtes)
- `POST` : La réponse n'est pas mise en cache par défaut (sauf configuration contraire via les entêtes)
- `PUT` et `DELETE` : Mise en cache interdit

Mécanisme de cache de HTTP 1.0 : Utilisation des entêtes `Date`, `Expires`, `Last-Modified` et `ETags`  
Mécanisme de cache de HTTP 1.1 : Utilisation de l'entête `Cache-Control`

Valeurs de `Cache-Control` :

- `private` : seuls les caches privés peuvent stocker une copie de la ressource. Utile pour des informations propres à un utilisateur. Cette directive permet la mise en cache de toute réponse qui ne l'est pas par défaut (réponse à POST par exemple)
- `public` : autorise le stockage par les caches publics et privés
- `no-cache` : Une demande doit systématiquement être envoyée pour stocker une copie de la ressource.
- `no-store` : Interdit la mise en cache
- `max-age=<secondes>` : durée de validité d'une ressource en seconde. Contrairement à `Expires` cela permet d'indiquer une date d'expiration qui est relative à la date de la réponse.
- `must-revalidate` : Le cache doit refaire une requête si les données sont expirées.

La durée de vie d'une ressource mise en cache est déterminée par (dans l'ordre) :

1. `Cache-control: max-age=N`
2. `Expires` (Durée de vie = valeur de `Expires` - valeur de `Date`)
3. `Last-Modified` (Durée de vie = valeur de `Last-Modified` - valeur de `Date`/10)