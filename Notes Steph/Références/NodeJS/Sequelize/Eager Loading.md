# Eager Loading

Permet de récupérer des données associés en effectuant des jointures 
On utilise pour cela l'option `include` qui permet d'indiquer le model associé. 
Par défaut Sequelize effectuera une requête avec une jointure externe de type `LEFT JOIN` 

## Fonctionnement

Exemple 

```JS

// on effectue une requête pour récuperer le capitaine et le bateau associé
const awesomeCaptain = await Captain.findOne({
  where: {
    name: "Jack Sparrow"
  },
  include: Ship // permet d'inclure les données du bateau dans la requête. 
});



console.log('Name:', awesomeCaptain.name);
console.log('Skill Level:', awesomeCaptain.skillLevel);
console.log('Ship Name:', awesomeCaptain.ship.name);
console.log('Amount of Sails:', awesomeCaptain.ship.amountOfSails);
```

Sequelize ajoute automatiquement les champs des tables associés dans l'objet retourné.

Exemple

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
  "user": {  // correspond au model User (utilisation du singulier car relation BelongsTo)
    "name": "John Doe",  
    "id": 1  
  }  
}]

// model User
[{  
  "name": "John Doe",  
  "id": 1,  
  "tasks": [{  // correspond au model Task (utilisation du pluriel car relation hasMany)
    "name": "A Task",  
    "id": 1,  
    "userId": 1  
  }]  
}]


```


## Récupérer plusieurs models associés 

Pour récupérer plusieurs model il faut passer à l'option `include` un tableau

```JS
Foo.findAll({  
  include: [  
    {  
      model: Bar,  
      required: true  
    },  
    {  
      model: Baz,  
      where: /* ... */  
    },  
    Qux // { model: Qux } 
  ]  
})
```

Pour inclure tout les models associés on utilise l'option `all: true`

```JS
User.findAll({ include: { all: true }});  
```


## Autres types de jointures

Par défaut la jointure effectuer est un `LEFT OUTER JOIN`  
Pour faire un `INNER JOIN` il faut indiquer l'option `required: true`

```JS
User.findAll({  
  include: {  
  model: Task,  
  required: true  
}  
})
```

Pour faire un `RIGHT OUTER JOIN` il faut indiquer l'option `right: true` (fonctionne que si `required` est à false)

```JS
User.findAll({
  include: [{
    model: Task,
    right: true 
  }]
});
```


## Model avec alias

Dans le cas d'une association qui utilise un alias il faut spécifier l'alias en plus du nom du model lors de l'inclusion.

```JS
User.hasMany(Tool, { as: 'Instruments' });
const users = await User.findAll({
  include: { model: Tool, as: 'Instruments' }
});
console.log(JSON.stringify(users, null, 2));
```

Ce qui donne

```JSON
[{
  "name": "John Doe",
  "id": 1,
  "Instruments": [{
    "name": "Scissor",
    "id": 1,
    "userId": 1
  }]
}]
```


## Relation Many-To-Many

Dans ce type de relation, Sequelize récupère également les données de la table de jonction

```JS
// models
const Foo = sequelize.define('foo', { name: DataTypes.TEXT });
const Bar = sequelize.define('bar', { name: DataTypes.TEXT });

// Association
Foo.belongsToMany(Bar, { through: 'fooBar' });
Bar.belongsToMany(Foo, { through: 'fooBar' });

// requêtes
const foo = await Foo.create({ name: 'foo' });
const bar = await Bar.create({ name: 'bar' });
await foo.addBar(bar);
const fetchedFoo = await Foo.findOne({ include: Bar });

