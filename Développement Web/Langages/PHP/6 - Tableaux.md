# Tableaux

### Créer un tableau

### Tableaux numérotés

`$variable = array(valeur0, valeur1, valeur2, …);`

on peut aussi créer manuellement le tableau case par case

```php
$variable[0] = 'valeur'; 
$variable[1] = 'valeur';
$variable[2] = 'valeur';
```

Tableau à deux dimensions

```php
$variable = array(
    array(valeur0, valeur1, valeur2, ...); 
    array(valeur0, valeur1, valeur2, ...); 
    array(valeur0, valeur1, valeur2, ...); 
    ...
); 

$variable[0][0] = 'valeur';
```

### Tableaux associatifs

```php
$variable= array (
    'nom0' => 'valeur0' ,
    'nom1' => 'valeur1',
    'nom2' => 'valeur2'
); 
```

pour créer le tableau case par case :

```php
$variable['nom0']='valeur0'; 
$variable['nom1']='valeur0'; 
$variable['nom2']='valeur0'; 
```

Pour afficher un élément

`$variable[nom];`

### Parcourir un tableau

### Boucle for

pour obtenir la taille d’un tableau : `count($tab)`

### Fonction foreach()

`foreach($variable as $element){}`

Pour récupérer aussi la clé de l’élément

`foreach($variable as $cle => $element)`

### Fonctions pour les tableaux

- `print_r(array)` : permet d’afficher le contenu d’un tableau
- `array_key_exists('cle', $tab)` : vérifier si une clé existe. Prend comme paramètres le nom de la clé à chercher et le nom du tableau. Renvoie un booléen
- `in_array('valeur', $tab)` : vérifier si une valeur existe
- `array_search('valeur', $tab)` : récupérer la clé d’une valeur. Renvoie la clé correspondante (un nombre pour un tableau simple ou un nom pour un tableau associatif). Sinon renvoie false si aucune clé est trouvée
- `array_replace$($tab1, $tab2)` : remplace les éléments du premier tableau par ceux du deuxième en se basant sur la clé. Si une clé existe dans le second tableau mais pas dans le premier, elle sera créée. Si une clé existe dans le premier tableau mais pas dans le second elle reste inchangée. Plusieurs tableaux peuvent être indiqués pour le remplacement, dans ce cas ils seront traités dans l’ordre. Retourne NULL en cas d’erreur.
- `explode (séparateur, chaine)` : découpe une chaine dans un tableau selon un séparateur. Peut aussi prendre un entier comme 3ème argument indiquant le nombre max de cases de tableau, la dernière case contenant le reste de la chaine si besoin. On peut indiquer un entier négatif, dans ce cas tous les éléments sont retournés sauf les x derniers
- `implode(séparateur, tableau)` : regroupe les éléments d’un tableau dans une chaine à l’aide d’un séparateur
- `array_push(tableau, valeur1, valeur2,…)` : permet d’ajouter une ou plusieurs valeurs à la fin d’un tableau
- `array_pop(tableau)` : supprime le dernier élément du tableau et retourne sa valeur

#### Fonctions de tri

- `sort()` : tri croissant sur la valeur sans préservation des couples clé/valeur. SI le tableau est associatif il devient un tableau numéroté.
- `rsort()` : tri décroissant sur la valeur sans préservation des couples clé/valeur
- `asort()` : tri croissant sur la valeur avec préservation des couples clé/valeur
- `arsort()` : tri décroissant sur la valeur avec préservation des couples clé/valeur
- `ksort()` : tri croissant sur la clé avec préservation des couples clé/valeur
- `krsort()` : tri décroissant sur la clé avec préservation des couples clé/valeur

Prend en arguments :

- un tableau à trier
- (optionnel) un indicateur permettant de modifier le comportement du tri.
- `SORT_REGULAR` : comportement par défaut`SORT_NUMERIC` : compare les éléments numériquement`SORT_STRING` : compare les éléments comme des chaines de caractères`SORT_LOCALE_STRING` : compare les éléments comme des chaines de caractères et en utilisant la configuration locale définie par `setlocale()SORT_NATURAL` : compare les élément selon un ordre naturel`SORT_FLAG_CASE` : à utiliser avec SORT_STRING ou SORT_NATURAL pour ne pas prendre en compte la casse
