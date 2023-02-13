# Gestion de la date

### Timestamp

timestamp PHP : nombre de secondes écoulés depuis le 1er janvier 1970 à 00:00:00 GMT

`time()` : permet d’obtenir le timestamp actuel.

`mktime(heure, minutes, secondes, mois, jour, annee)` : retourne le timestamp d’une date

```php
echo 'timestamp du 23 juin 2018 à midi : ' . mktime(12, 0, 0, 6, 23, 2018);
```

`strtotime(string)` : convertie une chaine de caractère représentant une date en timestramp La date doit être écrit dans un format valide (notation anglo-saxonne)

Exemple :

- `2018/06/23 12:00:00`
- `23 june 2018`
- `now`
- `+1 day`
- `next Saturday`

### Fonction date

Permet d’obtenir une date dans un format donné en argument. On peut également indiquer en deuxième argument un timestramp. Si ce dernier est omis, la fonction utilise la date actuelle

- `d` : Jour (01 - 31)
- `m` : Mois (01 - 12)
- `Y` : Année
- `N` : Nombre représentant le jour de la semaine (1 - 7)
- `H` : Heures (00 - 23)
- `i` : Minutes (00 - 59)
- `s` Secondes (00 - 59)

Exemple 1

```php
$jour = date('d');
$mois = date('m');
$annee = date('Y');
$heure = date('H');
$minute = date('i');
echo 'Bonjour ! Nous sommes le ' . $jour . '/' . $mois . '/' . $annee . ' et il est ' . $heure. 'h' . $minute;
```

Exemple 2

```php
echo date('d/m/Y H:i:s', 0); //01/01/1970 00:00:00 
```

### Vérifier la validité d’une date

`checkdate(mois, jour, annee)`

```php
var_dump(checkdate(12, 31, 2001)); // true
var_dump(checkdate(13, 31, 2001)); // false
var_dump(checkdate(11, 31, 2001)); // false
```
