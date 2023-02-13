# Sequelize

ORM (Object-Rlational Mapping) qui utilise les promesses  
Un ORM ajoute une couche d'abstraction en mappant un enregistrement dans une base de données à un objet JavaScript  
Cela permet d'opérer directement sur l'objet représentant l'enregistrement au lieu d'utiliser directement des requêtes SQL

installation : `npm install sequelize`

Il faut ensuite installer le driver correspondant au SGBD utilisé  

- MariaDB : `npm install mariadb`
- MySQL : `npm install mysql`
- PostgreSQL : `npm install pg`


## Avantages de Sequelize 

- Supporte MySQL/MariaDB, PostgreSQL, SQLite, Oracle et bien d'autre
- Prend en charge les requêtes brutes. avec `sequelize.query`
- Gère les transactions
- Protège contre les vulnérabilités d'injection SQL
- Validation des modèles
- Supporte TypeScript

## Créer une instance de Sequelize

```js

const { Sequelize } = require('sequelize');

//***

const sequelize = new Sequelize(
  'my-database', // nom de la bd
  'root', // id
  '', // mot de passe
  {
    host: 'localhost',
    dialect: 'mariadb', // le SGBD utilisé
    dialectOptions: {
       // options facutatives pour le SGBD
    },
    logging: false, // optionnel (désactive les logs)
  }
);

// tester la connexion à la bd
sequelize
  .authenticate()
  .then((res) => console.log('connexion base de données ok'))
  .catch((err) => console.log('Echec connexion à la base de données : ' + err));
```

Remarque : Par défaut Sequelize affiche dans la console chaque requête SQL exécutée. Pour désactiver utiliser l'option `logging : false`


-----------------

[[Models]]
[[Requêtes]]
[[Validateurs et contraintes]]
[[Associations]]
[[Eager Loading]]
[[Nommage dans Sequelize]]



