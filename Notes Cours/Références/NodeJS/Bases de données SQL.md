# Bases de données SQL

3 manière de gérer une base de données SQL sous NodeJS 
- Effectuer des requêtes brutes (*Raw SQL*)
- Utiliser un constructeur de requête (*Query Builder*) 
- Utilise un ORM  = *Object-Relational Mapping* => mappage d'objet-relationnel

## Raw SQL 

Exemple 

```JS
const mysql = require('mysql2');
const connection = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "root",
    database: "test"
});

// Données provenant de la requête cliente
const email = 'bruno@example.com';
const password = 'foo';

connection.connect(function (err, handshakeResult) {
    if (err) throw err;
    // Requête SQL brute
    connection.query(`
        SELECT id FROM users WHERE email = '${email}' AND password = '${password}';
    `, function (err, rows) {
        if (err) throw err;
        // Résultat
        console.log(rows);
        // `[ { id: 2 } ]`
        connection.end();
    });
});
```

Avantages : 
- Pas besoin d'apprendre l'utilisation d'une librairie tiers (Il suffit juste d'apprendre à utiliser le connecteur) 
- On sait exactement ce que la requête fait 
Inconvénients : 
- Il faut gérer soi-même les vulnérabilités liées aux  injections SQL 
- On utilise des chaines de caractères JS pour effectuer des requêtes JS ce qui peut facilement entrainer des erreurs de syntaxe ou des coquilles dans les noms de table ou de colonne 
- Pas de support lors d'une mise à jour ou une migration de la base de données. 

## Query Builder

Utilisation d'une librairie pour construire les requêtes SQL. 

```JS
// exemple avec la librairie knex

const knex = require('knex')({
  client: 'mysql2',
  connection: {
    host : 'localhost',
    user : 'root',
    password : 'root',
    database : 'test'
  }
});

let query = knex.from('users').select('*').where({ role_id: 1})
```

Avantages : 
- Gère les vulnérabilités liées aux  injections SQL 
- Empêche les coquilles dans les commandes SQL
- Homogénéité du code 
Inconvénients : 
- N'évite pas les coquilles dans les noms de tableaux ou de colonnes
- Pas de support lors d'une mise à jour ou une migration de la base de données. 

## ORM

Voir [[Notes Cours/Références/NodeJS/Sequelize/- Intro]]

Ajoute une couche d'abstraction en mappant un enregistrement de la  base de données à un objet JavaScript . Cela permet d'opérer directement sur l'objet représentant l'enregistrement au lieu d'utiliser directement des requêtes SQL

Avantages : 
-  Homogénéité du code
-  Gère les vulnérabilités liées aux  injections SQL 
- Empêche les coquilles dans les commandes SQL ainsi que les noms de tables et colonnes
- Offre un support lors d'une mise à jour ou une migration de la base de données.
Inconvénients 
- On doit apprendre l'utilisation d'une librairie tiers 
- On ne sait pas exactement ce que fait la requête
- Peut entrainer des problèmes de performance 
- Pour des requêtes très complexe on est obligé de passer des requêtes brutes 


