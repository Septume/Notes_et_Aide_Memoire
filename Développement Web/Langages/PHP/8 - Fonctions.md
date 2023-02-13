# Fonctions

### Définition et appel

```php
function nomFonction (parms…) {
    instructions;
    return valeur; 
} 
```

Appel : `nomFonction(args…);`

Il est possible de donner des valeurs par défaut aux paramètres. Ces paramètres optionnels doivent être indiqués après les paramètres obligatoires

### Indiquer le type des paramètres

permet d’imposer le type de valeur. on indique le nom du type devant le nom du paramètre

les types autorisés sont :

- `int`
- `float`
- `bool`
- `string`
- `array`
- `callable` (la valeur est un nom de fonction appelable)

Si la valeur passée en argument n’est pas du bon type, PHP lève une exception `typeError`

### Passage par valeur ou référence

Par défaut PHP utilise le passage par valeur. sauf pour les objets => passage par référence

Pour forcer le passage par référence on utilise l’opérateur & devant le nom du paramètre

`function nomFunction (&parametre)`

### Fonctions avec un nombre de paramètres variables

`function nomFonction (… params) {}`

Exemple

```php
function liste(...$element) {
	$nbElements = count($element);
	$elements = implode(" - ", $element);
	return 'Nombre d\'éléments : ' . $nbElements . '<br> Elements : ' . $elements;
}

echo liste('pim', 'pam', 'poum'); 

/* nombre d'élément : 3
Elements : pim - pam - poum 
*/
```

Remarque : on peut utiliser un tableau précédé de `…` pour indiquer une liste d’arguments

```php
$elements = ['pim', 'pam', 'poum'];
echo liste('toto', ...$elements); 

/* nombre d'élément : 3
Elements : toto - pim - pam - poum 
*/
```

### Fonction anonyme

Fonction sans nom qui peut être utilisée comme fonction de rappel ou valeur de variable

```php
$variable = function(){/* instructions */};$variable();
```

### Fonction générateur

Permet de retourner plusieurs valeurs dans un objet `generator` N’utilise pas le mot clé `return` mais le mot clé `yield`

```php
function generateur() {
        for ($i = 1; $i <= 5; $i++){
        yield $i;
}
}

$generateur = generateur();  

foreach ($generateur as $valeur) {
        echo $valeur . ' '; 
}
```
