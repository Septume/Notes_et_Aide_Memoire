# Base de données

L’ extension PDO permet d’accéder à n’importe quel type de base de données. ( MySQL, PostgreSQL, Oracle…).

Pour activer extension pour MySQL il faut dans le fichier `php.ini` décommenter la ligne :

`extension=php_pdo_mysql.dll`

### Se connecter à une base de données

On créé un objet PDO avec en paramètre du constructeur :

- le DSN (Data Source Name) sous la forme : `mysql:host=nom_hote;dbname=nom_base;charset=utf8`
- le login d’accès
- le mot de passe d’accès
- facultatif : `array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION)` => Permet d’afficher les erreurs SQL lors des requêtes. **Attention : A utiliser uniquement en développement et pas en production**

La connexion à la base de données se fait une seule fois dans la page même lorsqu’il y a plusieurs requêtes

```php
$bdd = new PDO('mysql:host=localhost;dbname=nom_base;charset=utf8', 'root', 'password', array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
```

Il faut également traiter les erreurs pour éviter que des informations sensibles soient affichées sur l’écran de l’utilisateur en cas d’échec de la connexion

```php
try{
    $bdd = new PDO('mysql:host=localhost;dbname=nom_base;charset=utf8', 'root', 'password', array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
}

catch (Exception $e){
    die('Erreur : ' . $e->getMessage());
}
```

### Effectuer une requête en lecture

`query()` : Méthode à appliquer sur l’objet PDO créé pour effectuer une requête. Prend en paramètre la requête SQL. Retourne un objet contenant la réponse à la requête

`fetch()` : Méthode à appliquer sur l’objet contenant la réponse. Retourne un tableau correspondant à la première ligne. Chaque valeur du tableau correspond à un champ de la base. Pour extraire toutes les lignes il faut utiliser une boucle `while()` qui sera exécutée tant qu’il reste des données à lire. A chaque tour de boucle, la méthode `fetch()` retourne une nouvelle ligne ou `false` s’il il n’y a plus de lignes à lire.

`closeCursor()` : Méthode à appliquer sur l’objet contenant la réponse. Permet de terminer la requête en fermant le curseur d’analyse des résultats

```php
// on se connecte à la base de donnée
try{
    $bdd = new PDO('mysql:host=localhost;dbname=mabase;charset=utf8', 'root', 'password');
} 
catch (Exception $e){
    die('Erreur : ' . $e->getMessage());
}

/* on effectue une requête 
sur les champs "nom" et "prenom"
de la base "membres" */

$reponse = $bdd->query('SELECT nom, prenom FROM membres');

/* on traire la réponse pour afficher
le nom et le prenom de chaque membres */
while ($donnees = $reponse->fetch()) {
    echo '<p>' . $donnees['nom'] . '</p>';
    echo '<p>' . $donnees['prenom'] . '</p>';
}

// on termine le traitement de la requête
$reponse->closeCursor();
```

La fonction `nl2br()` permet de convertir les retours à la ligne en balises HTML `<br />` (Utile pour conserver les retours à la ligne saisis dans les formulaires)

### Requêtes préparées

Permet d’exécuter des requêtes en fonction de variables.

Dans un premier temps on utilise la méthode `prepare()` pour construire la requête préparée. Cette méthode prend en paramètre une requête SQL contenant des marqueurs `?` pour indiquer où se trouve les paramètres. On exécute ensuite la requête préparée avec la méthode `execute()`. Celle-ci prend en paramètre un tableau contenant la liste des valeurs à utiliser dans l’ordre (Il possible d’utiliser des variables)

```php
// on prepare la requête

$req = $bdd->prepare('SELECT nom, console, prix FROM jeux_video WHERE console = ? AND prix <= ?');

/* on exécute la requête avec :
console = Xbox
prix <= 10 */

$req->execute(array('Xbox', 30));
```

Il est possible d’utiliser des marqueurs nominatifs sous la forme `:nom`

Dans ce cas la fonction `execute()` utilise un tableau associatif (l’ordre n’a plus d’importance)

```php
$req = $bdd->prepare('SELECT nom, console, prix FROM jeux_video WHERE console = :console AND prix <= :prix');

$prix = 30;
$console = 'Xbox';

$req->execute(array('prix' => $prix, 'console' => $console));
```

### Effectuer une requête sql en écriture

On utilise la méthode `exec()` pour l’insertion (INSERT TO) la modification (UPDATE SET) ou la suppression de donnée (DELETE). La requête retourne le nombre de lignes de la table qui sont impactées ou `false` s’il y a eu une erreur

```php
$bdd->exec("INSERT INTO jeux_video(nom, console, prix) VALUES('Battlefield 1942', 'PC', 45)");
```

Il est possible d’utiliser une requête préparée

```php
$req = $bdd->prepare('INSERT INTO jeux_video(nom, console, prix) VALUES(:nom, :console, :prix)');

$req->execute(array(
	'nom' => 'Battlefield 1942',
	'console' => 'PC',
	'prix' => 45
));
```

**Attention : En SQL le délimiteur d’un chaine est l’apostrophe. Ce qui peut créer des problèmes si la chaine envoyée contient elle-même des apostrophes.**

Solutions :

- utiliser la fonction `addslashes()`
- utiliser les requêtes préparées

### Sécurité

Injection SQL : injection de code SQL malveillant via les formulaires

Solutions :

- Interdire la connexion en root pour limiter les risques
- utiliser toujours les requêtes préparées
