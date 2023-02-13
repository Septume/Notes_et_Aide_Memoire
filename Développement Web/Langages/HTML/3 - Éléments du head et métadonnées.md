# Éléments du head et métadonnées

### Titre du document

`<title>`: **Obligatoire.** important pour l’accessibilité et le référencement.

### Style

`<style>` : Code CSS

- `media` : Requête media (Par défaut : `all`)
- `nonce` : Pour indiquer un nonce cryptographique dans le cadre de la CSP (Content Security Policy)
- `type` : Type MIME. Par défaut `text/css`

### Ressources liées

`<link />`: Lien vers une ressource externe

- `href` : URL de la source (absolue ou relative)
- `hreflang` : Code langue de la cible
- `rel` : Relation avec la cible
	- `stylesheet`
	- `alternate`
	- `author`
	- `canonical`
	- `help`
	- `icon`
	- `license`
	- `manifest`
	- `next` et `prev`
	- `pingback`
	- `prefetch`
	- `preload`
	- `search`
- `media` : Requête média dans le cas d’une relation `rel="stylesheet"`
- `title` : Dans le cas d’une relation `rel="stylesheet"` cet attribut général permet de définir une feuille de style alternative.
- `disabled` : Attribut booléen. À utiliser uniquement dans le cas d’une relation `rel="stylesheet"`. Permet de désactiver la feuille de style lors du chargement de la page. L’activation pourra être effectuée via un script.
- `sizes`: Dans le cas d’une relation icône `rel="icon"` pour indiquer les dimension de l’image en pixel. (A noter que Safari sur iOS ne prend pas en charge cet attribut car il utilise des types de lien non-standards pour définir une icône). Les valeurs possibles sont :
	- une liste de tailles, séparées par des espaces. La tailles est sous la forme `Largeur x Hauteur` (ex : `16x16`). Pour chaque tailles indiqués, une image correspondante doit exister
	- `any` : indique que l’image convient à plusieurs dimensions (image vectoriel.)
- `type`: Type MiME de la cible
- `as` : À utiliser uniquement pour les relations de type de `preload` et `prefetch`. Permet de préciser le type du contenu qui sera pré-chargé, ce qui permet au navigateur de déterminer sa priorité. Les valeurs possibles sont :
	- `image`
	- `audio`
	- `video`
	- `script`
	- `style`
	- `font`
	- `document` : document HTML destiné à être intégré dans un élément `iframe`
	- `embed` : ressource destinée à être intégrée dans un élément `embed`
	- `object` : ressource destinée à être intégrée dans un élément `object`
	- `track` : fichier WebVTT
	- `fetch` : ressource destinée à être récupérer via une requête AJAX
	- `worker`
- `integrity`: Subresource Integrity (SRI). Il s’agit d’un mécanisme qui permet au navigateur de contrôler l’intégrité d’une ressource externe via son empreinte cryptographique (Utilisée surtout pour les ressources récupérées depuis un CDN). Si le contrôle échoue, la ressource ne sera par chargée. La valeur est une chaine composée d’un préfixe indiquant l’algorithme utilisé ( `sha256`, `sha384` ou `sha512` ) , suivi d’un tiret puis le hash encodé en base64 (ex : `integrity="sha384-yC7kyQdHbdC5s22r6nKzQXwcHKCLKBeg/XRG6mPMTyAUyT8f3htNhtQdFQnhBld5"` )
- `crossorigin` : Indique si le CORS (Cross-Origin Ressource Sharing) doit être utilisé lors de la récupération de la ressource liée (Si l’attribut n’est pas présent le CORS n’est pas utilisé)
	- `"anonymous"`: autorise les requêtes cross-origin mai sans permettre l’authentification ou les cookies
	- `"use-credentials"`: permet également l’authentification et les cookies
- `referrerpolicy` : Permet de spécifier la politique concernant le referrer lors de la récupération de la ressource

```html
<!-- Icône associée au document -->
<link rel="icon" href="icone.gif" type="image/gif" sizes="32x32" />
<link rel="icon" href=icone.svg sizes="any" type="image/svg+xml" />
<!-- Icône pour iOS -->
<link rel="apple-touch-icon" href="icon.png" />

<!-- Feuilles de style pour diférent médias-->
<link rel="stylesheet" type="text/css" href="css/styles.css" media="screen" />
<link rel="stylesheet" type="text/css" href="css/print.css" media="print" />

<!-- Feuilles de styles par défaut et alternatives -->
<link href="default.css" rel="stylesheet" type="text/css" title="Style par défaut" />
<link href="joli.css" rel="alternate stylesheet" type="text/css" title="Joli" />
<link href="basique.css" rel="alternate stylesheet" type="text/css" title="Basique" />

<!-- Flux de syndication -->
<link rel="alternate" type="application/rss+xml" href="flux.rss" title="Actualités" />

<!-- autres langues -->
<link rel="alternate" hreflang="fr" href="http://fr.example.com/" />
<link rel="alternate" hreflang="en" href="http://en.example.com/" />
<link rel="alternate" hreflang="es" href="http://es.example.com/" />

<!-- Licence -->
<link rel="license" href="http://creativecommons.org/licenses/by-nc/2.0/fr/" />
```

`<base />` : Base d’adresse par défaut pour tout les liens du document. Un seul élément par page. La propriété JS `document.baseURI` permet d’accéder à l’URL de base

- `href` : URL de référence pour tous les URL relatives indiquées dans le document (liens, images, fichiers…)
- `target`: Contexte de navigation par défaut pour l’ouverture de tous les liens de la page

```html
<base href="http://www.exemple.com/files/" />
<!-- afficher une image dont le chemin est exemple.com/files/images/logo.png -->
<img src="images/logo.png" />
```

### Métadonnées

`<meta />`

- `charset` : Encodage de la page. Utiliser : UTF-8. À indiquer en premier
- `content` : À utiliser en combinaison de `http-equiv` et `name` pour indiquer les valeurs associées
- `http-equiv` : Informations à transmettre au navigateur ( Équivalent des entêtes HTTP) À associer à une valeur contenue dans l’attribut `content`
	- `refresh` : Rafraîchissement de la page. L’attribut `content` doit contenir un entier positif indiquant l’intervalle de rafraîchissement en seconde + éventuellement une URL de redirection. Syntaxe: `entier_positif;url=URL`
	- `Content-Security-Policy` : Permet de définir des règles CSP
	- `content-type` : (Obsolète) Pour indiquer le type MINE du document.
	- `content-langage` : ( Obsolète) Pour indiquer la langue de la page.
- `name`: Métadonnées relatives à la page. À associer à une valeur contenue dans l’attribut `content.` Quelques valeurs possibles :
	- `application-name` (pour les applications Web)
	- `author`
	- `description`
	- `keywords`
	- `viewport` : Permet de définir la taille du viewport pour les terminaux mobile.
	- `referrer` Permet de définir une politique pour le referrer (Utiliser les mêmes valeurs que `referrerpolicy`)

```html
<!-- encodage -->
<meta charset="utf-8" />

<!-- viewport  -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no"  />

<!--meta-données relatifs à la page -->
<meta name="author" content="Moi-même">
<meta name="description" content="mon super site">
<meta name="keywords" content="html5, css, developpement, web" />

<!-- Rafraîchissement de la page toutes les minutes -->
<meta http-equiv="refresh" content="60" />

<!-- Redirection vers une autre URL au bout de 5 secondes -->
<meta http-equiv="refresh" content="5;url=http://www.unsite.fr" />

<!-- Referrer Policy -->
<meta name="referer" content="no-referrer" />
```
