# Sequelize - Validateurs et contraintes

## Validateurs

Permet de valider les entrées utilisateurs avant d'envoyer la requête à la base de données.  
Les validateurs se déclenche lors de l'appel des méthodes `create()` et `update()`  
Ils se définissent au niveau du model en utilisant la propriété `validate` qui prend comme valeur un objet de configuration des validateurs


### Utiliser des validateurs prédéfinies

[Voir la liste des validateurs ](https://sequelize.org/docs/v6/core-concepts/validations-and-constraints/)

Si la validation échoue, Sequelize retourne une erreur `ValidationError` 
On peut retourner un message personnalisé avec l'option  `msg` 

```js
 sequelize.define(
  'user',
  {
    id: {
      type: DataTypes.INTEGER,
      primaryKey: true,
      autoIncrement: true,
    },
    name: {
      type: DataTypes.STRING,
      allowNull: false, // valeur obligatoire
      validate: {
        notEmpty: { msg: 'le nom ne peut pas être vide' },
        notNull: { msg: 'le nom est requis' },
      }
    },
    avatar: {
      type: DataTypes.STRING,
        allowNull: false,
        validate: {
          isUrl: { msg: 'URL non valide' },
          notNull: { msg: "l'image est requise" },
        },
    }
  }
);
```

Il faut également dans le code pour l'ajout ou la mise à jour des enregistrements indiqué la gestion des erreurs liés aux validateurs

```js
 app.post('/api/users', (req, res) => {
    User.create(req.body)
      .then(data => {
        const message = `L'utilisateur ${req.body.name} a bien été crée.`;
        res.json({ message, data });
      })
      .catch((error) => {
        // si la validation a échoué
        if (error instanceof ValidationError) {
          return res.status(400).json({ message: error.message, data: error });
        }
        const message = "L'utilisateur n'a pas pu être créé";
        res.status(500).json({ message, data: error });
      });
  });
```




### Créer des validateurs personnalisés

Exemple

```js
validate: {
  // définition du validateur personnalisé "isTypesValid"
  isTypesValid(value) {
    // test si au mois un type a été indiqué
    if (!value) {
      // on lève une erreur si la validation echoue
      throw new Error('un pokémon doit au moins avoir un type');
    }
    if (value.split(',').length > 3) {
      throw new Error('un pokémon ne peut pas avoir plus de 3 types');
    }
  },
}
```

## Contraintes

Permet de définir des règles de validation au niveau de la base de données qui ont en fonction de ces règles va accepter ou non la requête.
Si la vérification échoue, la base de données retourne une erreur qui sera transmis à JavaScript 


```js
 name: {
    type: DataTypes.STRING,
    allowNull: false, // on refuse les valeurs NULL
    // contrainte qui permet de garantir l'unicité du nom
    unique: {
      msg: 'Le nom est déjà pris',
    }
  }
```

Puis on ajoute la gestion des erreurs

```js
if (error instanceof ValidationError ||error instanceof UniqueConstraintError) {
   return res.status(400).json({ message: error.message, data: error });
}
```

Remarque sur `allowNull` 
Il s'agit d'un mélange entre une validation Sequelize et une contrainte SQL. 
- Génère une erreur `ValidationError` sans exécution d'une requête SQL
- Lors d'un  `sequelize.sync`, la colonne sera définie dans la base de données avec une contrainte  `NOT NULL`
