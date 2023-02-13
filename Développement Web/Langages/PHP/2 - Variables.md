# Variables

### Déclaration et initialisation

Les noms de variable sont précédés du symbole `$`

`$nom_variable = valeur;`

Une variable non initialisée a pour valeur `null`

Pour afficher la valeur d’une variable PHP dans du code HTML on peut utiliser cette syntaxe raccourcie :

`<?= $variable; ?>`

### Type de variables

Types primitifs

- `integer` ou `int`
- `float`
- `bool`
- `string`

Types évolués

- `array`
- `object`
- `ressource` (référence vers une ressource : fichier, base de données…)
- `null` (variable non initialisée)

Connaitre le type d’une variable : `gettype($variable)`

vérifier si une variable est d’un type précis (retourne un booléen) :

- `is_int($var)`
- `is_float($var)`

	etc.

Forcer le changement de type : `settype ($var, nv_type)`

```php
$variable  = "7"
settype($variable, int)
```

Pour modifier l’interprétation du type d’une variable dans un calcul mais sans en changer réellement le type on utilise le transtypage

```php
$variable1 = 7
$variable2 = (string) $variable1;
```

### Test sur les variables

Tester si la variable a une valeur numérique : `is_numeric($var)`

Tester si une variable est définie (la variable est déclarée et initialisée) : `isset($var)`

Tester si une variable est vide (la variable a pour valeur `null`, 0, `false,` une chaine ou un tableau vide) : `empty($var)`

### Portée des variables

variable locale à une fonction :

- accessible uniquement dans cette fonction
- est détruite à la fin de l’exécution de la fonction

variable globale :

- accessible dans l’espace global. **Attention** : les fonctions n’ont pas accès aux variables globales
- est détruite à la fin de l’exécution du script

Niveau de portée des variables :

- superglobale : accessible partout. Il n’est pas possible de créer soi-même des superglobales
- globale : variable visible à l’extérieur des fonctions mais pas à l’intérieur, sauf sui on exporte la variable avec le mot clé `global` ou le tableau `$GLOBALS[]`
- statique : variable locale à une fonction qui persiste le temps d’exécution du script. Conserve ses différentes valeurs à chaque appel de la fonction
- locale : variable visible dans la fonction ou elle et définie

### Mot clé global

Permet d’accéder localement à une variable déclaré globalement

```php
$nombre = 10;
function affiche(){
    global $nombre;
	echo $nombre;
}
affiche();
```

### Mot clé static

Permet de créer un espace statique au sein duquel les variables locales à une fonction seront conservées le temps de l’exécution du script

```php
function compte(){
	static $nombre = 0;
	$nombre++;
	return $nombre;
}

echo compte(); // 1
echo compte(); // 2
echo compte(); // 3
```

### Détruire une variable

`unset(variable)`

La variable n’est plus affectée (La fonction `isset()` retourne `false`)

### Afficher les variables pour le débogage

`var_dump($var)` : Affiche le type et la valeur d’une variable au moment de l’exécution. Les tableaux et objets sont explorés récursivement avec des indentations pour mettre en valeur leur structure

`print_r($var)` : affiche des informations de manière lisible. Utile pour les tableaux et les objets.

Il est recommandé d’utiliser des balises HTML `<pre>` pour un meilleur affichage

```php
<pre>
	<?php 
	$tab = array('pim', 'pam', 'toto');
	print_r($tab);
	?>
</pre>
```
