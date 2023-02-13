# Sequelize - Associations

4 types d'associations Sequelize

- `HasOne`
- `BelongsTo
- `HasMany`
- `BelongsToMany`

Ces 4 types peuvent être combinés par paire pour définir les 3 types types d'associations standard : `One-To-One`, `One-To-Many` et `Many-To-Many`

```JS
const A = sequelize.define('A', /* ... */);
const B = sequelize.define('B', /* ... */);

A.hasOne(B, { /* options */ });  
A.belongsTo(B, { /* options */ });  
A.hasMany(B, { /* options */ });  
A.belongsToMany(B, { through: 'C', /* options */ }); // C designe la table de jonction dans une relation Many-To-Many
````

Attention : L'ordre dans lequel l'association est définie est important.  
Dans l'exemple `A` est appelé le modèle source et `B` le modèle cible (seul le modèle source a "connaissance" de l'association)

- `A.hasOne(B)` : Relation `One-To-One` . La clé étrangère est définie dans le modèle cible B
- `A.belongsTo(B)` : Relation `One-To-One` . La clé étrangère est définie dans le modèle source A
- `A.hasMany(B)` : Relation `One-To-Many`. La clé étrangère est définie dans le modèle cible B

Dans ces 3 associations, Sequelize ajoute automatiquement les clés étrangères aux modèles appropriés (à moins qu'elles ne soient déjà présentes)

- `A.belongsToMany(B, { through: 'C' })` : Relation `Many-To-Many` . La table C sera utilisée comme table de jonction. Sequelize créé automatiquement le modèle (sauf s'il existe déjà) et y défini les clés étrangères appropriées

Ces types de relations sont utilisés par paire pour créer les relations standards:

- `One-To-One` : on utilise les associations `hasOne` et `belongsTo`
- `One-To-Many` : on utilise les associations  `hasMany` et `belongsTo`
- `Many-to-Many` : on utilise deux associations  `belongsToMany`

Remarque : on définie des paires afin de permettre à chaque modèle d'avoir "connaissance" de l'association avec l'autre.

## Types d'association

### One-To-One

Exemple

```JS
Foo.hasOne(Bar);
Bar.belongsTo(Foo);
```

```SQL
-- Equivalent à 
CREATE TABLE IF NOT EXISTS "foos" (/* ... */);
CREATE TABLE IF NOT EXISTS "bars" (
  /* ... */ 
  "fooId" INTEGER REFERENCES "foos" ("id") ON DELETE SET NULL ON UPDATE CASCADE
  /* ... */
);
```

Cela créé deux table `Foo` et `Bar`. Sequelize créé automatiquement la clé étrangère dans `Bar`  
celle-ci aura pour nom `fooId`


Les valeurs par défaut pour les associations One-To-One sont 
- pour `ON DELETE` : `SET NULL`
- pour `ON UPDATE` : `CASCADE`

Il est possible d'utiliser des options pour changer ces valeurs

```JS
Foo.hasOne(Bar, {
  onDelete: 'RESTRICT',
  onUpdate: 'RESTRICT'
});
Bar.belongsTo(Foo);
```

Les choix possibles sont `RESTRICT`, `CASCADE`, `NO ACTION`, `SET DEFAULT` et `SET NULL`

Il est possible d'indiquer un nom personnalisé pour la clé étrangère avec l'option `foreignKey`

```JS
// Option 1
Foo.hasOne(Bar, {
  foreignKey: 'myFooId' // nom à utiliser à la place de 'fooId'
});
Bar.belongsTo(Foo);

// Option 2 
Foo.hasOne(Bar, {  
  foreignKey: {  
    name: 'myFooId'  
  }  
});  
Bar.belongsTo(Foo);  
  
// Option 3  
Foo.hasOne(Bar);  
Bar.belongsTo(Foo, {  
  foreignKey: 'myFooId'  
});  
  
// Option 4  
Foo.hasOne(Bar);  
Bar.belongsTo(Foo, {  
  foreignKey: {  
    name: 'myFooId'  
  }  
});
```

Il est possible de préciser un type pour la clé étrangère

```JS
Foo.hasOne(Bar, {
  foreignKey: {
    name: 'myFooId'
    type: DataTypes.UUID // utilisation d'un UUID au lieu d'un integer
  }
});
Bar.belongsTo(Foo);
````

Par défaut l'association est considéré comme facultative, ce qui signifie que la clé étrangère peut avoir la valeur `NULL` .  
Pour changer ce comportement on utilise `allowNull: false`

```JS
Foo.hasOne(Bar, {
  foreignKey: {
    allowNull: false
  }
});
```

Remarque : Dans une relation `One-To-One` il faut choisir la table dans laquelle se trouvera la clé étrangère de l'autre table. Ce choix peut dépendre si la relation la relation est obligatoire ou facultative

### One-To-Many

Dans ce type de relation la clé étrangère doit se trouver du côté du *many*

Exemple :

```JS
Team.hasMany(Player);
Player.belongsTo(Team);
```

```SQL
-- Equivalent à 

CREATE TABLE IF NOT EXISTS "foos" (/* ... */);
CREATE TABLE IF NOT EXISTS "bars" (
  /* ... */ 
  "fooId" INTEGER REFERENCES "foos" ("id") ON DELETE SET NULL ON UPDATE CASCADE
  /* ... */
);

CREATE TABLE IF NOT EXISTS "Teams" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "Players" (
  /* ... */
  "TeamId" INTEGER REFERENCES "Teams" ("id") ON DELETE SET NULL ON UPDATE CASCADE,
  /* ... */
);
```

Les valeurs par défaut pour les associations One-To-Many sont 

- pour `ON DELETE` : `SET NULL`
- pour `ON UPDATE` : `CASCADE`

On peut utiliser les même options que pour la relations `One-To-One`

Exemple :

```JS
Team.hasMany(Player, {  
  foreignKey: 'clubId'  
});  
Player.belongsTo(Team);
```

### Many-To-Many

Ce type de relation utilise obligatoirement une 3ème table, dite table de jonction qui contient les clés étrangères des deux autres tables
L'option `through` est obligatoire et permet d'indiquer la table de jonction. Le modèle sera automatiquement créé par Sequelize (sauf s'il existe déjà) ainsi que les clés étrangères 


```JS
// créé la table de jonction ActorMovies
// avec les clés étrangères MovieId et ActorId
Movie.belongsToMany(Actor, { through: 'ActorMovies' });
Actor.belongsToMany(Movie, { through: 'ActorMovies' });
```


```SQL
-- Equivalent à 
CREATE TABLE IF NOT EXISTS "ActorMovies" (  
  "MovieId" INTEGER NOT NULL REFERENCES "Movies" ("id") ON DELETE CASCADE ON UPDATE CASCADE,  
  "ActorId" INTEGER NOT NULL REFERENCES "Actors" ("id") ON DELETE CASCADE ON UPDATE CASCADE,  
  "createdAt" TIMESTAMP WITH TIME ZONE NOT NULL,  
  "updatedAt" TIMESTAMP WITH TIME ZONE NOT NULL,  
  UNIQUE ("MovieId", "ActorId"), 
  PRIMARY KEY ("MovieId","ActorId")
);
````

Les valeurs par défaut pour les associations One-To-Many sont 
- pour `ON DELETE` : `CASCADE`
- pour `ON UPDATE` : `CASCADE`

Un clé unique composite est automatiquement créé sur les deux colonnes contenant les clés étrangères. Il est possible de personnalisé le nom de cette clé unique avec l'option `uniqueKey` 

```JS
Project.belongsToMany(User, { through: 'UserProjects', uniqueKey: 'my_custom_unique' })
```

Pour empêcher la création de cette clé unique il faut utiliser l' option `unique: false`

```JS
Project.belongsToMany(User, { through: 'UserProjects', unique: false})
```

L'option `timestamps: false` permet d'empêcher la création des attributs `ceateAt` et `udpdateAt`

```JS
Project.belongsToMany(User, { through: 'UserProjects', timestamps: false})
```

Il  est possible de définir manuellement le model de la table de jonction.  Les clés étrangères seront automatiquement créé lors de l'association

```JS
const userProfile = sequelize.define('UserProfile', {}, { timestamps: false });

// l'association ajoute les clés étrangères userId et profileId sur la table de jonction UserProfile
User.belongsToMany(Profile, { through: userProfile });
Profile.belongsToMany(User, { through: userProfile });
```

L'intérêt est de pouvoir ajouter d'autres colonnes sur la table de jonction

## Méthodes spéciales

L'instance d'un modèle utilisé lors d'une association dispose de méthodes spéciales permettant d'interagir avec le modèle associé

Les méthodes disponibles dépend du type d'association. Leur nom est composé d'un préfixe (ex :  `get`, `add`, `set`) et du nom du modèle associé (avec la première lettre en majuscule).  
Le nom peut être au pluriel. Dans ce cas les pluriels irréguliers sont gérés par Sequelize (`Person`=> `People`)

Toutes ces méthodes retournent une promesse

### hasOne ou BelongsTo`

Pour une association : `Foo.hasOne(Bar)` ou `Foo.belongsTo(Bar)`

Les méthodes disponibles pour l'instance de `Foo` sont :

- `getBar()` : pour obtenir l'instance associé
- `setBar()` : pour définir l'instance associé
- `createBar()` : pour créer une nouvelle instance associé (retourne l'instance)

```JS
const foo = await Foo.create({ name: 'the-foo' });
const bar1 = await Bar.create({ name: 'some-bar' });
const bar2 = await Bar.create({ name: 'another-bar' });


// on récupère l'instance associé
console.log(await foo.getBar()); // null

// on défini l'instance associé
await foo.setBar(bar1);
console.log((await foo.getBar()).name); // 'some-bar'

// on créé une nouvelle instance associée
await foo.createBar({ name: 'yet-another-bar' });
const newlyAssociatedBar = await foo.getBar();
console.log(newlyAssociatedBar.name); // 'yet-another-bar'

await foo.setBar(null); // on supprime les associations
console.log(await foo.getBar()); // null
```

### hasMany

Pour une association : `Foo.hasMany(Bar)` ou `BelongsToMany`

Les méthodes disponibles pour l'instance de `Foo` sont :

- `getBars()` : Obtenir tout ce qui est associé en utilisant une clause `WHERE` facultative (retourne un tableau). Pour une relation `BelongsToMany` retourne par défaut les champs de la table de jonction.
- `countBars()` : Compter tout ce qui est associé en en utilisant une clause `WHERE` facultative (retourne un nombre)
- `hasBar()`: Vérifie si l'instance est associée (retourne un booléen)
- `hasBars()` : Vérifier l'association de plusieurs instance
- `setBars()` : Définir les modèles associés en transmettant un tableau d'instances ou leurs clés primaires
- `addBar()` : Associer une instance
- `addBars()` : Associer plusieurs instance (prend en argument un tableau)
- `removeBar()` : Désassocier une instance
- `removeBars()` : Désassocier plusieurs instances
- `createBar()`: pour créer une nouvelle instance associé

```JS
const foo = await Foo.create({ name: 'the-foo' });
const bar1 = await Bar.create({ name: 'some-bar' });
const bar2 = await Bar.create({ name: 'another-bar' });

// retourne dans un tableau tout ce qui est associé 
console.log(await foo.getBars()); // []

// compte le nombre d'association
console.log(await foo.countBars()); // 0

// vérifie si l'instance est associée
console.log(await foo.hasBar(bar1)); // false

// ajoute un tableau d'instance
await foo.addBars([bar1, bar2]);

// compte le nombre d'association
console.log(await foo.countBars()); // 2

// vérifie l'existence d'une association
console.log(await foo.hasBar(bar1)); // true

// supprime une association
await foo.removeBar(bar2);
console.log(await foo.countBars()); // 1

await foo.createBar({ name: 'yet-another-bar' });
console.log(await foo.countBars()); // 2

await foo.setBars([]); // supprime toutes les associations
console.log(await foo.countBars()); // 0
```

Remarque : La méthode getter accepte les options comme les méthodes de recherche habituelles (telles que `findAll`)

```JS
const easyTasks = await project.getTasks({
  where: {
    difficulty: {
      [Op.lte]: 5
    }
  }
});
```

Pour les relations `BelongsToMany` la méthode getter retourne par défaut tout les champs de la table de jonction  
Pour choisir les champs de la table de jonction à inclure il faut utiliser l'option `joinTableAttributes` qui prend comme valeur un tableau contenant les champs

```JS
const foo = Foo.findByPk(id)
// pour ne pas récuperer les champs de la tables de jonction
console.log(foo.getBars({ joinTableAttributes: [] }))
```

## Alias  

Il est possible de définir un alias pour une association  
Ce dernier sera utilisé à la place du nom du modèle pour les former les noms des méthodes spéciales

```JS

// Utilisation de l'alias 'leader'. cela créé une clé étrangère avec pour nom 'leaderId' 
Ship.belongsTo(Captain, { as: 'leader' }); 

// Génère une erreur
console.log((await Ship.findAll({ include: Captain })).toJSON());

// il faut utiliser l'alias à la place
console.log((await Ship.findAll({ include: 'leader' })).toJSON());

//  ou utiliser un objet qui indique le nom du model et l'alias
console.log((await Ship.findAll({
  include: {
    model: Captain,
    as: 'leader'
  }
})).toJSON());

const ship = Ship.findOne();
// on utilise la méthode 'getLeader()' (au lieu de 'getCaptain()') 
console.log((await ship.getLeader()).toJSON());
```

Lors de la définition d'un alias pour :

- Une association `hasOne` ou `belongsTo` : on utilise un nom au singulier
- Une association `hasMany` et `belongsToMany` : On utilise un nom au pluriel

Il est possible de définir en même temps un alias et un nom de clé étrangère personnalisé

```JS
Ship.belongsTo(Captain, { as: 'leader', foreignKey: 'bossId' }); 
```

Les alias sont utiles lorsqu'on doit définir deux associations différentes entre les mêmes modèles. On utilise un alias différent pour chaque association afin d'éviter les ambiguïtés.

```js
Team.hasOne(Game, { as: 'HomeTeam', foreignKey: 'homeTeamId' });
Team.hasOne(Game, { as: 'AwayTeam', foreignKey: 'awayTeamId' });
Game.belongsTo(Team);
```

## Requêtes avec des associations

### Récupérer les données

Sequelize utilise deux techniques pour récupérer les données :

- Le *Lazy loading* : consiste à récupérer uniquement les données qui sont utiles
- le *Eager loading* : consiste à récupérer toutes les données (via des jointures)

#### Lazy loading

```JS

// Model Ship
const Ship = sequelize.define('ship', {  
  name: DataTypes.TEXT,  
  crewCapacity: DataTypes.INTEGER,  
  amountOfSails: DataTypes.INTEGER  
});  

// Model Captain
const Captain = sequelize.define('captain', {  
  name: DataTypes.TEXT,  
  skillLevel: {  
    type: DataTypes.INTEGER,  
    validate: { min: 1, max: 10 }  
  }  
});  

// relation One-To-One 
Captain.hasOne(Ship);  
Ship.belongsTo(Captain);


// on fait une requête pour récuper un capitaine
const awesomeCaptain = await Captain.findOne({  
  where: {  
  name: "Jack Sparrow"  
  }  
});  


// On affiche les données du captaine récupéré 
console.log('Name:', awesomeCaptain.name);  
console.log('Skill Level:', awesomeCaptain.skillLevel);  

// on effectue une nouvelle requête pour récupérer le bateau associé
const hisShip = await awesomeCaptain.getShip();  

// on affiche les données du bateau
console.log('Ship Name:', hisShip.name);  
console.log('Amount of Sails:', hisShip.amountOfSails);
````

#### Eager Loading

[[Eager Loading]]


### Créer les données 

Une instance peut être créée avec une association imbriquée en une seule étape

Exemple 1

```JS
const Tag = sequelize.define('tag', {  
  name: Sequelize.STRING
});  

Product.hasMany(Tag);

// pour créer un product avec plusieurs tags
Product.create({  
  id: 1,  
  title: 'Chair',  
  tags: [  
  { name: 'Alpha'},  // tag 1
  { name: 'Beta'}  .. // tag 2
  ]  
}, {  
  include: [ Tag ]  
})
```


Exemple 2

```JS

const Product = sequelize.define('product', {  
  title: Sequelize.STRING
});  

const User = sequelize.define('user', {  
   firstName: Sequelize.STRING,
   lastName: Sequelize.STRING
});  

const Address = sequelize.define('address', {  
  type: DataTypes.STRING,
  line1: Sequelize.STRING,
  line2: Sequelize.STRING,
  city: Sequelize.STRING,
  state: Sequelize.STRING,
  zip: Sequelize.STRING,
}); 


productUser = Product.belongsTo(User);
userAddresses = User.hasMany(Address);


// pour créer un product
Product.create({  
  title: 'Chair',  
    user: {  // model User
      firstName: 'Mick',  
      lastName: 'Broadstone',  
      addresses: [{  // model Address
        type: 'home',  
        line1: '100 Main St.',  
        city: 'Austin',  
        state: 'TX',  
        zip: '78704'  
      }]  
    }  
  }, {  
  include: [{  
    association: productUser,  // on précise l'association
    include: [ userAddresses ]  // qui inclus une autre association
  }]  
});
```

###  Mise à jour et suppression

Pour les mises à jour et suppression il n'est pas possible d'utiliser une seule étape. 
Il faut effectuer chaque action de manière explicite via les méthodes spéciales 

