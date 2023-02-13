# Définition des données

## Types de données

Type les plus courant

- `integer` : entier
- `real` ou `double precision`  : nombre à virgule flottante
- `numeric`  : pour stocker des nombres décimaux où l'exactitude est requise. Peut contenir la valeur spéciale `NaN`
- `money` : stocke un montant en devise avec un nombre fixe de décimales. La précision de la partie fractionnée est déterminée par le paramètre `lc_monetary` de la base de données.
- `character varying` : chaine de caractères variable avec limite
- `character` : chaine de caractères de longueur fixe
- `text` : chaine de caractères sans limite
- `boolean` : 3 états => `TRUE` , `FALSE` et `NULL`
- `timestamp` : date et heure
- `date`
- `time`

Chaque type de données a son propre type de tableau correspondant, par exemple, un entier a un type de tableau `integer[]`

Pour les chaines de caractères il est recommandé d'utiliser `character varying` ou `text`


### Date et heure

Pour les dates, postgreSQL utilise le format  `yyyy-mm-dd`  (ex:  2000-12-31)

horodatage :
-   `timestamp` : timestamp sans fuseau horaire.
-   `timestamptz` : timestamp avec un fuseau horaire
    
Pour définir le fuseau horaire du serveur de la base de données

```SQL
SET timezone = 'America/Los_Angeles';
```


##  Auto incrémentation

`serial` : il ne s'agit pas d'un vrai type mais plutôt un raccourci de notation pour créer des id unique ((similaires à la propriété `AUTO_INCREMENT` utilisée par d'autres SGBD). Une contrainte `NOT NULL` est ajoutée pour s'assurer qu'une valeur NULL ne puisse pas être insérée.

```SQL
CREATE TABLE nom_de_table (
  nom_de_colonne SERIAL
);
```

## Contraintes


Contrainte de  colonne : concerne une seule colonne
Contrainte de table : concerne plusieurs colonne


Type de contraintes
-   `CHECK` : La valeur doit correspondre à une condition
-   `NOT NULL` : La valeur ne peut pas être nulle
-   `UNIQUE` : La valeur doit être unique par rapport aux autres lignes
-   `PRIMARY KEY` : Clé primaire. Ajoute automatiquement un index unique B-tree  et force la valeur à être `NOT NULL`.
-   `FOREIGN KEY` : Clé étrangère. Cela oblige à ce que la valeur corresponde à la clé de l'autre table. On dit que cela maintient l'_intégrité référentielle_ entre les deux tables. Si la clé étrangère provient de la même table on dit qu'elle est _auto-référencée._ La table qui contient la clé étrangère est appelée table de référencement ou table enfant. Et la table référencée par la clé étrangère est appelée la table référencée ou la table parent.
    

Comportements à adopter lorsque la clé primaire de la table référencée est supprimée et mise à jour.
-   `RESTRICT` : Interdire la suppression de la ligne référencée
-   `NO ACTION` : idem avec levée d'une erreur . Comportement par défaut
-   `CASCADE` : Supprimer automatiquement la ligne dans l'autre table => entraine une suppression en cascade
-   `SET NULL` ou `SET DEFAULT` : Mettre la valeur dans l'autre table à nulle ou utiliser celle par défaut
