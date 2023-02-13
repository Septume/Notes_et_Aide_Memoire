# Sequelize - Requêtes

## Opérations CRUD

Pour effectuer ces opérations on utilise des méthodes de l'instance du model qui retournent une promesse

### Créer un enregistrement (INSERT)

Méthode `create()` qui prend en argument un objet qui contient les noms des colonnes et leur valeurs. La méthode peut prendre comme deuxième argument un objet pour les options

```JS
const user = await User.create({ firstName: "Jane", lastName: "Doe" });  
```

Il est également possible de restreindre les colonnes à renseigner (cela peut être utilise pour des données provenant d'un formulaire) 
On utilise l'option `fields` qui prend comme valeur un tableau contenant les colonnes concernées

```JS
const User = sequelize.define(
  'user',
  {
    id: {
      type: DataTypes.INTEGER,
      primaryKey: true,
      autoIncrement: true,
    },
    username : {
      type: DataTypes.STRING,
      allowNull: false,
    },
    isAdmin : {
      type: DataTypes.BOOLEAN,
      defaultValue: false,
      
    }
  }
);

// on enregistre que le champ username
const user = await User.create({  
username: 'jane',  
isAdmin: true  
}, { fields: ['username'] });  


console.log(user.username); // jane  
console.log(user.isAdmin); // false
```

**Exemple d'utilisation dans un API REST**

```js
 app.post('/api/users', (req, res) => {
    USer.create(req.body) // req.body contient les données envoyés
      .then(data => {
        const message = `L'utilisateur ${req.body.name} a bien été crée.`;
        res.json({ message, data});
      })
      .catch((error) => {
        const message = "L'uitilisateur n'a pas pu être créé";
        res.status(500).json({ message, data: error });
      });
  });
```



### Récupérer les enregistrements (SELECT)

####  Récupérer tout les enregistrements d'une table

Méthode `findAll()`

```JS
const users = await User.findAll();
```

Il est possible de spécifier les colonnes à récupérer 

```JS
User.findAll({  
  attributes: ['id', 'username']  
});
```

```SQL
-- Equivalent à 
SELECT id, username FROM Users
```

On peut également renommer les colonnes à l'aide d'un tableau imbriqué

```JS
User.findAll({  
attributes: ['id', ['username', 'name']]  
});
```

```SQL
-- Equivalent à 
SELECT id, username AS name FROM Users
```


**Exemple d'utilisation dans une API REST**

```js
  app.get('/api/users', (req, res) => {
    User.findAll()
      .then(data => {
        const message = 'La liste des utilisateurs a bien été récupérée.';
        res.json({ message, data});
      })
      .catch(error => {
        const message = 'Erreur dans la récupération de la liste des utilisateurs';
        res.status(500).json({
          message,
          data: error,
        });
      });
  });
```

**Exemple d'utilisation dans une API REST avec paramètre d'URL**

```js
 app.get('/api/users', (req, res) => {
   // dans le cas d'une /users?username=jane
    if (req.query.username) {
      const name = req.query.name;
      // utilisation de la clause where
      return User.findAll({ where: { username: username } }).then(data  => {
        const message = `Il y a ${data.length} utilisateurs qui correspond au terme de recherche ${username}`;
        res.json({ message, data });
      });
    } else {
      Pokemon.findAll()
        .then(data => {
          const message = 'La liste des utilisateurs a bien été récupérée.';
          res.json({ message, data });
        })
        .catch((error) => {
          const message =
            'Erreur dans la récupération de la liste des utilisateurs';
          res.status(500).json({
            message,
            data: error,
          });
        });
    }
  });
```


#### Récupérer un enregistrement en fonction de sa clé primaire

Méthode `findByPk()` . Prend en argument l'ID de la clé primaire. Si l'argument est une chaine de caractère celle ci sera automatiquement convertit en nombre

**Exemple d'utilisation dans une API REST**

```js
 app.get('/api/users/:id', (req, res) => {
    Pokemon.findByPk(req.params.id) // on récupère l'id dans l'URL
      .then(data => {
        if (data === null) {
          const message = "l'utilisateur demandé n'existe pas";
          return res.status(404).json({ message });
        }
        const message = 'Un utilisateur a bien été trouvé.';
        res.json({ message, data});
      })
      .catch((error) => {
        const message = "L'utilisateur n'a pas pu être récupéré";
        res.status(500).json({ message, data: error });
      });
  });
  ```


### Mettre à jour un enregistrement (UPDATE)


Un utilise la méthode `update()`

```JS
User.update({ username: 'Ada' }, {  
where: {  // option permettant de faire un filtre
  lastName: 'jaune 
}  
});
```

**Exemple d'utilisation dans une API REST**

```js
app.put('/api/users/:id', (req, res) => {
    const id = req.params.id;
    User.update( req.body, { where: { id: id },})
      .then((_) => {
      //  retour des données de l'utilisateur modifié
        return User.findByPk(id).then(data => {
          // dans le cas où l'id n'existe pas
          if (data === null) {
            const message = "l'utilisateur demandé n'existe pas";
            return res.status(404).json({ message });
          }
          const message = `L'utilisateur ${data.name} a bien été modifié.`;
          res.json({ message, data});
        });
      })
      .catch((error) => {
        const message = "L'utilisateur n'a pas pu être modifié";
        res.status(500).json({ message, data: error });
      });
  });
