Pour créer une table PostgreSQL qui va accueillir une image, vous pouvez utiliser le type de données "bytea" qui permet de stocker des données binaires (comme des images). Voici un exemple de requête SQL qui crée une table "images" avec une colonne "image_data" de type "bytea":

```sql
CREATE TABLE images (     id SERIAL PRIMARY KEY,     image_data BYTEA );
```

Cette requête crée une table "images" avec deux colonnes: "id" qui est un entier auto-incrémenté utilisé comme clé primaire, et "image_data" qui est de type "bytea" et qui va stocker les données de l'image.

Vous pouvez ensuite insérer des données dans la table en utilisant la fonction "lo_import" pour charger l'image depuis un fichier sur votre disque dur. Par exemple:

```sql
INSERT INTO images (image_data) VALUES (lo_import('/chemin/vers/image.jpg'));`
```

Cela va insérer l'image stockée dans le fichier "/chemin/vers/image.jpg" dans la colonne "image_data" de la table "images".

