# Scripts

`<script>` : Permet d’intégrer le code d’un langage de script (à indiquer entre la balise ouvrante et fermante) ou pour lier un fichier contenant le code (via l’attribut `src`)

- `type`: Type MIME du script. Par défaut JavaScript.
- `src` : URL d’un script externe. (Les balises ne doivent pas contenir du code)
- `defer`: Attribut booléen. Indique que le script doit être exécuté seulement à la fin de l’analyse HTML. (Si il y a plusieurs scripts, ils seront exécutés dans l’ordre d’apparition dans le code). Cela permet de placer le script dans l’élément `head` sans bloquer l’analyse HTML. Attention, cet attribut n’a pas d’effet pour les scripts inline ou si l’attribut `async` est utilisé
- `async` : Attribut booléen. Indique que le script peut être exécuté de manière asynchrone. L’analyseur HTML n’est pas mis en pause et le script sera exécuté dès qu’il sera prêt (quelque soit l’ordre d’apparition dans le code). A utiliser si le fonctionnement de la page n’est pas dépendante du script. (Pas d’interaction avec le DOM, le CSSOM et les autres scripts). Attention, cet attribut n’a pas d’effet pour les scripts inline
- `nomodule` : Attribut booléen. Indique que le script doit être exécuté si le navigateur ne prend pas en charge les modules ES6
- `crossorigin` : Indique si le CORS (Cross-Origin Ressource Sharing) doit être utilisé lors de la récupération de la ressource liée (Si l’attribut n’est pas présent le CORS n’est pas utilisé)
	- `"anonymous"`: autorise les requêtes cross-origin mai sans permettre l’authentification ou les cookies
	- `"use-credentials"`: permet également l’authentification et les cookies
- `integrity`: Subresource Integrity (SRI). Il s’agit d’un mécanisme qui permet au navigateur de contrôler l’intégrité d’une ressource externe via son empreinte cryptographique (Utilisée surtout pour les ressources récupérées depuis un CDN). Si le contrôle échoue, la ressource ne sera par chargée. La valeur est une chaine composée d’un préfixe indiquant l’algorithme utilisé ( `sha256`, `sha384` ou `sha512` ) , suivi d’un tiret puis le hash encodé en base64 (ex : `integrity="sha384-yC7kyQdHbdC5s22r6nKzQXwcHKCLKBeg/XRG6mPMTyAUyT8f3htNhtQdFQnhBld5"` )
- `nonce` : Pour indiquer un nonce cryptographique dans le cadre de la CSP (Content Security Policy)
- `referrerpolicy`

`<noscript>` : Permet d’indiquer du code HTML qui sera exécuté si le navigateur ne prend pas en charge les fonctionnalités de script.

`<canvas>` : Permet d’intégrer une zone graphique modifiable via un script.

- `height` : hauteur de la zone en pixel. Par défaut 150px
- `width` : largeur de la zone en pixel. Par défaut 300px
