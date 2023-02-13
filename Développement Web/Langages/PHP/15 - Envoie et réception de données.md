# Envoie et réception de données

### Url et get

### Envoyer des paramètres dans l’url

Format : `http//<www.site.tld/page.php?parm1=valeur1&parm2=valeur>`

- `?` : permet d’écrire les paramètres après l’url
- `&` : permet de séparer les paramètres .

Remarque :

- une URL ne doit pas dépasser les 256 caractères
- dans le code HTML les `&` doivent être écrit `&amp`. Exemple : `<a href="bonjour.php?parm1=valeurt&amp;parm2=valeur">`

### Récupérer les paramètres en php

La page qui reçoit les paramètres va automatiquement créer l’array `$_GET` dont les clés correspondent aux noms des paramètres envoyés en URL.

Attention : n’importe quel internaute peut modifier les paramètres d’une URL ce qui peut entrainer une modification du traitement de la page PHP cible. Il faut donc :

- toujours vérifier er que les paramètres attendus sont présent dans l’URL
- toujours vérifier qu’ils contiennent des valeurs correctes

pour contrôler les paramètres :

- `isset(parm)` : teste la présence du paramètre
- `empty(param)` : teste si le paramètre a une valeur vide

Exemple

Avec l’URL : `http://tests.test/?pseudo=stef&age=40`

```php
if(isset($_GET['pseudo']) AND !empty($_GET['pseudo'])){
	$pseudo = $_GET['pseudo'];
}else{
	$pseudo = 'inconnu';
}

echo '<p>Bonjour ' . $pseudo . '.</p>'; 

if(isset($_GET['age']) AND !empty($_GET['age'])){
	$age =  (int) $_GET['age'];
	if ($age > 0) {
		echo '<p>Vous avez ' . $age . ' ans.</p>';
	}else{
		echo '<p>Vous n\'avez pas indiqué votre âge.</p>'; 
	}
}else{
	echo '<p>Vous n\'avez pas indiqué votre âge.</p>'; 
}
```

Si les données envoyées dans l’URL contient des caractères spéciaux il faut d’abord faire un encodage avec la fonction `rawurlencode($chaine)`

### Formulaires

### Méthode post

Deux méthodes pour envoyer un formulaire :

- GET : les données sont transmis par l’URL que l’on récupère avec `$_GET`
- POST : les données sont récupérés avec `$_POST`

Pour utiliser à la fois la méthode GET et la méthode POST

- `method=post`
- on passe les arguments à transmettre à GET directement dans l’attribut `action`

Les clés de `$_GET` ou `$_POST`correspondent a l’attribut `name` des champs du formulaire

Remarque : un page contenant un formulaire peut s’appeler elle-même. Dans ce cas elle contiendra également le code pour le traitement des données.

```html
<form action="cible.php" method="POST">
    <p>
        <label for="pseudo"><strong>Votre pseudo</strong></label>
    </p>
    <p>
        <input type="text" name="pseudo" required>
        <input type="submit">
    </p>
</form>
```

```php
if(empty($_POST['pseudo'])){
    echo 'Erreur : pseudo inconnu';
}else{
	echo 'Bonjour ' . $_POST['pseudo']; 
}
```

Remarque pour les cases à cocher :

- si la case est cochée : la valeur de la variable sera `on`
- si la case n’est pas cochée : la variable n’est pas envoyé

=> il faut tester l’existence de la variable avec `isset()`

```html
<form action="cible.php" method="POST">
	<label for="newsletter"><strong>Inscription à la newsletter ? </strong></label>
	<input type="checkbox" name="newsletter">
	<input type="submit">
</form
```

```php
if (isset($_POST['newsletter'])){
    echo "vous êtes inscris à la newsletter";
}else {
    echo "vous n'êtes pas inscris à la newsletter";
}
```

### Listes à sélections multiples

La balise `<select>` permet d’avoir des listes à sélections multiples. Si plusieurs éléments sont sélectionnés par l’utilisateur, le paramètre sera envoyé plusieurs fois avec les différentes valeurs et seules la dernière sera prise en compte. Pour pallier au problème il faut mettre `[]` à la fin du nom du champ pour indiquer à PHP qu’il s’agit d’une liste avec plusieurs valeurs

```html
<form action="index.php" method="POST">
	<select name="id_langage[]" multiple>
		<option value="PHP">PHP</option>
		<option value="Python">Python</option>
		<option value="Java">Java</option>
		<option value="JavaScript">JavaScript</option>
		<option value="Ruby">Ruby</option>
	</select>
	<input type="submit" name="submit">
</form>
```

