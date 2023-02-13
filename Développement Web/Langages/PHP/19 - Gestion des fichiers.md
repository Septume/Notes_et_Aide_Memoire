# Gestion des fichiers

Remarque : Pour que PHP (ou tout autre programme) puisse écrire dans un fichier/dossier ce dernier doit avoir un chmod de 777

Sinon on a le message d’erreur : `Warning: fopen(fichier.txt): failed to open stream: Permission denied`

### Les droits

- `r` : lecture seule
- `r+` : lecture/écriture
- `w` : écriture seule. Le fichier est vidé. s’il n'existe pas, il est créé automatiquement
- `w+` : lecture/écriture. Le fichier est vidé. s’il n'existe pas, il est créé automatiquement
- `a` : écriture seule. le texte est ajouté à la fin. Si le fichier n'existe pas il est créé automatiquement
- `a+` : lecture/écriture. le texte est ajouté à la fin. Si le fichier n'existe pas il est créé automatiquement
- `x` : écriture seule avec création du fichier (erreur si le fichier existe déjà)
- `x+` : lecture/écriture avec création du fichier (erreur si le fichier existe déjà)
- `c` : écriture seule. le pointeur est positionné en début de fichier sans qu'il soit vidé. Si le fichier n'existe pas il est créé automatiquement
- `c+` : lecture/écriture seule. le pointeur est positionné en début de fichier sans qu'il soit vidé. Si le fichier n'existe pas il est créé automatiquement

### Ouvrir et fermer un fichier

`fopen(chemin, droits)` : Ouvrir un fichier. Renvoie la référence du fichier ou false en cas d’échec

`fclose(fichier)` : Fermer le fichier.

```php
// ouverture du fichier en lecture/écriture
$fichier = fopen('fichier.txt', 'r+');

// fermeture du fichier
fclose($fichier);
```

### Lire dans un fichier

Remarque : il est conseillé de vérifier que le fichier est bien ouvert avant de le lire

`fgetc(fichier)`: lire le premier caractère

`fgets(fichier)`: lire la première ligne

Pour lire plusieurs caractères/lignes il faut utiliser une boucle

```php
$fichier = fopen('fichier.txt', 'r+'); 

for ($ligne = 1 ; $ligne <= 3 ; $ligne++){
	$texte = fgets($fichier);
	echo $texte . '<br />'; 
} 
fclose($fichier);
```

`fread(fichier)` : lis un le contenu entier du fichier et le retourne dans une chaine de caractères. on peut indiquer comme deuxième argument un entier indiquant la longueur en octet à afficher

### Lecture rapide de fichiers

Permet de lire le fichier sans avoir besoin de l’ouvrir

`file_get_contents('fichier.txt)` : lis le contenu et le retourne dans une chaine de caractère

`readfile('fichier.txt')` : affiche automatiquement le contenu et retourne le nombre de caractère

`file('fichier.txt')` : retourne le contenu dans un tableau ligne par ligne

### Écrire dans un fichier

`fputs(referenceFichier, nouvelleLigne)`

`fwrite()` : alias de `fputs()`

Attention : si on a avant lu une ligne avec `fgets()` le texte sera écrit juste après celle-ci.

La fonction `fseek()` permet d’indiquer où placer le curseur pour écrire dans le fichier :

- pour placer le curseur au début du fichier : `fseek($fichier, 0)`
- pour placer le curseur devant le second caractère : `fseek($fichier, 1)`

Une fois le curseur en début de fichier un `fputs()` va permettre d’écrire la ligne par-dessus l’ancienne

```php
$fichier = fopen('compteur.txt', 'r+');

$pages_vues = fgets($fichier);
$pages_vues += 1;

fseek($fichier, 0);
fputs($fichier, $pages_vues);

fclose($fichier);

echo '<p> Cette page a été vue ' . $pages_vues . ' fois</p>';
```

`ftell($fichier)` : retourne la position du curseur

`rewind($fichier)` : place le curseur en début de fichier (attention : les caractères écrits remplaceront ceux déjà présents)

### Écriture rapide

`file_put_contents('fichier.text', 'contenu')`

Le contenu du fichier sera effacé

### Gérer l’accès concurrent

`flock($fichier, type)` : permet de verrouiller le fichier. Prend en arguments la référence du fichier et le type de verrouillage

Les types de verrous :

- LOCK_SH : verrou partagé (lecture)
- LOCK_EX : verrou exclusif (écriture)
- LOCK_UN : pour libérer un verrou

### Manipulation de fichiers

`copy('fichierSource.txt', 'fichierDestination.txt')` : permet de copier un fichier

`rename('fichier.txt', 'fichier2.txt')` : permet de renommer un fichier. Génère une erreur si le fichier n’existe pas

`file_exists()` : permet de tester l’existence d’un fichier ou d’un dossier (à indiquer en argument)

`is_file('fichier.txt')` : teste l’existence d’un fichier (ne fonctionne pas avec les dossiers)

`is_executable('fichier.txt')` : teste si le fichier est exécutable

`touch('fichier.txt')` : créé un fichier. Si le fichier existe déjà, cela change uniquement sa date de modification

`unlink('fichier.txt')` : supprime le fichier. Génère une erreur si le fichier n’existe pas

`filesize('fichier.txt')` : retourne la taille du fichier en octets

### Manipulation de répertoire

`dir("/chemin/du/repertoire")` : retourne un objet de la classe Directory contenant la référence vers le répertoire indiqué en argument

on peut utiliser sur l’objet les propriétés :

- `handle` : la référence du répertoire
- `path` : le chemin du répertoire

`is_dir("/chemin/du/repertoire")`: permet de tester l’existence d’un répertoire

`opendir("/chemin/du/repertoire")` : ouvre un répertoire. Retourne un objet Directory `readdir($repertoire)` : lis le contenu d’un répertoire

```php
$rep = opendir("/laragon/www/tests/test");
while ($fichier = readdir($rep)) {
	// tant qu'il y a encore des fichiers à la lire
	echo $fichier  . '<br>';  
}
```

`glob(masque)` : retourne un tableau contenant les fichiers d’un répertoire selon un masque donné

```php
// tous les fichiers .txt du dossier courant
$fichiers = glob('./*.txt');
```

`getcwd()` : retourne le répertoire courant

`chdir("/chemin/du/repertoire")` : se déplacer dans un répertoire

`mkdir("/chemin/du/repertoire")` : créer un répertoire

`rmdir("/chemin/du/repertoire")` : supprimer un répertoire

`dirname()` : retourne le chemin parent d’un répertoire
