# Helmet

Ensemble de middleware  pour Express qui permet de sécuriser les entêtes HTTP

-  `Content-Security-Policy`  :  Voir [[Content security policy (CSP)]] 
- `Strict-Transport-Security` : HSTS. Permet de forcer la navigation via HTTPs 
-

Installation `npm install helmet` 

```JS
const helmet = require('helmet')
app.use(helmet())
```


Paramètres par défaut 

```
Content-Security-Policy: default-src 'self';base-uri 'self';font-src 'self' https: data:;form-action 'self';frame-ancestors 'self';img-src 'self' data:;object-src 'none';script-src 'self';script-src-attr 'none';style-src 'self' https: 'unsafe-inline';upgrade-insecure-requests

Cross-Origin-Embedder-Policy: require-corp
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Resource-Policy: same-origin

Origin-Agent-Cluster: ?1
Referrer-Policy: no-referrer
Strict-Transport-Security: max-age=15552000; includeSubDomains
X-Content-Type-Options: nosniff
X-DNS-Prefetch-Control: off
X-Download-Options: noopen
X-Frame-Options: SAMEORIGIN
X-Permitted-Cross-Domain-Policies: none
X-XSS-Protection: 0
```