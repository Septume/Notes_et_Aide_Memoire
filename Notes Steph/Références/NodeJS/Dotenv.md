# Dotenv

Module qui permet de configurer les variables d'environnement via un fichier `.env`. 

Installation : `npm install dotenv` 

On créé ensuite à la racine du projet un fichier avec pour nom `.env` 
On indique les variables sous la forme `KEY=value` (Par convention les noms sont écrit en majuscule)

Exemple 

```
# commentaire

DB_HOST=localhost
DB_USER=root
DB_PASS=azerty
```

Puis on indique tout en haut du fichier de démarrage de l'app 

```JS
require('dotenv').config();

// on peut spécifier un chemin différent 
require('dotenv').config({ path: '/custom/path/to/.env' })

```


On peut ensuite accéder aux variables  n'importe où dans l'application avec `process.env` 

```JS
const host = process.env.DB_HOST;
const user = process.env.DB_USER; 
const password = process.env.DB_PASS;
```

SI on utile Git, il faut exclure le fichier `.env` (qui peut contenir des données sensibles comme un mot de passe) via un fichier `.gitignore` 

Il est tout de fois recommandé de créer  un fichier `.env.sample` et de le commit pour garder une trace des variables utilisées

```
KEY= 
SQL_USER= 
SQL_PASSWORD=
```
