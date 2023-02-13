# Types de relations

[Types de lien](https://developer.mozilla.org/fr/docs/Web/HTML/Types_de_lien)

Attribut `rel` des éléments `link`, `a`, `area` et `form`

- `stylesheet` : Élément `link`  
Lien vers une feuille de style. Combiné avec `alternate`, permet de définir une feuille de style alternative ( L’ attribut `title` doit être présent et non vide)
- `alternate` : Éléments `link`, `a` et `area`  
Lien vers une version alternative du document.
	- Flux de syndication : l’attribut `type` doit avoir pour valeur `application/rss+xml` ou `application/atom+xml`. Le premier flux définit est le flux par défaut
	- Pour un autre média : l’attribut `media` doit être défini
	- Dans un autre langue : l’attribut `hreflang` doit être défini
	- Dans un autre format : l’attribut `type` doit être défini
- `author` : Éléments `link`, `a` et `area`  
Lien vers une page décrivant l’auteur ou permettant de le contacter. Le lien peut être un lien mailto
- `canonical`: Élément `link`  
Lien vers l’URL canonique du document (URL officielle) dans le cas où celui ci est accessible via plusieurs URL (duplicate content). Il est recommandé d’utiliser une URL absolue.
- `help`: Éléments `link`, `a`, `area` et `form`  
Lien vers une page d’aide concernant le document
- `icon` : Élément `link`  
Indique une icône pour le document (favicon). Utiliser avec `type` et `sizes`. Remarque : Safari sur iOS ne prend pas en charge cette valeur et utilise à la place un le type de lien non standard `apple-touch-icon` )
- `license` : Éléments `link`, `a`, `area` et `form`  
Lien vers un document d’information relatif à la licence du contenu.
- `manifest` : Élément `link`  
Lien vers un manifeste d’application Web
- `next` et `prev` : Éléments `link`, `a`, `area` et `form`  
Indique les ressources suivante et précédente (Par exemple pour un contenu paginé)
- `pingback` : Élément `link`  
Lien vers une ressource externe qui doit être appelée si quelqu’un ajoute un commentaire ou une citation à propos de la page web courante. (Protocole défini dans la spécification Pingback 1.0)
- `prefetch` : Élément `link`  
Indique au navigateur que la ressource doit être pré-chargée et mise en cache. Ce pré-chargement est déclenché silencieusement à la fin du chargement de la page courante. À utiliser pour les ressources qui sont fortement susceptibles d’être demandées par le visiteur lors des prochaines étapes de navigation. (Par exemple : une suite de pages dans une présentation, des ressources ou des styles alternatifs qui s’affichent sur plusieurs pages principales du site). Doit être utilisé avec parcimonie pour ne pas saturer inutilement la bande passante du visiteur (Certains navigateurs peuvent imposer des limites).
- `preload` : Élément `link`  
Indique au navigateur que la ressource doit être pré-chargée au plus vite pour la navigation en cours. Utile lorsque on a besoin de cette ressource quelques secondes après le chargement de la page et qu'on souhaite l'accélérer.
- `search` : Éléments `link`, `a`, `area` et `form`  
Lien vers un document destinée à la recherche.(Par exemple un plugin [OpenSearch](https://fr.wikipedia.org/wiki/OpenSearch))
- `bookmark` : Éléments `a` et `area`  
Permalien de l’élément `article` ancêtre le plus proche. Sinon pour la section la plus proche.
- `external` : Éléments `a`, `area` et `form`  
Lien vers une ressource externe au site.
- `nofollow` : Éléments `a`, `area` et `form`  
Le lien pointe vers une ressource non approuvée. (Peut être utilisé par les moteurs de recherche pour exclure le document lié des classements selon la popularité)
- `noopener` : Éléments `a`, `area` et `form`  
Le lien est ouvert sans que le nouveau contexte de navigation créé ait accès au document source ( La propriété JS `Window.opener` renverra `null`). Cela permet de sécuriser les liens ouverts avec l’attribut `target="_blank"`
- `noreferrer` : Éléments `a`, `area` et `form`  
 Empêche le navigateur d’envoyer le `Referrer` dans les en-têtes HTTP (URL de la page précédente sur laquelle l’utilisateur a suivi un lien pour arriver sur la page courante)
- `tag` : Éléments `a` et `area`  
Lien vers une ressource qui décrit le tag appliqué au document (ne doit pas être utilisé pour renvoyer vers un nuage de tags)
