# Content Security Policy (CSP)

Politique de sécurité permettant d'indiquer au navigateur les contenus qu'il peut exécuter ou non.  
Permet de limiter les attaques Cross-Site-Scripting (XSS)  
Standardisé par le W3C

Pour activer CSP :
- Utiliser l'entête de réponse HTTP `Content-Security-Policy` contenant les directives CSP (séparées par des points-virgules)
- Ou utiliser une balise HTML `meta http-equiv` pour configurer la politique

```html
 <meta http-equiv="Content-Security-Policy" content="default-src 'self'">
```

Remarque : si le navigateur ne supporte pas CSP ces directives seront ignorées. Dans ce cas c'est la politique Same-origin Policy qui sera appliquée

**Attention : En activant CSP, les scripts et les styles inline (c'est à dire directement indiqués dans le code HTML) ne seront plus autorisés par défaut, ainsi que le code JS généré avec la fonction eval()**

## Liste des directives

### **Directives de récupération**

Permet d'indiquer les sources autorisées pour un type de ressource

- `script-src` : scripts
- `styles-src` : styles
- `img-src` : images
- `font-src` : polices définies via `@font-face`
- `media-src` : médias (éléments `audio` et `video`)
- `object-src` : plugins (éléments `object` et `embed`)
- `frame-src` : éléments iframes (Remarque : cette directive a été déprécié dans la version 2 du standard avant d'être rétablie dans la version 3)
- `worker-src` : Workers
- `child-src` : Web Workers et iframes (dépréciée dans la version 3)
- `connect-src` : s'applique pour les API `XMLHttpRequest`, `Fetch`, `WebSocket` ou `EventSource`.
- `prefetch-src` : ressources préchargées
- `default-src` : directive par défaut pour les ressources sans définition de directives spécifiques

Pour indiquer les sources (séparées par des espaces) on peut utiliser :

- Une URL. Il est possible d'utiliser le caractère `` comme joker (Exemple : `.example.com` => tout les sous-domaines de `example.com`)
- `http:` ou `https:` : Pour limiter les sources à un protocole
- `data:` Pour autoriser les data-URI
- `'self'` : Mot clé (entouré de guillemets simples) pour indiquer toutes sources de même origine (Même protocole, port et hôte)
- `'none'` : Mot clé pour indiquer aucune source
- `'unsafe-inline'` : Mot clé permettant d'autoriser les scripts et styles inline
- `'unsafe-eval'` : Mot clé permettant d'autoriser le JavaScript généré avec la fonction `eval()`
- `'unsafe-hashes'` : Mot clé permettant d'autoriser le JavaScript en ligne mais uniquement pour les gestionnaires d'évènements (attributs `onclick`, etc..)
- un hash : Permet d'autoriser des scripts et styles inline spécifiques via un contrôle d'intégrité. A indiquer sous la forme `'<algorithme>-<valeur>'` (Par exemple : `'sha256-d08VMHuG2SHhy9Tk5'`). Il est possible d'utiliser `sha256`, `sha384` ou `sha512` (Remarque : Cette directive est utile uniquement pour du code qui n'est pas destiné à être souvent modifié)
- un nonce : (nonce = identifiant unique ne pouvant être utilisé qu'une seule fois). Permet d'autoriser des scripts et styles inline spécifiques via son nonce (à indiquer dans l'attribut `nonce`). Le serveur doit générer aléatoirement un nouveau nonce à chaque requête (sous la forme d'une chaine base64 d'au moins 128 bits). A indiquer sous la forme `'nonce-<valeur>'` (Par exemple : `'nonce-12345666789'`)

Exemple :

```
 Content-Security-Policy: 
     default-src 'self' ; 
     img-src * data: ;
     frame-src 'none' ; 
     font-src 'self' https: ;
     styles-src 'self' 'unsafe-inline' https//example.com ;
     script-src 'self' 'nonce-EDNnf03nceIOfn39fn3e9h3sdfa'
     media-src 'self' *.example.net
```

Dans cet exemple les sources autorisées sont :

- pour les images : n'importe quelle URL + data-URI
- pour les iframes : aucune source (désactive les iframes)
- pour les polices : sources de même origine ou provenant d'une URL sécurisée
- pour les styles : sources de même origine ou provenant de `https//example.com`, ainsi ques les styles inline
- pour les scripts : sources de même origine + le script ayant pour nonce `EDNnf03nceIOfn39fn3e9h3sdfa` (`<script nonce="EDNnf03nceIOfn39fn3e9h3sdfa">/* code JS */</script>`)
- pour les médias : sources de même origine ou provenant des sous-domaines de `example.com`
- pour toutes autres ressources : sources de même origine

### **Autres directives**

- `base-uri` : sources autorisées pour l'élément `base`
- `form-action` : sources autorisées pour l’attribut `action` d’un formulaire
- `frame-ancestors` : Élément parents autorisés à embarquer une ressource dans un élément `iframe`, `object` ou `embed`
- `upgrade-insecure-requests` : indique à l’agent utilisateur de réécrire les URLs en changeant HTTP en HTTPS ( Utile pour les sites avec beaucoup d’ URLs qui ont besoin d’être réécrites).
- `block-all-mixed-content` : indique à l’agent utilisateur de bloquer les contenus mixtes (c'est à dire les contenus servis en HTTP sur une page HTTPS). Si cette directive est activée, la directive `upgrade-insecure-requests` n'est plus pertinente
- `sandbox` : similaire à l'attribut HTML `sandbox` pour les éléments `iframe`. Il faut utiliser les même valeurs (ex : `allow-forms`, `allow-modals`, etc..)
- `plugin-types` : Pour spécifier le type de contenu (type MIME) qui est autorisé à être embarqué via un un plugin (élément `embed` et `object`)
- `require-sri-for` : indique à l’agent utilisateur d'autoriser uniquement les scripts ou/et les styles utilisant le SRI (Subresource Integrity) via l'attribut HTML `integrity`. Il faut indiquer comme valeur `script` , `style` ou les deux.

Exemple :

```
 Content-Security-Policy : 
     base-uri 'self' ;
     form-action 'self' ; 
     frame-ancestors 'none' ;
     upgrade-insecure-requests ;
     sandbox allow-scripts ;
     plugin-types application/x-shockwave-flash
     require-sri-for script style
```

### **Test des directives**

L'entête `Content-Security-Policy-Report-Only` permet de tester des directives sans les appliquer réellement. Cela permet de reporter les violations de la politique mais sans procéder au blocage des ressources

La directive `report-uri` permet d'indiquer une URL à laquelle il faut envoyer les rapports.

Exemple :

```
Content-Security-Policy: default-src 'self'; report-uri http://example.com/csp-report.php
```

Le report est un objet JSON qui contient :

- `document-uri` : L'URI de la page concernée par la violation de la politique
- `referrer` : Le referrer de cette page
- `blocked-uri`: L'URI de la ressource qui a été bloquée. Si la ressource vient d'une autre origine que la page, indique seulement le protocole, le nom de domaine et le port.  
`violated-directive` : la directive concernée  
`original-policy` : L'ensemble des directives utilisées

Exemple :

```
{
  "csp-report": {
    "document-uri": "http://example.com/connexion.html",
    "referrer": "",
    "blocked-uri": "http://example.com/script.js",
    "violated-directive": "script-src 'none'",
    "original-policy": "default-src 'self'; script-src 'none'; report-uri http://example.com/csp-report.php"
  }
}
```