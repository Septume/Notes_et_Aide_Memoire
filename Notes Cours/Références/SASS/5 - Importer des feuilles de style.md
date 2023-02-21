# Importer des feuilles de style

Lorsqu'on utilise la directive `@import` le navigateur doit faire plusieurs requêtes pour pouvoir charger toutes les feuilles de style importées, ce qui peut créer des problèmes de performances.

SASS permet de modifier le comportement de `@import`

### Feuille de styles partielle (partial)

Il s'agit de fichiers dont le nom commence par un underscore et qui ne seront pas générés dans un nouveau fichier CSS lors de la compilation.

L'import d'un partial doit se faire sans la fonction `url()` ce qui permet d'indiquer à SASS que le contenu des fichiers importés doit être incorporé dans le fichier principal (Dans le cas contre les instructions d'import resteront dans le fichier et le contenu ne sera pas incorporé)

Remarque : Pour le nom des fichiers à importer, il est possible d'utiliser une écriture raccourcie en omettant l'underscore et l'extension de fichier

```scss

@import 'partials/reset'; 
@import 'partials/config';
@import 'partials/style';
```

### Importation imbriquée

Avec SASS il est possible d'utiliser l'instruction `@import` à l'intérieur d'une règle CSS

Remarque :

- Si on utilise le selecteur `&` dans le partial, ce dernier correspondra bien au sélecteur dans lequel le partial a été importé.
- Les variables globales du partial auront une portée réduite au contexte local de la règle qui importe le fichier
- Cette fonctionnalité reste limitée par le fait qu'il n'est pas possible de déclarer des propriétés en dehors d'une règle CSS, y compris dans les fichier partials

```scss
/* fichier partial _info.scss */
&.info {
	// code B
}

/* fichier principal */

.content {
	// code A
	@import 'info';
}

/* fichier CSS généré */

.content {
	// code A
}

.content.info {
	// code B
}
```

### Variable par défaut

L'importation peut entrainer comme effet de bord l'écrassement des valeurs des variables donc le nom est identique.

```scss
/*fichier _theme.scss */
$alert-color: yellow; 

/* fichier main.scss */ 
$alert-color: red; 
@import 'theme';
.alert {
	color: $alert-color; 
}

/* css généré */ 

.alert {
	color: yellow; 
}
```

Si on déclare une variable avec le mot clé `!default` la valeur ne sera pas écrasée si la variable existe déjà.

```scss
/*fichier _theme.scss */
$alert-color: yellow !default; 

/* fichier main.scss */ 
$alert-color: red; 
@import 'theme';
.alert {
	color: $alert-color; 
}

/* css généré */ 

.alert {
	color: red; 
}
```
