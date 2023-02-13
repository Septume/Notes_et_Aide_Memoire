# Gérer les tables

### Créer une table

```SQL
CREATE TABLE  posts(
  title VARCHAR(150),
  content TEXT,
  category VARCHAR(50),
  create_at DATETIME
);
```

Pour les colonnes on indique

- le nom
- le type
- facultatif : les contraintes

### Supprimer une table

```SQL
DROP TABLE IF EXISTS links;
```

### Modifier les colonnes d'une table

```SQL
-- suppression champ category
ALTER TABLE posts DROP category;
```

### Insérer des données 

```SQL
INSERT INTO table_name(column1, column2, ...)
VALUES (value1, value2, ...);
```

Attention : Les colonnes et les valeurs correspondantes doivent être indiquées dans le même ordre.

Exemple 

```SQL
CREATE TABLE links (
	id SERIAL PRIMARY KEY,
	url VARCHAR(255) NOT NULL,
	name VARCHAR(255) NOT NULL,
	description VARCHAR (255),
  last_update DATE
);

-- la valeur NULL sera indiquée pour description et last_update. L'id sera généré automatiquement
INSERT INTO links (url, name) VALUES('https://www.digifab.fr/','Digifab');


```

Remarque : les chaines de caractères doivent être indiquées entre guillemets simples. Si la chaine contient également une apostrophe `'`  il faut l'échapper avec une apostrophe supplémentaire 

```SQL
INSERT INTO links (url, name)
VALUES('https://www.chakchoukacorp.com','O''Chakchouka');
```

Les dates doivent être indiquées au format `AAAA-MM-JJ`

```SQL
INSERT INTO links (url, name, last_update)
VALUES('https://www.digifab.fr/','Digifab','2021-03-23');
```

La clause facultative `RETURNING` permet de retourner la ligne insérée 

```SQL
-- on retourne l'intégralité de la ligne inséré grace à *
INSERT INTO table_name(column1, column2, ...)
VALUES (value1, value2, ...)
RETURNING *;
```

```SQL
-- on retourne uniquement l'id de la ligne insérée
INSERT INTO table_name(column1, column2, ...)
VALUES (value1, value2, ...)
RETURNING id;
```

L'instruction `INSERT` renvoie une balise de commande sous la forme : `INSERT oid count`  ou `oid` est  un identificateur d'objet utiliser comme clé primaire en interne par PostGreSQL pour ses tables systèmes et `count` est le nombre de ligne insérées 

