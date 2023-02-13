# Identifiant unique

fonction `uniqid()`

2 arguments facultatifs :

- préfixe à ajouter à l’id (chaine)
- le booléen `true` pour obtenir un id plus long

Pour rendre l’id plus aléatoire on peut utiliser en plus la fonction `md5()`

```php
$id = md5(uniqid('', true));
```