```

### Supprimer un enregistrement (DELETE)

On utilise la méthode `destroy()`

```JS
User.destroy({
  where: {
    username: "Jane"
  }
});
```

**Exemple d'utilisation dans une API REST**

```js
app.delete('/api/users/:id', (req, res) => {
  // recherche de l'utilisateur à supprimer
    User.findByPk(req.params.id).then(data => {
      // dans le cas où l'id n'existe pas
      if (data === null) {
        const message = "l'utilisateur demandé n'existe pas";
        return res.status(404).json({ message });
      }
      // Sinon suprression de l'utilisateur et retour des données
      return User.destroy({
        where: { id: data.id },
      })
        .then((_) => {
          const message = `L'utilisareur avec l'identifiant n°${data.id} a bien été supprimé.`;
          res.json({ message, data});
        })
        .catch((error) => {
          const message = "L'utilisateur n'a pas pu être supprimé";
          res.status(500).json({ message, data: error });
        });
    });

```


Remarque : Si on souhaite supprimer toutes les données d'une table on peut utiliser l'option `truncate`

```JS
User.destroy({  
  truncate: true  
});
```

```SQL
--- Equivalent de 
TRUNCATE TABLE Users
```

## Requêtes avancés

### Utiliser une fonction d'agrégation 
 

```JS
User.findAll({  
  attributes: [  
    'id', 'username', // colonnes
    // on compte le nombre d'users
    [sequelize.fn('COUNT', sequelize.col('id')), 'nbUsers'] // 'nbUsers' => alias (facultatif - permet d'acéder à la donnée depuis le modèle)
  ]  
});
```

```JS
// alternative pour sélectionner toutes les colonnes d'un coup

User.findAll({  
  attributes: {  
    include: [  
      [sequelize.fn('COUNT', sequelize.col('id')), 'nbUsers']
    ]  
  }  
});
```


```SQL
SELECT username, COUNT(id) AS nbUsers FROM Users
```

Remarque : on peut aussi utiliser `exclude` pour exclure des colonnes

### Filtrer la requête (clause WHERE)

On utilise l'option `where` qui s'utilise conjointement avec les opérateurs Sequelize pour indiquer la condition

Exemple 

```JS
const { Op } = require("sequelize");  // importation des opérateurs Sequelize

Post.findAll({  
  where: {  
    authorId: {  
    [Op.eq]: 2  // authorId = 2
    }  
  }  
});  

// remarque : dans le cas d'une égalité l'opérateur peut être omis (il sera implicite) 

Post.findAll({  
  where: {  
  authorId: 2  // authorId = 2
  }  
});
```

```SQL
-- Equivalent à 
SELECT * FROM post WHERE authorId = 2;
```

**Exemple d'utilisation dans une API REST**

```js
app.get('/api/users', (req, res) => {
    if (req.query.username) {
      const search = req.query.username;
      return User.findAll({
        where: {
          username: {
            // rechercher les noms qui contient le terme de la recherche
            [Op.like]: `%${search}%`,
          },
        },
      }).then(data => {
        const message = `Il y a ${data.length} utilisateurs qui correspond au terme de recherche : ${search}`;
        res.json({ message, data});
      });
    } else {
      User.findAll()
        .then(data => {
          const message = 'La liste des utilisateurs a bien été récupérée.';
          res.json({ message, data });
        })
        .catch(error => {
          const message =
            'Erreur dans la récupération de la liste des utilisateurs';
          res.status(500).json({
            message,
            data: error,
          });
        });
    }
  });
```

### Trier les résultats (clause ORDER BY)

On utilise l'option `order` qui prend comme valeur un tableau contenant les éléments de tri 
Les éléments de tri sous sous la forme ` [column, direction]` 


```JS
User.findAll({
  order: [
    // trier par nom ASC
    ['name', 'ASC'],
    // trier par max(age) DESC
    [sequelize.fn('max', sequelize.col('age')), 'DESC'],
  ],
});
```

Exemple 2 avec association ( Voir [[Associations]] et [[Eager Loading]])

```JS
Subtask.findAll({  
order: [  
  // trier par titre DESC
  ['title', 'DESC'], 
  // tri par la date createAt du model associé Task
  [Task, 'createdAt', 'DESC'], 
  // tri sur le createAt du model associé Task qui est associé au model Projet
  [Task, Project, 'createdAt', 'DESC'],  
});
```

### Limiter les résultats 

```JS
// limiter à 10 résultats
Project.findAll({ limit: 10 });

// sauter les 8 premiers résultats
Project.findAll({ offset: 8 });

// sauter les 5 premiers résultats et limiter au 5 résultats suivants
Project.findAll({ offset: 5, limit: 5 });
```

## Opérateurs Sequelize 

### Listes des opérateurs 

Liste non exhaustive 

```JS
// basiques
[Op.eq]: 3, // = 3  
[Op.ne]: 20, // != 20  
[Op.is]: null, // IS NULL  
[Op.not]: true, // IS NOT TRUE  
[Op.col]: 'user.id'
        
// comparaison
[Op.gt]: 6, // > 6  
[Op.gte]: 6, // >= 6  
[Op.lt]: 10, // < 10  
[Op.lte]: 10, // <= 10  
[Op.between]: [6, 10], // BETWEEN 6 AND 10  
[Op.notBetween]: [11, 15], // NOT BETWEEN 11 AND 15 

// autres opérateurs 
[Op.all]: sequelize.literal('SELECT 1'), // > ALL (SELECT 1)  
[Op.in]: [1, 2], // IN [1, 2]  
[Op.notIn]: [1, 2], // NOT IN [1, 2]  
[Op.like]: '%hat', // LIKE '%hat'  
[Op.notLike]: '%hat', // NOT LIKE '%hat'  
[Op.startsWith]: 'hat', // LIKE 'hat%'  
[Op.endsWith]: 'hat', // LIKE '%hat'  
[Op.substring]: 'hat', // LIKE '%hat%'  
```


Il existe une syntaxe abrégé pour `Op.in`

```JS
Post.findAll({  
  where: {  
  id: [1,2,3] // équivalent à `id: { [Op.in]: [1,2,3] }`  
  }  
});  
// SELECT ... FROM "posts" AS "post" WHERE "post"."id" IN (1, 2, 3);
```


### Combinaison logique

On utilise les opérateurs `Op.and`, `Op.or` et `Op.not`

Exemple 1

```JS
Post.findAll({  
  where: {  
    [Op.and]: [  
      { authorId: 12 },  
      { status: 'active' }  
    ]  
  }  
});


// alernative implicite 
Post.findAll({  
  where: {  
    authorId: 12,  
    status: 'active'  
  }  
});
```

```SQL
-- Equivalent à 
SELECT * FROM post WHERE authorId = 12 AND status = 'active';
```

Exemple 2 avec l'operateur OR

```JS
Post.findAll({  
  where: {  
    [Op.or]: [  
      { authorId: 12 },  
      { authorId: 13 }  
    ]  
  }  
});  

// alernative avec une syntaxe plus courte (si les deux conditions concerne la même colonne)
 
Post.findAll({  
  where: {  
    authorId: {  
      [Op.or]: [12, 13]  
    }  
  }  
});
```

```SQL
--- Equivalent à 
SELECT * FROM post WHERE authorId = 12 OR authorId = 13;
```

Exemple 3 

```JS
Foo.findAll({
  where: {
    rank: {  // rank < 1000 ou rank IS NULL
      [Op.or]: {
        [Op.lt]: 1000,
        [Op.eq]: null
      }
    }
});
```

## Autres méthodes de Sequelize 

### Méthodes utilitaires 

Méthode `count()` : compte le nombre d'occurence 

```JS
const amount = await Project.count({
  where: {
    id: {
      [Op.gt]: 25
    }
  }
});
console.log(`There are ${amount} projects with an id greater than 25`);
```

Méthodes : `max`, `min` et `sum` (somme)

```JS
await User.max('age'); 
await User.min('age'); 
```

Méthode `increment` et `decrement`

```JS
await User.increment({age: 1}) // incrémente l'age de 1
```

### Méthodes Finders

Méthodes qui génèrent des requêtes `SELECT`. Toutes ces méthodes retournent des instances de la classe du modèle. 
Il est possible de retourner uniquement des simples objets JS avec l'option `{ raw: true }` 

`findAll()` : pour faire un `SELECT` standard
`findByPk(PrimayKey)` : Recherche un enregistrement en fonction de sa clé primaire
`findOne()` : Retourne uniquement la première entrée trouvée (on peut utiliser des options de recherche comme le `where`) 
`findOrCreate()` :  Recherche un enregistrement qui correspond à la recherche ou le créé si il n'existe pas.  Renvoi soit l'instance trouvée, soit l'instance créée,
`findAndCountAll()` : permet de combiner `findAll()` et `count()` => utilise pour créer une pagination 



### Méthode bulkCreate() 

Permet de créer plusieurs enregistrement à la fois dans la même requête. Prend comme argument un tableau d'objets représentant les éléments à insérer

```JS
const captains = await Captain.bulkCreate([
  { name: 'Jack Sparrow' },
  { name: 'Davy Jones' }
]);
console.log(captains.length); // 2
console.log(captains[0].name); // 'Jack Sparrow'
console.log(captains[1].name); // 'Davy Jones'
```

Attention : par défaut la méthode n'exécute pas les éventuelles validateurs pour des questions de performance. On peut changer cela dans les options

```JS
const captains = await Captain.bulkCreate([
  { name: 'Jack Sparrow' },
  { name: 'Davy Jones' }
], { validate: true }); // activé la validation
```

La méthode accepte une option `fields` pour limiter les colonnes concernées

```JS
await User.bulkCreate([
  { username: 'foo' },
  { username: 'bar', admin: true }
], { fields: ['username'] }); // on accepte que le champ 'username'
```



## Requêtes brutes 



