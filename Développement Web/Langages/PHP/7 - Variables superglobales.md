# Variables superglobales

Variables de type array associatif générées automatiquement par PHP à chaque chargement de la page. Accessibles partout dans le script

`$GLOBALS` : stocke toutes les variables de l’espace global. Utile pour accéder à une variable globale depuis une fonction

```php
$nombre = 0; // variable globale 

function incremente(){
    $GLOBALS['nombre']++; // accès à la variable globale 'nombre'
    echo $GLOBALS['nombre']
}

incremente(); // 1
incremente(); // 2
```

- `$_GET`: données envoyées avec la méthode GET
- `$_POST`: données envoyées avec la méthode POST
- `$_REQUEST` : données envoyées avec les méthodes POST, GET ou via un cookie (déconseillé à l’utilisation)
- `$_FILES` : liste des fichiers qui ont été envoyés
- `$_SESSION` : variables de session qui restent stockées sur le serveur le temps de la visite d’un visiteur.
- `$_COOKIE` : contient les valeurs des cookies enregistrés sur l’ordinateur du visiteur.
- `$_SERVER`: Informations sur le serveur
	- `$_SERVER['SERVER_NAME']` : nom canonique du serveur ou de l’hôte virtuel
	- `$_SERVER['DOCUMENT_ROOT']`: racine du serveur (répertoire où sont stockés les pages). Peut être utilisé pour indiquer l’adresse d’un fichier
	- `$_SERVER['REMOTE_ADDR']` : adresse IP du client
- `$_ENV` : variables d’environnement
