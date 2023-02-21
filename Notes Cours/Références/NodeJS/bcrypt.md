# bcrypt

Permet d'encoder des données 

Installation : `npm i bcrypt` 

```JS
const bcrypt = require('bcrypt');

const secret = 'secret'
const salt = 10, 

// hash et salage du mot de passe
bcrypt.hash(secret, salt).then(
  // traitements
)

// comparation 
bcrypt.compare('secret', 'secretCrypt').then(
   // traitements
)


