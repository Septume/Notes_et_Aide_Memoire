# Same-origin policy

Politique de sécurité des navigateurs qui permet de restreinte l'accès à une ressource depuis une origine différente

## Définition de l'origine

Deux URLs ont la même origine s'ils utilisent le même protocole, le même hôte et le même port. Par exemple pour l'URL `http://docs.example.com`, les URLs suivants ne sont pas de la même origine :

- `https://docs.example.com` : car protocole différent
- `http://docs.example.com:8080` : car port différent
- `http://www.example.com` : car hôte différent

## Politique par défaut

En général :
- Les contenus embarqués (images, iframes, médias, plugins,etc) cross-origin sont autorisés. Par contre leur accès en lecture par un script est bloqué. (Pour les iframes, l'entête HTTP de réponse `X-Frame-Options` permet d'imposer d'autres restrictions)
- Les fichiers CSS cross-origin sont autorisés (À condition que l'entête http `Content-Type` correspond bien à un fichier de type `text/css`)
- Les scripts JS cross-origin sont autorisés. Par contre les requêtes HTTP depuis un script sont bloquées (`XMLHttpRequest`, `Fetch`)
- Les polices (embarqués avec `@font-face`) cross-origin sont autorisés ou non en fonction des navigateurs
- Pour les formulaires, Les URL cross-origin (indiqués avec l'attribut `action`) sont autorisés

Pour changer la politique, on peut utiliser le [[Cross-origin resource sharing (cors)]]
