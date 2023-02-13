# Interroger les données

## Effectuer une sélection

On utilise la déclaration `SELECT`

```sql
-- pour selectioner une ou plusieurs colonne d'une table
SELECT collums2, collum2 FROM table_name;

-- pour sélectionner toutes les colonnes d'une table
SELECT * FROM table_name;
````

Il est possible d'utiliser des expressions

```SQL
SELECT 5 * 3;
```

### Concaténation

On peut faire une concaténation du résultat avec l'opérateur `||`

```SQL
-- fait une concaténation des valeurs des deux colonnes en ajoutant un espace entre
SELECT first_name || ' ' || last_name FROM customer;
```

### Alias

#### Colonne

Permet d'attribuer un nom temporaire à une colonne ou une expression

```SQL
SELECT column_name AS alias_name FROM table_name;
````

Si le nom de l'alias contient des espaces il faut l'entourer de guillemets doubles

```SQL
SELECT first_name || ' ' || last_name AS "full name" FROM customer;
```

Le mot-clé `AS` est facultatif, on peut donc utiliser une syntaxe raccourci

```SQL
SELECT column_name alias_name
FROM table_name;
```

#### Table

On peut également utiliser un alias pour les tables 

```SQL
table_name AS alias_name;

-- le mot clé AS peut être ommis 
table_name alias_name;

```

Les alias de table sont utiles pour rendre les requêtes plus lisible . 
Par exemple au lieu d'utiliser cette expression : `a_very_long_table_name.column_name` 
On peut utiliser un alias : `a_very_long_table_name AS alias`
Et utiliser l'alias pour faire référence à la colonne : `alias.column_name`

Les alias de table sont également très utiles dans le cadre des jointures 

```SQL
SELECT
	c.customer_id,
	first_name,
	amount,
	payment_date
FROM
	customer c
INNER JOIN payment p 
    ON p.customer_id = c.customer_id
ORDER BY 
   payment_date DESC;
```

Enfin les alias de table doivent obligatoirement être utilisés dans le cadre d'une table qui s'auto-référence 

```SQL
SELECT
    e.first_name employee,
    m.first_name manager
FROM
    employee e
INNER JOIN employee m 
    ON m.employee_id = e.manager_id
ORDER BY manager;
```



### Supprimer les lignes en doubles

  On utilise la clause `DISTINCT` suivi du nom du ou des colonnes permettant d'évaluer les doublons

```SQL
-- supprime les lignes ou la valeur de col1 est en double
SELECT DISTINCT col1 FROM demo;

-- suprrime les lignes où les valeurs de col1 ET col2 sont en double 
SELECT DISTINCT col1, col2 FROM demo;

```

## Trier les résultats

On utilise la clause `ORDER BY` suivi d'une expression servant pour le tri et éventuellement d'une option de tri :

- `ASC` : Pour trier par ordre croissant (valeur par défaut)
- `DESC` : Pour trier par ordre décroissant

```SQL
-- trier par prénom dans un ordre croissant
SELECT first_name, last_name FROM customer ORDER BY first_name;

-- trier par nom dans un ordre décroissant
SELECT first_name, last_name FROM customer ORDER BY last_name DESC;

-- trier dabord par prénom en ordre croissant puis par nom en ordre décroissant
SELECT first_name, last_name FROM customer ORDER BY first_name ASC, last_name DESC;
```

### Trier en fonction d'une expression

```SQL
-- la fonction LENGTH compte le nombre de caractères 
SELECT first_name, LENGTH(first_name) AS len
FROM customer
ORDER BY len DESC;
```

### Prise en compte des valeurs NULL

Tri croissant avec `ASC` : les valeurs NULL s'affichent à la fin  
Tri décroissant avec `DESC` : les valeurs NULL s'affichent au début

Pour changer ce comportement on peut utiliser en plus les options :

- `NULLS FIRST`
- `NULLS LAST`

```SQL
-- tri les bombe par ordre croissant et affiche les NULL en premier
SELECT num
FROM demo_table
ORDER BY num ASC NULLS FIRST;
```

## Filtrer les résultats

On utilise la clause `WHERE` suivi d'une condition

Operateurs logiques :

- `=` , `<`, `>`, `<=`, `>=`, `!=`
- `AND`, `OR`, `NOT`
- `IN` : si la valeur se trouve dans une liste (on peut aussi utiliser `NOT IN`) 
- `BETWEEN` : si la valeur se situe dans une intervalle on peut aussi utiliser `NOT BETWEEN`) 
- `LIKE` : si la valeur correspond à un ensemble de caractères. (on peut aussi utiliser `NOT LIKE`) 
  -  `%` :  correspond à toute séquence de zéro ou plus de caractères.
-    `_`  : correspond à n'importe quel caractère unique.
- `IS NULL` / `IS NOT NULL` 

```SQL
SELECT last_name, first_name FROM customer WHERE first_name = 'Jamie' AND last_name = 'Rice';

SELECT last_name, first_name FROM customer WHERE first_name IN ('Ann','Anne','Annie');

-- tous les clients dont le prénom commence par la chaîne `Ann` (% correspond à n'importe quelle chaine de caractère)
SELECT last_name, first_name FROM customer WHERE first_name LIKE 'Ann%';
```

```SQL
SELECT first_name, LENGTH(first_name) AS name_length
FROM customer
WHERE LENGTH(first_name) BETWEEN 3 AND 5
ORDER BY name_length;
```

Remarque : La clause `WHERE` peut également être utilisés avec les instructions `UPDATE` et `DELETE` pour spécifier les lignes à mettre à jour ou à supprimer.

### Limiter les résultats

On utilise la clause `LIMIT` suivi d'un nombre ou une expression

```SQL
-- limiter aux 10 premiers résultats
SELECT film_id, title FROM film ORDER BY film_id LIMIT 10;
```

Il est possible de démarrer à partir d'un certains nombre de ligne avec `OFFSET`

```SQL
-- commencer à la 6ème ligne et limiter aux 10 premiers résultats
SELECT film_id, title FROM film ORDER BY film_id LIMIT 10 OFFSET 5;
```
