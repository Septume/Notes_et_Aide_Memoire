# Gestion de la date

## Créer un objet date

`var date = new Date()`  

Si on n'indique pas d'argument pour le constructeur, la date créée (avec une heure locale) correspond à l'instant T où est exécuté le code

Le constructeur peut prendre en paramètre une date à créer. Celle-ci peut être indiquée :

- Sous la forme d'un entier : nombre de millisecondes écoulées depuis le 1er Janvier 1970 00:00:00 UTC ( Correspond à un timestramp Unix multiplié par 1000)
- Avec des nombres correspondant à l'année, mois etc
	- Année : les valeurs entre 0 et 99 correspondent aux années 1900 à 1999. Sinon indiquer un nombre à 4 chiffres
	- Mois : attention, le mois commence à 0 (pour janvier) et va jusqu'à 11 (pour décembre)
	- Jour (optionnel) : un entier entre 1 et 31 (par défaut : 1)
	- Heure (optionnel) : une entier entre 0 et 23 (par défaut : 0)
	- Minutes (optionnel) : un entier entre 0 et 59 (par défaut : 0)
	- Secondes (optionnel) : un entier entre 0 et 59 (par défaut : 0)
	- Millisecondes (optionnel) : un entier entre 0 et 999 (par défaut : 0)
- Sous une forme littérale. Ex : `Sat, 04 May 1991 20:00:00 GMT+02:00`

```jsx
var date = new Date(2020,11,25);
console.log(date); // Fri Dec 25 2020 00:00:00 GMT+0100
```

La méthode `Date.parse()` peut être utilisée pour tester une chaine de caractère correspond bien à une date littérale valide. Si oui la méthode retourne le timestramp de la date, sinon elle retourne `NaN`

```jsx
console.log(Date.parse('31 Jan 2020')); // 1580425200000
console.log(Date.parse('2020-01-31')); // 1580425200000
console.log(Date.parse('2020-31-01')); // NaN
```

## Méthodes

### Renvoyer les informations

- `getFullYear()` : Renvoie l'année sur 4 chiffres
- `getMonth()` : Renvoie le mois (0 à 11)
- `getDate()` : Renvoie le jour du mois (1 à 31)
- `getDay()` : Renvoie le jour de la semaine (0 à 6, la semaine commence le dimanche)
- `getHours()` : Renvoie l'heure (0 à 23)
- `getMinutes()` : Renvoie les minutes (0 à 59)
- `getSeconds()` : Renvoie les secondes (0 à 59)
- `getMilliseconds()` : Renvoie les millisecondes (0 à 999)
- `getTime()` : Renvoie le timestamp
- `getTimezoneOffset` : Renvie le décalage horaire en minute

### Modifier les informations

Pour chacune des méthodes précédentes, il existe une méthode similaire de type "*set*" qui permet de définir une valeur de date. Par exemple : `setFullYear()`, `setTime()` , etc.

### Affichage de la date

Ces méthodes renvoient la date sous la forme d'une chaine de caractère lisible par un humain

- `toDateString()` : Renvoie la date dans le format américain (ex : `Thu Jun 23 1977`)
- `toTimeString()` : Renvoie l'heure sous la forme `hh:mm:ss GMT+hhmm`
- `toString()` : Surchage la méthode héritée de l'objet `Object` . Renvoie la date et l'heure dans le format américain (Remarque : Cette méthode peut donner des resultats différents selon les implémentations)
- `toUTCString()` : Renvoie la date selon le fuseau horaire UTC
- `toISOString()` : Renvoie la date au format ISO 8601 (sous la forme de `YYY-MM-DDTHH:mm:ss.sssZ`). A noter que la méthode `toJSON()` (Qui permet de sérialiser des objets au format JSON) renvoie également la date au format ISO 8601 lorsque la méthode est appliquée sur un objet Date
- `toLocaleDateString()` : Permet de renvoyer la date selon une locale. On peut indiquer en argument une locale différente que celui du navigateur (ex : `de-DE`)
- `toLocaleTimeString()`
- `toLocaleString()`

```jsx
var date = new Date('2020-12-31 23:59');

console.log(date.toDateString()); // Thu Dec 31 2020
console.log(date.toTimeString()); // 23:59:00 GMT+0100
console.log(date.toString()); // Thu Dec 31 2020 23:59:00 GMT+0100

console.log(date.toUTCString()); // Thu, 31 Dec 2020 22:59:00 GMT
console.log(date.toISOString()); //2020-12-31T22:59:00.000Z

console.log(date.toLocaleDateString()); // 01/06/2018
console.log(date.toLocaleTimeString()); // 23:59:00
console.log(date.toLocaleString()); // 01/06/2018 à 00:35:56
console.log(date.toLocaleString("de-DE")); // 31.12.2020, 23:59:00

```

Les méthodes `toLocaleDateString()` et `toLocaleTimeString()` en plus de prendre comme argument une locale peuvent également prendre en deuxième argument un objet permettant de paramétrer des options d'affichage

Liste des propriétés et valeurs associées les plus intérressantes :

- `weekday` : Jour de la semaine.
	- `long` : Format long (Ex : *Thursday*)
	- `short`: Format court (Ex : *Thu*)
	- `narrow` : Lettre (Ex : *T*)
- `year` : Année
	- `numeric` (Ex : 2020)
	- `2-digit` : (Ex : 12)
- `month` : Mois
	- `numeric` (Ex : 1)
	- `2-digit` (Ex : 01)
	- `long`
	- `short`
	- `narrow`
- `day`, `hour`, `minute`, `second` : Les valeurs posssible sont `numeric` ou `2-digit`
- `timeZoneName` : Fuseau horaire.
	- `long` (Ex : *British Summer Time*)
	- `short` (Ex : *GMT+1*)

```jsx
var date = new Date('2020-12-31 23:59');
var options = {weekday: "long", year: "numeric", month: "long", day: "2-digit"};
console.log(date.toLocaleDateString("fr-FR", options)); // jeudi 31 décembre 2020
```
