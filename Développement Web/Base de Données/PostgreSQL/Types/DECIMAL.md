##### Permet la création d'une valeur précise avec un nombre choisie derrière la virgule.

```sql
CREATE TABLE Mytable ( 
	id SERIAL PRIMARY KEY, 
	taux DECIMAL(5,2) 
);
```

La colonne "taux" est de type "decimal" avec une précision de 5 chiffres au total et 2 chiffres après la virgule.

```sql
INSERT INTO MyTable (taux) VALUES (55.5);
```

exemple, insère une valeur à "taux" de 55,5%.