```php
if(!empty($_POST['id_langage'])){
	foreach ($_POST['id_langage'] as $option) {
		echo $option . '<br>';
	}
}
```

### Envoie de fichier

**Attention : on doit éviter que l’utilisateur puisse envoyer des fichiers PHP sur le serveur ou tout autre fichier exécutable.**

Pour indiquer au navigateur que l’on peut envoyer des fichiers on ajoute l’attribut `enctype="multipart/form-data"` à la balise `<form>`

La balise permettant d’envoyer un fichier est de type `<input type="file" />`

```html
<form action="cible.php" method="post" enctype="multipart/form-data">
    <p> Envoyer un fichier </p>
    <p><input type="file" name="fichier"/></p>
    <p><input type="submit" value="Envoyer le fichier" /></p>
</form>
```

Le fichier qui a été envoyé est stocké dans un dossier temporaire et est en attente de traitement

### Vérification du fichier

`$_FILES['fichier']` : contient les informations sur le fichier

- `$_FILES['fichier']['name']` : nom du fichier (contient le chemin complet)
- `$_FILES[fichier']['type']` : type du fichier (ex : image/gif)
- `$_FILES['fichier']['size']` : taille du fichier en octet (La configuration par défaut de PHP interdit l’envoi de fichier de plus de 8 Mo)
- `$_FILES[fichier']['tmp_name']` : emplacement temporaire du fichier (gérer par PHP)
- `$_FILES['monfichier']['error']` : code erreur. Si la valeur est 0, il n’y a pas d’erreurs

Pour vérifier l’extension du fichier : La fonction `pathinfo($_FILES['fichier']['name'])` renvoie un array qui contient entre autre l’ extension du fichier dans `['extension']` que l’on peut ensuite comparer à un tableau d’extensions autorisées via la fonction `in_array(tableau, tableau_de_comparaison)`

### Valider le fichier

fonction `move_uploaded_file()`

2 paramètres :

- Le nom temporaire du fichier : `$_FILES['fichier']['tmp_name']`
- Le chemin sous lequel est stocké le fichier de façon définitive. On peut utiliser le nom d’origine du fichier ou générer un nom au hasard. Il est cependant fortement recommandé de renommer le fichier pour éviter les éventuels problèmes (espaces dans le nom, nom déjà utilisé par un autre fichier…)

Comme `name` contient le chemin complet, on utilise la fonction `basename()` qui permet d’obtenir uniquement le nom du fichier : `basename($_FILES['fichier']['name'])`

Attention : Le dossier de destination doit exister et avoir les droits en écriture (733)

```php
$fichier_ok = false;

// test si le fichier a bien été envoyé 
if(isset($_FILES['fichier']) AND $_FILES['fichier']['error'] == 0){
	
	// on récupère les information du path
	$info_fichier = pathinfo($_FILES['fichier']['name']);
	
	// on récupère l'extension du fichier
	$ext_fichier = $info_fichier['extension'];
	
	// tableau des extensions autorisés
	$ext_autorisees = array('jpg', 'jpeg', 'gif', 'png');
	
	// teste si le fichier a le bon format 
	if (in_array($ext_fichier, $ext_autorisees)){
	
		//teste si la taille < 1 Mo
		if ($_FILES['fichier']['size'] <= 1000000){
			$fichier_ok = true;
		}else{
			echo 'Erreur : le fichier ne doit pas faire plus de 1 Mo';
		}
	}else{
		echo 'Le fichier n\'est pas une image dans le format autorisé';
	}
}else{
	echo 'Erreur : Le fichier n\'a pas été envoyé';
}

// traitement du fichier si ok 

if($fichier_ok){

	// on récupère le nom temporaire
	$nom_fichier_tmp = $_FILES['fichier']['tmp_name'];
	
	// on récupère le nom du fichier
	$nom_fichier = basename($_FILES['fichier']['name']);
	
	// le fichier sera stocké dans un sous dossier "upload"
	$chemin_fichier = 'uploads/' . $nom_fichier ; 
	
	// on valide le fichier
	move_uploaded_file($nom_fichier_tmp, $chemin_fichier); 
	
	// on confirme
	echo 'fichier envoyé';
}
```

### Gestion des erreurs

indiquer par `$_FILES['monfichier']['error']`

