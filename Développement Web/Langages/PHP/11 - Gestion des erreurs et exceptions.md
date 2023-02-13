# Gestion des erreurs et exceptions

### Les messages d’erreurs de php

![](php-errors.png)

Depuis la version 7 la plupart des erreurs fatales sont signalées en levant une exception de type `Error`. Si l’exception n’est pas traitée, le script s’arrête

### Fonctions de gestion des erreurs

`error_reporting(niveau)` : permet de définir le niveau d’erreur. Sans argument retourne la valeur courante. Il est recommandé d’utiliser les nom de constantes plutôt que les valeurs numériques

Exemple :

- `E_ERROR+E_WARNING` : les niveaux `ERROR` et `WARNING`
- `E_ALL-E_ERROR` : tous les niveaux sauf `ERROR`

`error_log(message, type, destination, complement)` : permet d’envoyer un message d’erreur vers une destination. Retourne un booléen pour indiquer le succès ou échec. Les arguments :

- message à envoyer (chaine)
- type de destination (entier) :
- 0 - historique PHP (le fichier de sortie est défini par la directive de config `error_log`)
- 1- adresse mail
- 3 - fichier
- précision de la destination pour les types 1 et 3
	- adresse mail
	- nom de fichier (sera créé s’il n’existe pas)
- facultatif : entête supplémentaire à envoyer pour le type 1 (voir fonction `mail()`)

### Exceptions

```php
try {
	// code a tester
	//  s’il n'y a pas d'erreur, le bloc est exécuté
} catch(Exception $e) {
	// ce bloc est exécuté si une erreur est detectée
	echo $e->getMessage(); // retourne le message de l'exception
} finally {
	// bloc facultatif
	// le code est exécuté dans tous les cas
}
```

`die()` : fonction qui permet d’arrêter le script. Peut prendre en argument une chaine de caractère affichant un message. On peut utiliser `die()` lorsqu’une exception est levé

```php
try {
    // code a tester
} catch(Exception $e) {
    die($e->getMessage()); // affiche le message d'erreur et arrête le script
}
```

`throw new Exception()` : permet de lever une exception. Peut prendre en argument le message à afficher ainsi qu’un code erreur

```php
$test = false; 
try {
    if($test){
        echo 'test ok';
    }else{
        throw new Exception("Echec du test"); // on lève une exeception si $test = false
    }
} catch(Exception $e) {
    // s'exécute si une exception est levée
    echo 'Erreur : ' . $e->getMessage();
}
```

Méthodes de la classes `Exception`

- `getMessage()` : permet de récupérer le message d’erreur
- `getCode()` : permet de récupérer le code d’erreur

Remarque : si une exception n’est pas traité => `Fatal error : Uncaught Exception`
