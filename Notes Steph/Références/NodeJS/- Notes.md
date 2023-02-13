Utilisation d'un module pour créer les routes 

```js
module.exports = (app) => {
  app.get('/path', (req, res) => {
    // traitements
  });
};
```

```js
const app = express();

// on importe la route
const route = require('./route');

// on met en place la route 
const app = express(); 

// on appelle la route en lui passant l'instance de l'app Express
route(app); 
```

Forme raccourci 

```js
const app = express();
require('./route')(app); 
```


---------------------
requête PUT

Pour éviter des problèmes de collision en cas de modification de la même ressource par plusieurs client en même temps la bonne pratique est de remplacer complètement la ressource par une nouvelle qui contient les éléments modifiés

```js
app.put('/api/users/:id', (req, res) => {
  const id = parseInt(req.params.id);
    // on créé un utilisateur avec les données envoyées + l'id passé en paramètre
  const userUpdated = { ...req.body, id: id };

  // on génére une nouvelle liste d'utilisateurs
  users = users.map(user => {
    // pour chaque utilisateur de la liste on retourne le même utilisateur sauf pour l'utilisateur modifié
    return user.id === id ? userUpdated : user;
  });

  const message = `L'utilisateur ${userUpdated.name} a bien été modifié.`;
  // on retourne l'utilisateur modifié
  res.json(success(message, userUpdated));
});
```

-------------------

 Requête Delete

```js
app.delete('/api/pokemons/:id', (req, res) => {
  const id = parseInt(req.params.id);
  // recherche de l'utilisateur dans la liste
  const userDeleted = users.find((pokemon) => user.id === id);
  // on filtre la liste pour retourner une nouvelle liste sans le pokemon à supprimer
  users = users.filter((user) => user.id !== id);
  const message = `L'utilisateur ${userDeleted.name} a bien été supprimé.`;
   // on retourne l'utilisateur supprimé
  res.json(success(message, userDeleted));
});
```