- `UPLOAD_ERR_OK` : succès
- `UPLOAD_ERR_INI_SIZE` : le fichier dépasse la taille max définie dans la config PHP (directive `upload_max_filesize`)
- `UPLOAD_ERR_FORM_SIZE` : le fichier dépasse la taille max définie dans le formulaire HTML
- `UPLOAD_ERR_PARTIAL` : le fichier a été que partiellement chargé
- `UPLOAD_ERR_NO_FILE` : le fichier n’a pas été chargé

### Filtres

Extension `Filter`Permet de valider ou nettoyer des données reçues

### Les principaux filtres

Deux types de filtres :

- `validate` : test la validité. Retourne un booléen
- `sanitize` : nettoyage. Retourne la donnée nettoyée ou `false` si le filtre a échoué

### Filtres de validation

- `FILTER_VALIDATE_EMAIL`
- `FILTER_VALIDATE_URL`
- `FILTER_VALIDATE_IP`
- `FILTER_VALIDATE_MAC`(Adresse MAC)
- `FILTER_VALIDATE_INT`
- `FILTER_VALIDATE_FLOAT`
- `FILTER_VALIDATE_BOOLEAN` : Attention - retourne `null` en cas échec au lieu de `false`

### Filtre de nettoyage

- `FILTER_SANITIZE_STRING` : supprime les balises et encode les caractères `'` et `"`
- `FILTER_SANITIZE_SPECIAL_CHAR`S : encode les caractère spéciaux utilisé en HTML
- `FILTER_SANITIZE_FULL_SPECIAL_CHARS` : applique `htmlentities()`
- `FILTER_SANITIZE_MAIL` : retire tous les caractères interdit dans une adresse mail. Attention : il n’est pas garanti que le résultat retourné soit une adresse valide
- `FILTER_SANITIZE_URL` : idem mais pour une URL
- `FILTER_SANITIZE_NUMBER_INT` : retire tous les caractères qui ne compose pas un nombre entier.
- `FILTER_SANITIZE_NUMBER_FLOAT` : retire tous les caractères qui ne compose pas un nombre flottant
- `FILTER_SANITIZE_ENCODED` : convertie les caractères étendus d’une URL en `%xx`
- `FILTER_SANITIZE_MAGIC_QUOTE`S : applique la fonction `addslashes()`

### Autres

`FILTER_CALLBACK` : Ce filtre ne fait rien par lui-même. Il se contente d’appeler une fonction callback à indiquer en dernier argument et qui sera chargé de faire le traitement

### Utiliser les filtres

### Filtrer les données récupérées

`filter_var(var, filtre, options/indicateur)` : filtrer une donnée

`filter_var_array(array, filtre, options/indicateur)` : filtrer un tableau de données

### Filtrer directement les données utilisateurs

Permet de faire la validation avant la lecture des variables superglobales. On utilise pour cela la source de la donnée (définie par une constante) ainsi que son nom (name)

`filter_input(source, nom, filtre, options/indicateur)`: filtrer une donnée `filter_input_array(source, nom, filtre, options/indicateur)` : filtrer un tableau de données

Source de données :

- `INPUT_GET`
- `INPUT_POST`
- `INPUT_COOKIE`
- `INPUT_REQUEST`
- `INPUT_SESSION`
- `INPUT_EN`
- `INPUT_SERVER`

### Sécurité

Faille XSS (cross-site scripting) : Technique qui consiste à injecter du code HTML contenant du Javascript dans les pages (via l’URL ou un formulaire) pour le faire exécuter

Pour faire un test, indiquer dans un champ :

```html
<script type="text/javascript">alert('bonjour')</script>
```

Si une boite de dialogue apparait, la page est sensible à la faille

Solutions :

- `htmlspecialchars()` : transforme le code HTML et JS en simple texte (le code sera affiché et non pas exécuté). On peut également ajouter en second argument `ENT_QUOTES` pour convertir les apostrophes et guillemets (Nécessaire dans le cas d’un attribut HTML)
- `strip_tags()` : permet de retirer les balises HTML plutôt que de les afficher
- `htmlentities()` : code les les caractères spéciaux HTML
- `addslashes()` : échappe avec un antislashs les apostrophes, guillemets et antislashs

```php
if(empty($_POST['pseudo'])){
	echo 'Erreur : pseudo inconnu';
}else{
	echo 'Bonjour ' . strip_tags($_POST['pseudo']); 
}
```
