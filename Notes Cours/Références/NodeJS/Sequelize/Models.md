# Sequelize - Models

Classe qui représente une table de la base de données.  une instance de cette classe représente un enregistrement de la table. 


## Créer un model

### Définition d'un model 

On utilise la méthode `define()` de `Sequelize` pour déclarer un modèle. 3 arguments :
- nom du model qui doit être au singulier => une table sera créé à partir du model avec le même nom mais au pluriel. Remarque : Sequelize est capable de gérer les pluriels irréguliers (par exemple : `Person` => `People` )
- un objet de description du model. Pour chaque attributs on indique un objet de configuration
- un objet d'options (facultatif)
  
```js
const User = sequelize.define(
  'user', // nom du model (créé une table du même nom mais au pluriel)
  {
    id: {
      // identifiant unique
      type: DataTypes.INTEGER, // nombre entier
      primaryKey: true, // clé primaire
      autoIncrement: true, // autoincrémentation
    },
    name: {
      type: DataTypes.STRING, // chaine de caractère
      allowNull: false, // valeur obligatoire
    },
  },
  // options
  {
    //***
  }
);


```

Si pour une colonne on juste besoin de d'indiquer le type de données on peut utiliser une syntaxe raccourcie

```JS
sequelize.define('user', { name: DataTypes.STRING });

//** version raccourci de 

sequelize.define('user', {  
  name: {  
    type: DataTypes.STRING  
  }  
});
```

On peut indiquer une valeur par défaut avec `defaultValue` 

```JS
sequelize.define('user', {  
  name: {  
    type: DataTypes.STRING,  
    defaultValue: "John Doe"  
  }  
});


sequelize.define('foo', {  
  bar: {  
    type: DataTypes.DATETIME,  
    defaultValue: DataTypes.NOW // valeur spécial qui correspond à la date courante
  }  
});
```


Par défaut Sequelize créé automatiquement deux champs supplémentaire de type `DataTypes.DATE` 
 -  `createAt` : date de création de la nouvelle instance du model
 - `updateAt` : date de modification
Ces propriétés peuvent être surchargés 


### Types de données 

- `DataTypes.STRING` : VARCHAR(255)
- `DataTypes.STRING(1234)` : VARCHAR(1234)
- `DataTypes.TEXT` 
- `DataTypes.BOOLEAN` 
- `DataTypes.INTEGER`          
- `DataTypes.FLOAT`
- `DataTypes.REAL`    (seulement PostgreSQL)
- `DataTypes.DATE` 
- `DataTypes.DATEONLY` : date sans l'heure 
- etc... 



### Options du model

Il possible dans les options de surcharger les attributs `createAt` et `updateAt` 

```JS
sequelize.define(
  'user', 
  {
   //** 
  },
  // options
  {
    createdAt: 'created', // on renomme la propriété en 'created'
    updatedAt: false, // on desactive la propriété
  }
);
```

Autres options : 
- `timestamps: false` :  permet de désactiver  la création automatique de `createAt` et `updateAt`
  - `freezeTableName: true` : désactive la mise au pluriel du nom de la table générée 
  - `tableName: 'nom_table'` : pour préciser le nom de la table. 

On peut définir certaines options  de manière globale lors de l'instance de sequelize 

```JS
const sequelize = new Sequelize(
/**/
{
  define: { // desactiver la mise au pluriel pour toutes les tables
    freezeTableName: true
  }
});
```

### Créer des index 

On indique les index dans les options du model 

```JS
sequelize.define(
  'user', 
  {
   //** 
  },
  // options
  {
    // créé un index unique sur le champ 'email'
    indexes: [  
      { unique: true, fields: ['email'] },
    ]
  }
);
```

### Getters et setters personnalisés 

Il est possible d'utiliser des getters et setters personnalisés pour les attributs du model. Ces derniers seront appelé automatiquement lorsque la valeur du champ sera lue.

```js
module.exports = (sequelize, DataTypes) => {
  return sequelize.define(
    'pokemon',
    {
      id: {
        type: DataTypes.INTEGER,
        primaryKey: true,
        autoIncrement: true,
      },
      name: {
        type: DataTypes.STRING,
        allowNull: false,
      },
      hp: {
        type: DataTypes.INTEGER,
        allowNull: false,
      },
      cp: {
        type: DataTypes.INTEGER,
        allowNull: false,
      },
      picture: {
        type: DataTypes.STRING,
        allowNull: false,
      },
      types: {
        type: DataTypes.STRING,
        allowNull: false,
        get() {
          // convertir la chaine récupérée de la bd en tableau
          return this.getDataValue('types').split(',');
        },
        set(types) {
          // convertir le tableau en chaine de caractère avant de l'envoyer dans la bd
          this.setDataValue('types', types.join());
        },
      },
    },
  );
};
```


### Exporter un model sous forme de module 

Créé un dossier  *models* qui contiendra tout les fichiers de model (nommer le fichier du nom du model au singulier) 

La fonction à exporter utilise comme paramètres :
- `sequelize` (instance de *Sequelize*)
- `DataTypes` (objet qui permet de définir le type de donnée pour chaque propriétés du model)

```js
module.exports = (sequelize, DataTypes) => {
  return sequelize.define('user', {
  // attributs
});
};
```

Pour importer le module 

```JS
const UserModel = require('../models/pokemon');

// création du model User
const User = UserModel(sequelize, DataTypes); 

```

## Mettre à jour la base de données 

### Synchroniser les models avec la base de données

