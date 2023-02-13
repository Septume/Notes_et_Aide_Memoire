# Jointures

Utiliser pour combiner les colonnes d'une ou plusieurs tables en fonction de colonnes communes clés primaire <=> clé étrangère

## Types de jointures 

![[types-jointures.png]]

**Exemple** 

Table ville
![[ex-table-ville.webp]]

Table email
![[ex-table-mail.webp]]


### Jointure interne 

`INNER JOIN` : retourne les enregistrements quand la condition est vrai dans les 2 tables. Typiquement, cette condition sera l’égalité d’un attribut en commun

![[inner-join.png]]


```SQL
SELECT *
FROM A
INNER JOIN B ON A.key = B.key;
```

**Exemple**

```SQL
SELECT id_client, nom, prenom, email, ville
FROM ville
INNER JOIN email
ON ville.id_client = email.id_client;
```

On obtient seulement les `id_client` qui sont présent dans les deux tables c'est à dire les id 1, 2 et 3
![[ex-inner-join.webp]]


### Jointure externe gauche

`LEFT JOIN`  :   retourne tous les enregistrements de la table de gauche même s’il n’y a pas de correspondance avec la table de droite. Dans ce cas les valeurs manquantes sont définies à `NULL` 

![[left-join.png]]

```SQL
SELECT *
FROM A
LEFT JOIN B ON A.key = B.key;
```

**Exemple**

```SQL
SELECT ID_CLIENT, NOM, PRENOM, VILLE 
FROM EMAIL
LEFT JOIN VILLE
ON EMAIL.ID_CLIENT = VILLE.ID_CLIENT;
```

On affiche toute les lignes de la table email. Si il n'y a pas de correspondance dans la table ville la valeur `NULL` est indiquée

![[ex-left-join.webp]]


### Jointure externe droite

 `RIGHT JOIN`  :  idem mais pour la table de droite

![[right-join.png]]

```SQL
SELECT *
FROM A
RIGHT JOIN B ON A.key = B.key;
```

**Exemple**

```SQL
SELECT id_client, nom, prenom, ville 
FROM email
RIGHT JOIN ville
ON email.id_client = ville.id_client;
```

On affiche toute les lignes de la table ville. Si il n'y a pas de correspondance dans la table email la valeur `NULL` est indiquée

![[ex-right-join.webp]]

### Jointure externe complète

 `FULL JOIN` :  retourne les résultats quand la condition est vrai dans au moins une des 2 tables.
 
![[full-join.png]]

```SQL
SELECT *
FROM A
FULL JOIN B ON A.key = B.key;
```

**Exemple**

```SQL
SELECT id_client, nom, prenom, ville
FROM ville
FULL JOIN email
ON ville.id_client = email.id_client;
```


![[ex-full-join.webp]]



