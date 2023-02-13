# Introduction

### Syntaxe de base

Balise PHP : `<?php /* code PHP ici */ ?>`

Une balise PHP peut être mis n’importe où dans le code HTML (`head` compris)

Les instructions se terminent toujours par un point-virgule

```php
<?php 
    // Affichage
    echo "Hello World" </br>;
?>
```

il est recommandé d’enlever la balise de fermeture `?>` sur les pages qui ne contiennent que du code PHP

### Inclure le code d’un autre fichier

- `include(fichier.php)` : si le fichier n’est pas trouvé, un avertissement s’affiche et le script continu son exécution
- `require(fichier.php`) : si le fichier n’est pas trouvé, une erreur s’affiche et le script s’arrête brusquement.
- `include_once(fichier.php)` et `require_one(fichier.php)` : le fichier est inclus sur la page qu’une seule fois. Les autres inclusions seront ignorées (utile pour les fichiers contenant des fonctions et des classes)

La constante `$_SERVER['DOCUMENT_ROOT']` permet d’obtenir la racine du serveur web (à utiliser en préfixe dans les adresses)

### Interrompre le script

`exit()` ou `die()`

On peut indiquer en argument un message à afficher avant l’arrêt ou un entier indiquant un code de retour

### Fichier de configuration

Fichier `php.ini`

Le `;` permet de commenter les lignes

Pour afficher les erreurs

`display_errors = On`

`error_reporting = E_ALL`

### Serveur intégré

Lancer la commande : `php -S`
