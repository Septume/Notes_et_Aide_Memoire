| Êtes-vous? | pas stressé(e) | peu stressé(e) | stressé(e) | très stressé(e) |
| :--------|:--------:|:--------:|:--------:|:--------:| --------:|
| Êtes-vous? | pas stressé(e) | peu stressé(e) | stressé(e) | très stressé(e) |
| Fumez-vous? | Jamais | vous avez arrêté depuis au moins 3 mois | occasionnellement | régulièrement |
| Quel est votre régime alimentaire? | Je mange de tout | végétalien | végan, (à revoir) | je fais souvent des écarts (fast-food, sucreries, etc…) |
| Combien de verres d’alcool consommez-vous par semaine? | Jamais | plus de 5 | plus de 10 | plus de 15 | plus de 20 |
| Combien de verres d’eau buvez-vous par jour? | Moins de 2 | 3-4 | 5-6 | 7-9 | 9 ou plus |
| Combien d’heures dormez-vous par nuit en moyenne? | Moins de 4 heures | 5-6 | 7-8 | 9-10 | plus de 10 |
| En moyenne, combien d’heures de sport faites-vous par semaine? | Jamais | 1-3 | 4-7 | 7-10 | plus de 11 |

form_id
gender 30
birth_date
stress
smoke
food
alcohol
water
sleep
sport

```sql
-- Tables de l'utilisateur

CREATE TABLE app_user (
	form_id int PRIMARY KEY,
	username varchar(30) NOT NULL,
	email varchar(100) NOT NULL,
	password varchar(1000) NOT NULL,
	register_date (date),
	last_connection (date),
	verified (boolean)
);

SELECT * FROM app_user;

-- Tables de la géolocalisation

CREATE TABLE geolocation (
	geo_id int PRIMARY KEY,
	temperature decimal(2,3),
	hygrometry decimal(2,3),
	pollution decimal(2,3)
);

SELECT * FROM geolocation;

-- Tables de stoquage des photos

CREATE TABLE pictures (
	picture_id int PRIMARY KEY,
	image_data bytea
);

SELECT * FROM pictures;

-- Tables du Formulaire

CREATE TABLE form (
	form_id int PRIMARY KEY,
	gender varchar(30),
	birth_date date,
	stress varchar(30),
	smoke varchar(30),
	alcohol varchar (30),
	water varchar(30),
	sleep varchar (30),
	sport varchar(30)
);

SELECT * FROM form;
```

