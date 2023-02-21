# **Sécurité des iframes**

## Header HTTP

`X-Frame-Options` : Entête HTTP qui permet de régler les autorisations concernant le chargement de la page dans un iframe

Les valeurs sont :

- `DENY` : interdiction
- `SAMEORIGIN` : autoriser depuis la même origine
- `ALLOW-FROM <URI>` : autoriser depuis L'URL indiqué
- `ALLOWALL` : autoriser depuis n'importe quelle origine

## Code HTML

Attribut `sandox`: Permet de placer l'iframe dans un bac à sable afin de limiter les interactions possibles. Utiliser cet attribut sans valeur permet d'appliquer toutes les restrictions. On peut également indiqué en valeur une liste de permissions séparées par des espaces

- `allow-forms` : Autorise l'envoie de formulaires
- `allow-scripts`: Autorise l'exécution de scripts
- `allow-same-origin` : Le contenu est considéré comme étant de la même origine que le contexte parent. Cela permet d' autoriser les requêtes AJAX, l'utilisation du localStorage, des cookies…
- `allow-modals` : Autorise l'ouverture des fenêtres modales.
- `allow-popups`: Autorise l'ouverture de fenêtres popup.
- `allow-orientation-lock` : Autorise la désactivation du verrouillage de l'orientation de l'écran.
- `allow-top-navigation`: Autorise l'accès à la page parente.  
`allow-pointer-lock`: Autorise l'utilisation de l'API Pointer Lock

Attention : il est fortement déconseillé pour des raisons de sécurité d'activer en même temps les permissions `allow-scripts` et `allow-same-origin`