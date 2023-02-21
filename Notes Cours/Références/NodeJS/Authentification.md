# Authentification

## Créer un JWT

Il faut d'abord installer le paquet `jsonwebtoken` 

Pour créer le jeton 

```JS
const jwt = require('jsonwebtoken');
const privateKey = 'CUSTOM_PRIVATE_KEY';

const token = jwt.sign(
  { userId: user.id },
  privateKey,
  { expiresIn: '24h' },
);
```

Exemple d'utilisation dans une API

```JS
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');

const privateKey = 'CUSTOM_PRIVATE_KEY';
const username = 'username'
const password = 'password'

app.post('/api/login', (req, res) => {
// on compare le mot de passe envoyé avec celui enregistré
 bcrypt.compare(req.body.password, password)
   .then((valid) => {
     if (!valid) {
     const message = 'Mot de passe incorrect';
       return res.status(401).json({ message });
      }
      // Création du jeton
      const token = jwt.sign(
        { userId: user.id },
        privateKey,
        { expiresIn: '24h' },
        );
        const message = 'succès de la connexion';
        return res.json({ message, token });
    });
})
```

On créé un module pour l'authentification qui sera appliquer comme middleware
La méthode `verify()` permet de vérifier la validité du token. 

```JS

const jwt = require('jsonwebtoken');
const privateKey = 'CUSTOM_PRIVATE_KEY';

module.exports = (req, res, next) => {
  // récupération du header authorization (chargé de transmettre le JWT)
  const authorizationHeader = req.headers.authorization;

  // on vérifie que le JWT a été fourni par le client
  if (!authorizationHeader) {
    const message = 'Vous n\'avez pas fourni de jeton d\'authentification. Ajoutez-en un dans l\'en-tête de la requête.';
    return res.status(401).json({ message });
  }

  /*
    le header a la forme => authorization: Bearer <JWT>
    Il faut utiliser la méthode split pour retirer le "Beader"
    pour ne garder que la chaine représentant le jeton
  */
  const token = authorizationHeader.split(' ')[1];

  // on vérifie le jeton
  jwt.verify(token, privateKey, (error, decodedToken) => {
    // en cas d'erreur
    if (error) {
      const message = 'L\'utilisateur n\'est pas autorisé à accèder à cette ressource.';
      return res.status(401).json({ message, data: error });
    }
    // on extrait l'id du token
    const { userId } = decodedToken;
    // on le compare avec celui envoyé par le client
    if (req.body.userId && req.body.userId !== userId) {
      // l'id est invalide. On envoie un message d'erreur
      const message = 'L\'identifiant de l\'utilisateur est invalide.';
      res.status(401).json({ message });
    } else {
      // l'id est valide. On continue
      next();
    }
  });
};
```

Autre exemple 

```JS
const jwt = require('jsonwebtoken');
const privateKey = 'CUSTOM_PRIVATE_KEY';
 
module.exports = (req, res, next) => {
   try {
     // on extrait le token du header
     /*
      le header a la forme => authorization: Bearer <JWT>
      Il faut utiliser la méthode split pour retirer le "Beader"
      pour ne garder que la chaine représentant le jeton
    */
     const token = req.headers.authorization.split(' ')[1];
     // on vérifie le token
     const decodedToken = jwt.verify(token, privateKey);
     // on extrait l'id du token
     const userId = decodedToken.userId;
     // on l'ajoute à l'objet Request pour que les routes puissent l'exploiter
     req.auth = {
         userId: userId
     };
     // on continue
     next();
   } catch(error) {
       res.status(401).json({ error });
   }
};
```


Il faut penser à ajouter le middleware d'authentification aux routes concernés 

```JS
app.get('/api', auth, (req, res) => {
    // traitement
  });
```