On utilise la méthode `sync` de `sequelize` pour mettre à jour la base de données (création des tables à partir des models qui ont été instanciés)  
Prend en argument un objet de configuration et retourne une promesse 
La méthode peut prendre en argument un objet (facultatif)  pour les options 
-  `force: true`  : si la table existe déjà, elle sera débord supprimée pour être recréée
- ` alter: true` : si la table existe déjà, les colonnes seront mis à jour
Sans option, rien ne se passe si la table existe déjà


```js
sequelize
  .sync({ force: true }) 
  .then((res) => console.log('synchronisation bd ok'))
  .catch((err) => console.log('Echec synchronisation bd : ' + err));
```

Il est possible de synchroniser uniquement un model 

```JS
const User = sequelize.define('user', {
  // attributs
});

//***
await User.sync()

```

### Supprimer des tables

Pour supprimer des tables associée à un model on utilise la méthode `drop()`  (retourne une promesse)

```JS

const User = sequelize.define('user', {
  // attributs
});

// supprimer la table User
await User.drop();

// supprimer toutes les tables 
await sequelize.drop()

```


## Instance d'un model 

### Créer une instance

Un model est une classe. Une instance de cette classe représente un enregistrement dans la table. 
Pour créer une instance on utilise la méthode Sequelize spécifique  `build()` 

```JS
const jane = User.build({ name: "Jane" });  
console.log(jane.toJSON()) // il est conseillé d'utiliser toJSON() pour afficher l'instance
console.log(jane.name); /
```

Cette méthode se contente de créer l'objet. Pour enregistrer les données dans la base de données on utilise ensuite la méthode `save()` qui retourne une promesse

```JS
await jane.save();
```

La méthode `create()` est un raccourci pour les deux précédentes méthodes (retourne une promesse)

```JS
const jane = await User.create({ name: "Jane" });  
console.log(jane.name); // "Jane"
```

### Mettre à jour un champ 

```JS
const jane = await User.create({ name: "Jane" });

// on change la valeur du champ
jane.name = "Ada";

// on fait appel save() pour sauvegarder le changement en base de donnée
await jane.save();
```

La méthode `set` permet de modifier plusieurs champ. Il faut ensuite utiliser `save()` pour sauvegarder les modifications en base de données

```JS
const jane = await User.create({ name: "Jane" }, { favoriteColor: "green" });

jane.set({
  name: "Ada",
  favoriteColor: "blue"
});

// mise à jour de la base de données
await jane.save();
```

On peut également utiliser `update` pour modifier des champs et enregistrer directement les modifications 

```JS
const jane = await User.create({ name: "Jane" }, { favoriteColor: "green" });

// on change la couleur
jane.favoriteColor = "blue"  

// on change le nom et on enregistre ce changement en base de donnée (attention : le changement de couleur précédent se sera pas enregistré) 
await jane.update({ name: "Ada" })  


// on enregistre toutes les modifications (changement de couleur) 
await jane.save()  
```

### Supprimer une instance 

On utilise ma méthode `destroy()` . Cela aura pour conséquence de supprimer l'enregistrement en base de données 

```JS
const jane = await User.create({ name: "Jane" });
console.log(jane.name); // "Jane"

// on supprime jane
await jane.destroy();
```

### Recharger une instance 

On utilise la méthode `reload()` qui va générer une requête `SELECT` pour obtenir les données à partir de la base de données

```JS
const jane = await User.create({ name: "Jane" });
console.log(jane.name); // "Jane"

// on change le nom mais on ne l'enregistre pas en base de données
jane.name = "Ada";

// On recharge l'instance dpuis la base de données
await jane.reload();
console.log(jane.name); // "Jane"
```


### Enregistrer seulement certains champs 

Pour enregistrer en base de données seulement certains champs il faut passer à la méthode `save()` un tableau contenant des noms de colonnes (Ceci est utilisé en interne par Sequelize lors d'une requête de mise à jour) 

```JS
const jane = await User.create({ name: "Jane" }, { favoriteColor: "green" });
console.log(jane.name); // "Jane"
console.log(jane.favoriteColor); // green


jane.name = "Ada";
jane.favoriteColor = "blue";
console.log(jane.name); // Ada
console.log(jane.favoriteColor); // blue

// on sauvegarde en base de données uniquement le champ 'name'
await jane.save({ fields: ['name'] });


// on récupère les infos en base de données
await jane.reload();
console.log(jane.name); // Ada
console.log(jane.favoriteColor); // green (le changement de couleur n'a pas été sauvegardé) 
```


### Incrémenter / décrémenter des valeurs 

 Les méthodes  `increment()` et  `decrement()` permet d'incrémenter/décrémenter les valeurs d'une instance sans rencontrer de problèmes de concurrence

```JS
const jane = await User.create({ name: "Jane", age: 100 });
await jane.increment('age'); // on incrémente de 1 le champ 'age'
await jane.increment('age', { by: 2 }); // on incrémente de 2
await jane.decrement('age'); // on décrémente de 1
```

Il est possible d'incrémenter/décrémenter plusieurs champs à la fois 

```JS
const jane = await User.create({ name: "Jane", age: 100, cash: 5000 });
await jane.increment({
  'age': 2, // on incrémente de 2
  'cash': 100 // on incrémente de 100
});

// autre syntaxe si les valeurs sont incrémentées de la même quantité
await jane.increment(['age', 'cash'], { by: 2 }); // on incrémente tout les champs de 2
```


