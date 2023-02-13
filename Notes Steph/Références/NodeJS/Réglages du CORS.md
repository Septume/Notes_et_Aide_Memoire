# Réglages du CORS

Voir [[Cross-origin resource sharing (cors)]]

```JS
const http = require('http');
const httpServer = http.createServer();

// origines acceptées
const allowOrigins = ['http://app.exemple.com', 'http://autre.exemple.com'];

httpServer.on('request', (request, response) => {
    // On test si l'entête "Origin" fait partie des origines acceptées
    if (request.headers['origin'] && allowOrigins.includes(request.headers['origin'])) {
      // Si oui alors on renseigne "Access-Control-Allow-Origin" avec l'origine de la requête
      response.setHeader('Access-Control-Allow-Origin'
      request.headers['origin']);
    } else {
        // Sinon on renseigne "Access-Control-Allow-Origin" à null créant une erreur CORS dans le navigateur
        response.setHeader('Access-Control-Allow-Origin', 'null');
    }

   // cas où le navigateur fait un pré-contrôle avec OPTIONS
    if (request.method === 'OPTIONS') {
        response.setHeader('Access-Control-Allow-Headers', 'Content-Type, Accept, Origin, Authorization');
        response.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, PATCH, OPTIONS');
        return response.end();
    }

    // suite du traitement ...
});

httpServer.listen(8080);
```

