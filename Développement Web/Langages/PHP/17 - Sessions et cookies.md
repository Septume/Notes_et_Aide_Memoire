# Sessions et cookies

### Les sessions

Permet de transmettre des données de page en page via des variables de session. Une session se termine automatiquement quand l’utilisateur ferme le navigateur

Démarrer une session : `session_start()`

Cette fonction doit être appelée en début de script avant tout contenu et sur toutes les pages où on a besoin d’utiliser des variables de session

Elle créé une clé unique ( PHPSESSID ) pour permettre de reconnaitre l’utilisateur. côté client le PHPSESSID est stocké dans un cookie. côté serveur les informations sur les sessions utilisateurs sont stockés dans des fichiers (placés dans un dossier spécial de PHP)

Pour définir les variables de sessions on utilise la variable superglobale `$_SESSION`

Page 1

```php
<?php 
session_start();
$_SESSION['pseudo'] = 'Toto';
?>
<!DOCTYPE html>
<html lang="fr">
    <head>
        <meta charset="UTF-8">
        <title>Accueil</title>
    </head>
    <body>
        <h1>Bienvenue <?php echo $_SESSION['pseudo'] ?></h1>
        <p><a href="profil.php">Voir mon profil</a></p>
    </body>
</html>
```

page 2

```php
<?php 
session_start();
?>

<!DOCTYPE html>
<html lang="fr">
    <head>
        <meta charset="UTF-8">
        <title><?php echo $_SESSION['pseudo'] . ' : Mon profil' ?></title>
    </head>
    <body>
        <h1>Profil de <?php echo $_SESSION['pseudo'] ?></h1>
    </body>
</html>

```

Il faut utiliser les sessions sur toutes les pages où l’utilisateur doit être connecté pour la consulter. Si l’utilisateur n’est pas connecté, on peut le rediriger vers la page de connexion

```php
if(!isset($_SESSION['pseudo']))) {
    //redirection vers la page de connexion
	header("Location:connexion.php");
}
```

Pour supprimer une session :

- `session_unset()` : détruit toutes les variables de session
- `session_destroy()`: supprime la session

### Les cookies

Chaque cookie stocke généralement une information à la fois

### Écrire un cookie

`setcookie()`Cette fonction doit être appelée une seule fois pour chaque cookie et avant l’affichage de tout contenu

paramètre obligatoire : nom du cookie

Paramètres facultatifs :

- valeur du cookie
- chemin sur lequel le cookie est accessible
- les dossiers pour lesquels le cookie est accessible
- le domaine pour lequel le cookie est accessible
- un booléen qui indique si le client doit obligatoirement utiliser une connexion sécurisée (https) pour transmettre le cookie
- un booléen qui indique si le cookie doit être disponible uniquement via le protocole http. (permet d’avoir une protection contre les faille XSS en interdisant l’accès au cookie aux langages de scripts comme JS)

Pour définir une date d’expiration du cookie, on utilise `time()` pour avoir le timestramp actuel puis on ajoute le nombre de secondes dans le quel le cookie doit expirer

Exemple 1

```php
setcookie('pseudo', 'jean', time() + 365*24*3600, null, null, false, true)
```

Exemple 2

```php
setcookie('pseudo', 'jean', time() + 365*24*3600, '/', 'monsite.com', false, true)
```

### Récupérer la valeur d’un cookie

Les informations du cookie sont indiquées dans la variable superglobale `$_COOKIE`

Exemple pour récupérer une valeur : `$_COOKIE['pseudo']`

Si le cookie n’existe pas, la variable superglobale n’existe pas. Il faut donc faire un `isset()` pour vérifier si le cookie existe ou non. (Il faut penser à le faire sur toute les pages au cas où le cookie a été effacé)

Attention :

- Comme toute information qui vient du visiteur le cookie n’est pas sur car modifiable
- Après sa création le cookie est accessible uniquement qu’au chargement de la prochaine page ou au rechargement de la page courante

### Modifier un cookie existant

Il faut refaire appel à `setcookie()` en gardant les même arguments mais avec une valeur différente (le temps d’expiration du cookie est remis à zéro)

```php
setcookie('pseudo', 'pierre', time() + 365*24*3600, null, null, false, true)
```

### Supprimer un cookie

On refait appel à `setcookie()` en indiquant une date d’expiration déjà passée Il n’est pas nécessaire de repréciser la valeur du cookie

```php
setcookie('pseudo', '', time() - 1, null, null, false, true)
```