console.log(JSON.stringify(fetchedFoo, null, 2));
```

Ce qui donne

```JSON
{
  "id": 1,
  "name": "foo",
  "bars": [ // model associé
    {
      "id": 1,
      "name": "bar",
      "fooBar": { // table jonction
        "fooId": 1,
        "barId": 1
      }
    }
  ]
}
```

Par défaut, tout les champs de la table de jonction sont récupérés.  
Pour inclure seulement certains champs on utilise l'option `attributes` qui prend comme valeur un tableau listant les champs à récupérer. Cette option doit se trouver à l'intérieur de l'option `through`  
Si on souhaite en récupérer aucun champ, il suffit de passer un tableau vide

```JS
const foo = Foo.findByPk(id, {
  include: [{
    model: Bar,
    // pour ne pas récuperer les champs de la tables de jonction
    through: { attributes: [] }
  }]
})

```

Pour inclure tout les models associés ainsi que toutes les tables de jointures on utilise les options `all` et `nested`

```JS
User.findAll({ include: { all: true, nested: true }});
```

## Utiliser un filtre au niveau du modèle associé 

On utilise l'option `where` dans le `include`. Dans ce cas Sequelize définie automatiquement l'option `required` sur `true` pour effectuer une requête `INNER JOIN` 
De plus la condition `where` sera convertie en condition pour la clause `ON` 

```JS
// récupère les utilisateurs qui possède l'outil 'small'
User.findAll({
  include: {
    model: Tool,
    where: { // filtre au niveau du model Tool
      size: {
        [Op.ne]: 'small'
      }
    }
  }
});

```

```SQL
SELECT
  users.id, 
  users.name, 
  tools.id,
  tools.name,
  tools.size,
  tools.userId
FROM users 
INNER JOIN tools 
ON user.id = tools.userId AND tools.size != 'small';
```

Pour se référer à une colonne du model parent on utilise la fonction `Sequelize.col` 

```JS
// Trouver tout les projets avec au moins une tache ou task.state === project.state
Project.findAll({
  include: {
    model: Task,
    where: {
      state: Sequelize.col('project.state')
    }
  }
})
```

Si on souhaite plutôt faire un `OUTER JOIN` avec une clause `WHERE` il faut utiliser les colonnes imbriqués avec une syntaxe sous la forme  `$nested.column$` (on peut utiliser plusieurs niveaux) 

```JS
User.findAll({
  where: {
    'tools.size$': { [Op.ne]: 'small' }
  },
  include: Tools
});
```

```SQL
SELECT
  users.id, 
  users.name, 
  tools.id,
  tools.name,
  tools.size,
  tools.userId
FROM users 
LEFT OUTER JOIN tools 
ON user.id = tools.userId 
WHERE tools.size != 'small';
```

## Utiliser le tri

```JS
Company.findAll({
  include: Division,
  order: [
    // Tri sur le model associé Division
    [Division, 'name', 'ASC']
  ]
});


// si l'include utilise un alias 

Company.findAll({  
  include: { model: Division, as: 'Div' },  
  order: [  
    // Tri sur le model Division
    [{ model: Division, as: 'Div' }, 'name', 'DESC']  
  ]  
});


// pour des include imbriqués 

Company.findAll({  
include: {  
  model: Division,  
  include: Department  
},  
order: [   
  // Tri sur le model associé Division 
  [Division, Department, 'name', 'DESC']  
]  
});


// Dans le cas d'une relation Many-To-Many 

Company.findAll({  
  include: {  // relation Many-To-Many entre Division et Department
    model: Division,  
    include: Department  
  },  
  order: [  
    // Tri sur le model Division
    [Division, DepartmentDivision, 'name', 'ASC']  
  ]  
});

```


## Utiliser findAndCountAll

```JS


// recherche et compte uniquement les utilisateurs qui ont un profil 
// créé un INNER JOIN
User.findAndCountAll({  
  include: [  
    { model: Profile, required: true }  
  ],  
  limit: 3  
});


// recherche et compte uniquement les utilisateurs qui ont un profil 
// La clause WHERE créé automatiquement required à true 
// créé un INNER JOIN

User.findAndCountAll({  
  include: [  
    { model: Profile, where: { active: true } }  
  ],  
  limit: 3  
});


// recherche et compte tout les utilisateurs (meme ceux qui n'ont pas de profil)
// créé Un OUTER JOIN
User.findAndCountAll({  
  include: Profil,  
  limit: 3  
});



```

`

