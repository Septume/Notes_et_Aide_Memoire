# Nommage dans Sequelize

Rappel : Sequelize est capable de gérer les pluriels irréguliers (par exemple : `Person` => `People` )

## Nommage des models et des tables

Les noms de model doivent être au singulier => crée une table avec le même nom mais au pluriel 

```JS
// créé une table 'users'
sequelize.define('user', { name: DataTypes.STRING });
```

 `freezeTableName: true` : option qui désactive la mise au pluriel du nom de la table générée 

## Nommage lors d'une requête Eager Loading 

Les données incluses sont ajoutés dans l'objet retourné. Sequelize créé automatiquement les noms de propriété selon les règles suivantes :
- lors d'une association `hasOne` ou `belongsTo` le nom de la propriété sera la version au singulier du nom model associé
- lors d'une association `hasMany` ou `belongsToMany` le nom de la propriété sera la a version au pluriel du nom model associé


```JS
// models
const User = sequelize.define('user', { name: DataTypes.STRING }, { timestamps: false });
const Task = sequelize.define('task', { name: DataTypes.STRING }, { timestamps: false });

// associations
User.hasMany(Task);
Task.belongsTo(User);

// requêtes 
const tasks = await Task.findAll({ include: User });  
console.log(JSON.stringify(tasks, null, 2));

const users = await User.findAll({ include: Task });  
console.log(JSON.stringify(users, null, 2));


```

Ce qui donne

```JSON

// Model Task
[{  
  "name": "A Task",  
  "id": 1,  
  "userId": 1,  
  "user": {  // correspond au model user (utilisation du singulier car relation BelongsTo)
    "name": "John Doe",  
    "id": 1  
  }  
}]

// model User
[{  
  "name": "John Doe",  
  "id": 1,  
  "tasks": [{  // correspond au model task (utilisation du pluriel car relation hasMany)
    "name": "A Task",  
    "id": 1,  
    "userId": 1  
  }]  
}]

```


## Option Underscored

Lors de la définition d'un model, cet option permet de générer côté base de données des noms avec le style `snake_case` plutôt que `camelCase` 


```JS
const User = sequelize.define('user', { username: Sequelize.STRING }, {
  underscored: true
});
const Task = sequelize.define('task', { title: Sequelize.STRING }, {
  underscored: true
});
User.hasMany(Task);
Task.belongsTo(User);

```

Dans cette exemple Sequelize va générer les noms suivants : 
- propriété `createAt` (sur tout les models)  => colonne `create_at` (sur toutes les tables)
- propriété `updateAt` (sur tout les models) => colonne `update_at`  (sur toutes les tables)
- propriété `userId` (model *task*) => colonne `user_id`  (table *tasks*) 

Dans tout les cas les noms sont toujours au format  `camelCase` côté JavaScript. Cette option modifie uniquement la façon dont les noms des champs sont mappés à la base de données 


