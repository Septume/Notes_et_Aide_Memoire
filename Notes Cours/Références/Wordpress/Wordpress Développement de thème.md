# Wordpress : développement de thème

## Fonctionnement d’un thème

### Structure d’un thème

**Fichiers de base**

- `index.php` : page de démarrage. Obligatoire
- `style.css` : Obligatoire

Les commentaires du style.css permet d’indiquer les informations sur le thème qui sera affichés par Wordpress.

Exemple :

```css
/*
Theme Name: nom du thème
Theme URI: http://www.site.tld
Author: Machin Bidule
Author URI: http://www.site.tld
Description: description du thème
Version: 1.0
Tags: simple, menu, widget
*/
```

- `screenshot.png` : miniature du thème. La taille doit être 300x225px
- `functions.php` : pour définir les fonctions pouvant être utilisées dans tous les fichiers du thème. Son inclusion est fait automatiquement par Wordpress s’il est présent dans le dossier du thème courant. Facultatif
- `header.php` : Contient le contenu de l’élément `head` ainsi que le début de l’élément `body` commun à toutes les pages. Ce fichiers est appelé par les autres à l’aide de la fonction d’inclusion `get_header()`
- `footer.php` : Contient la fin de l’élément `body` commun à toutes les pages ainsi que les balises de fermeture `body` et `html`. Ce fichiers est appelé par les autres à l’aide de la fonction d’inclusion `get_footer()`
- `sidebar.php` : barre latérale des widgets. Ce fichiers est appelé par les autres à l’aide de la fonction d’inclusion `get_sidebar()`

**Autres fichiers**

- `home.php` : utilisé pour la page d’accueil du site et listant les derniers articles
- `front-page.php` : utilisé lorsqu’on veut afficher une page statique comme page d’accueil plutôt que les derniers articles (à paramétrer dans *réglages -> lecture -> la page d’accueil affiche -> une page statique*)
- `single.php` : affiche un article seul
- `page.php` : affiche une page seule
- `search.php` : affiche la liste des résultats d’une recherche
- `archive.php` : affiche la liste des articles archivés
- `404.php` : affiche la page erreur 404
- `author.php` : affiche la liste des articles correspondants à un auteur
- `date.php` : affiche la liste des articles correspondants à une date
- `tag.php` : affiche la liste des articles correspondants à un tag
- `category.php` : affiche la liste des articles correspondants à une catégorie
- `comments.php` : liste des commentaires associés à un article ainsi que le formulaire pour laisser un commentaire. Ce fichiers est appelé par les autres à l’aide de la fonction d’inclusion `comments_template()`
- `searchform.php` : formulaire de recherche. Ce fichiers est appelé par les autres à l’aide de la fonction d’inclusion `get_searchform()`
- `attachement.php` : pour afficher les médias attachés à un article (comme les images)
- `image.php` : affiche la page unique d’une image

On peut utiliser des fonctions qui permet de tester si la page actuelle correspond à un type de page particulier

- `is_home()`
- `is_frontpage(`
- `is_404()`
- `is_search()`
- `is_archive()`
- `is_paged()` : pour une page paginée.

Peut prendre comme argument l’ ID, le nom ou le permalien

- `is_single()`
- `is_page()`
- `is_category()`
- `is_tag()`
- `is_author()`

### Dossiers

Ces dossiers peuvent éventuellement être présents à la racine d’un thème

- `template-parts` : contient tous les fichiers permettant d’afficher le contenu d’une page
- `Genericons` : bibliothèque gratuite d’icônes vectorielles basé sur des polices de caractères utilisée par Wordpress (<http://genericons.com/)>
- `languages` : contient les langues du thème
- `css` ou `style` : contient les CSS du thème
- `js` ou `javascript` : script JS
- `fonts`
- `images` ou `img`
- `pages-templates` : contient les templates de page
- `inc` ou `includes` : contient les fichiers PHP propre au thème

### Fonctions d’inclusion

- `get_header()` : Appelle le fichier `header.php`
- `get_footer()` : Appelle le fichier `footer.php`
- `get_sidebar()` : Appelle le fichier `sidebar.php`
- `get_searchform()` : Appelle le fichier `searchform.php`
- `comments_template()` : Appelle le fichier `comments.php`

`get_template_part()` : permet d’inclure un sous-template dans plusieurs autres templates

- `get_template_part($slug)` : pour inclure un fichier ​`$slug.php`
- `get_template_part($slug,$name)`: pour inclure un fichier ​`$slug-$name.php`

Exemple

```php
/* inclure le fichier template-parts/content-page.php */
get_template_part('template-parts/content', $page)
```

`get_template_part('content' get_post_format())` : pour inclure le fichier `content-$format.php`

où `$format` correspond à un format d’article. La fonction `get_post_format()` permet de récupérer le nom du format. Par exemple, si *Audio* est sélectionné comme format d’article (bloc `Format`) la fonction `get_template_part()` fait appel au fichier `content-audio.php`

On peut également appelé le fichier `content-audio.php` en utilisant la forme `get_template_part('content', 'audio')`

Remarque : les posts format doivent être activés dans le fichier `function.php`, leur utilisation peuvent être différente d’un thème à l’autre

### Hiérarchie des templates

Les templates permettent d’afficher le contenu en fonction du type de page demandée

![Wordpress%20De%CC%81veloppement%20de%20the%CC%80me%20fe2054135b6541868a3fb6b5101f159b/wp-hierarchy.png](Wordpress%20De%CC%81veloppement%20de%20the%CC%80me%20fe2054135b6541868a3fb6b5101f159b/wp-hierarchy.png)

Liens :

- [Documentation Wordpress.org](https://developer.wordpress.org/themes/basics/template-hierarchy/)
- [wphierarchy.com](https://wphierarchy.com/)

La hiérarchie se lit de gauche à droite

Exemple de fonctionnement pour un template de type `Author` :

- Si il existe, Wordpress utilise le fichier : `author-{nicename}.php`
- Sinon : `author-{id}.php`
- Sinon : `author.php`
- Sinon : `archive.php`
- En dernier recours : `index.php`

Extension utile : [What The File](https://fr.wordpress.org/plugins/what-the-file/) (permet d’afficher dans la toolbar le template utilisé par la page en cours)

### Thème enfant

On créé un thème enfant à partir d’un thème déjà existant.

Cela permet notamment de personnaliser le style d’un thème existant sans devoir modifier directement son fichier style.css (=> recommandé)

```css
/*Theme Name: Template: theme_parent*/
```

Attention : La directive template doit indiquer exactement le nom du dossier du thème parent

Le fichier `style.css` n’est pas pris en compte dans l’héritage du thème. Il est toutefois possible d’importer le style du thème parent avec la directive `@import` à placer dans le fichier `style.css` du thème enfant

```css
@import url("../twentysixteen/style.css");
```

`functions.php` : celui du thème parent est utilisé dans le thème enfant. La création d’un fichier `function.php` dans le thème enfant permet de rajouter des nouvelles fonctions sans écraser celles du parent

Surcharge de fichiers : consiste à copier un fichier du thème parent dans le dossier du thème enfant afin d’en modifier le contenu.

### Traduction du thème

Il est possible d’insérer du texte brut dans les fichiers templates mais les caractères spéciaux et accentués ne sont pas pris en compte, à moins de faire un encodage du texte en UTF-8

On peut toutefois utiliser des fonctions spécifiques de Wordpress qui ont l’avantage de pouvoir gérer le multilingue

`__($text, $domain)` : Retourne une chaine à traduire indiquer en argument. En 2ème argument il faut indiquer le nom clé du fichier où se trouve les chaines de traduction (un fichier *.po*)

Ex : `__('Nothing Found', 'twentytwelve')`

`_e($text, $domain`) : affiche le texte traduit ce qui revient à faire un `echo __()`

### Starter themes

Thèmes neutres et minimalistes, servant de base pour créer son propre de thème

- Underscores : Starter Theme officiel de Wordpress
- Genesis Framework
- FoundationPress

## Créer son thème

### Post format

Modèle d’article

`content.php` : format par défaut

`content-aside.php` : format En passant (billet cours sans titre)

`content-link.php` : format Lien

`content-gallery.php` : format Galerie

`content-quote.php` : format Citation

`content-image.php` : format Image (image unique)

`content-video.php` : format Video content-audio.php : format Audio

La déclaration des formats d’articles se fait dans le fichier `function.php`

```php
add_theme_support( 'post-formats', array( 
	'aside', 
	'link', 
	'gallery', 
	'quote', 
	'image', 
	'video', 
	'audio' 
) );
```

### Hooks

Deux types de hooks :

- les actions : permet d’appeler des fonctions Wordpress lors d’un évènement. Plusieurs fonctions peuvent écouter le même évènement.  
Exemple d’évènement : `save_post` => sauvegarde d’un article
- les filtres : permet de modifier les fonctions existantes de Wordpress

### Actions

Pour créer une action :

`add_action('nom_evenement', 'nom_fonction', prioriete)`

L’argument concernant la priorité est facultatif. Celle-ci est représentée par un nombre (par défaut : 10). Plus le nombre est faible plus la priorité est haute

```php
add_action('save_post', 'ma_fonction', 20);
```

Pour appeler les actions liées à un évènement

`do_action('nom_evenement', args…);`

En plus du nom de l’évènement on indique les éventuels arguments à passer aux actions exécutées

```php
do_action('save_post', $post->ID, $post)
```

### Quelques actions

`after_setup_theme` : après le chargement du fichier `function.php`. Utilisé pour les arguments et les options du thème.

`init` : après que Wordpress est fini de se charger mais avant que les header soit envoyé. Utilisé pour l’initialisation des extensions ou l’interception des variable `$_POST` et `$_GET`

`widget_init` : pour initialisation des widget

`wp_loaded` : Wordpress a fini de charger toutes les extensions et le thème

`wp` : quand l’objet `$wp` est initialisé. Utilisé pour filter ou valider certaines requête

`after_switch_theme` : après un changement de thème

`template_redirect` : avant que Wordpress détermine la page à chargé. Utilisé pour faire une redirection

### Templates tags

Ensembles de fonctions conçues pour être appelées dans les fichiers d’un thème afin de récupérer ou afficher le contenu.

`bloginfo()` : Affiche des Informations sur la configuration du site en fonction de l’argument utilisé

- `bloginfo('name')` : titre du site (*Réglages -Général - Titre du site*)
- `bloginfo('description')` : slogan du site (*Réglages - Général - Slogan*)
- `bloginfo('url')` : URL du site (*Réglages - Général - Adresse Web du site*)
- `bloginfo('wurl')` : URL de wordpress (*Réglages - Général - Adresse Web de Wordress*)
- `bloginfo('admin_mail)` : adresse mail de contact du site (*Réglages - Général - Adresse de messagerie*)
- `bloginfo('charset')` : encodage de caractère utilisé sur le site
- `bloginfo('stylesheet-url')` : chemin d’accès du fichier style.css
- `bloginfo('template-url')` : chemin d’accès au dossier racine du thème actif
- `bloginfo('language')` : langue du site (indiquer dans le fichier *wp-config.php*)
- `bloginfo('stylesheet_url)` : URL du fichier *style.css* du thème actif. Revient à faire un echo de la fonction `get_stylesheet_uri()`
- `bloginfo('stylesheet_directory')` : URL du dossier du fichier *style.css* du thème actif. Revient à faire un echo de la fonction `get_stylesheet_directory_uri()`
- `bloginfo('template_url')` ou `bloginfo('template_directory')`: URL du thème actif ou du dossier du thème parent. Revient à faire un echo de `get_template_directory_uri()`
- `bloginfo('atom_url')`: URL du flux Atom
- `bloginfo('rss_url')`: URL du flux RSS
- `bloginfo('rdf_url')` : URL du flux RDF
- `bloginfo('rss2_url')`: URL du flux RSS 2.0
- `bloginfo('comments_atom_url')`: URL du flux Atom des commentaires
- `bloginfo('comments_rss2_url')` : URL du flux RSS 2.0 des commentaires

`get_bloginfo()` : renvoie les données au lieu de les afficher

`wp_title()` : titre de la page (balise `<title>`)

`the_post()` : un article

`the_title()` : titre d’un article

`the_content()` : contenu d’un article

`the_author()` : auteur d’un article

`the_date()` : date de l’article

`comments_template()` : commentaires

`comment_form()` : formulaire pour ajouter un commentaire

`get_template_directory_uri()` : chemin vers le dossier du thème. Nécessaire pour lier les ressources (CSS, JS, images…)

[Listes des templates tags](https://codex.wordpress.org/Template_tags)

### Boucle de rendu (the loop)

Utilisation d’une boucle while qui permet de récupérer le contenu des articles et pages. La condition `have_posts()` teste s’il reste des articles à afficher. La boucle continue tant que la fonction renvoie `true` . La fonction `the_post()` récupère le contenu d’un article ou d’une page

```php
<?php
while (have_posts()) :
	the_post(); // récupère un article
	/* Fonctions pour afficher le contenu */
endwhile; ?>
```

En général la boucle contient des fonctions d’affichage du contenu, des fonctions de récupération de variables ou des fonctions d’inclusion de fichiers.

### Principales fonctions d’affichage

Ces fonctions affichent directement le résultat. Elles commencent généralement par le préfixe `the_`

`the_ID()` : l’ ID de l’article ou la page

`the_title($before, $after, $bool)` : La fonction peut recevoir des arguments facultatifs pour permettre d’afficher du texte avant ou après le titre (en général du code HTML comme `<h1>`). En 3ème argument on indique un booléen pour permettre l’affichage (par défaut `true`)

`the_content($more, $aftermore)` : Affiche le contenu d’un article ou d’une page. 2 arguments facultatifs. Le premier est le texte d’affichage pour le lien permettant de voir la suite du contenu. Le deuxième est un booléen pour permettre l’affichage du texte `$more`. Par défaut `false`

`the_excerpt()` : l’extrait d’un article ou d’une page si le bloc *Extrait* est renseigné

`the_permalink()` : affiche l’URL de l’article/page

`the_post_thumbnails($size, $arguments)` : L’image à la une. S’utilise avec la fonction `have_post_thumbnails()`qui permet de tester la présence d’une image. Peut prendre deux arguments :

- `$size` : le format (thumbnail, medium, large ou full)
- `$arguments` : tableau indiquant les paramètres de largeur, hauteur etc…

Pour utiliser cette fonction il faut la déclarer dans le fichier `functions.php` à l’aide d’un hook

`add_theme_support('post-thumbnails)`

`the_author()` : nom de l’auteur sous la forme d’un lien vers son profil

`the_time()` : date de publication. Peut prendre en argument un format de date PHP. Par défaut c’est le format paramétré dans le menu *Réglages -> Général -> Format de date*

`the_category($separator)` : liste des catégories d’un article/page avec lien vers la page qui liste tous les articles/pages de la catégorie. Peut prendre deux arguments :

- `$separator` : chaine de caractère à afficher entre les liens
- `$parents` : affiche la relation parent/enfant. Deux valeurs : multiple ou single

`the_tags($before, $separator, $after)` : liste des tags avec lien vers la page du tag.

- `$before` : chaine de caractère à afficher avant la liste. Par défaut : “tags:”
- `$separator` : chaine à afficher entre les liens. Par défaut une virgule
- `$after` : chaine à afficher après la liste.

`edit_post_link($name, $before, $after)` : affiche le lien vers la page d’administration de l’article/page

- `$name` : titre du lien (par défaut : *Éditer*)
- `$before` : texte avant. En général une balise HTML
- `$after` : texte après. En général la balise de fermeture HTML

`wp_link_pages($arguments)` : affiche les liens vers les pages précédentes et suivantes. Prend en argument un tableau associatif pour indiquer les différents paramètres

- `before` : texte HTML avant le premier lien.
- `after` : texte HTML après le dernier lien
- `link_before` : texte HTML avant le lien
- `link_after` : texte HTML après le lien
- `next_or_number` : indique le numéro des pages ou un texte. Deux valeurs : `next` ou `number`
- `separator` : caractères s’affichant entre les liens
- `nextpagelink` : texte du lien vers la page suivante
- `previouspagelink` : texte du lien vers la page précédente
- `pagelink` : format de chaine de pour le numéro de page. % doit être utilisé pour indiquer le numéro. (ex : Page %)
- `echo` : booléen indiquant s’il y a affichage. Par défaut `true`

Par défaut :

```php
	wp_link_pages(
	'before'            => '<p>' . __( 'Pages:'),
	'after' 			      => '</p>',
	'link_before'		    => '',
	'link_after'    	  => '',
	'next_or_number' 	  => 'number',
	'separator'    		  => ' ',
	'nextpagelink'   	  => __( 'Next page'),
	'previouspagelink' 	=> __( 'Previous page'),
	'pagelink'     		  => '%',
	'echo'       		    => 1
);
```

Exemple

```php
	while (have_posts()) :
	the_post(); // récupère un article
	the_title(); // affiche le titre de l'article
	the_content(); // affiche le contenu
	the_author(); // affiche l'auteur
endwhile; ?>
```

### Principale fonctions de récupération de variables

Commence en général par `get_` nécessitent la fonction echo pour afficher le résultat. La récupération des variables est surtout utilisée pour la création de ses propres fonctions

`get_the_id()`

`get_the_title($id)` : Peut prendre en argument un id ou sinon retourne le titre de l’article courant

`get_the_content($more, $aftermore)`

`get_the_excerpt()`

`get_the_permalink($id)`

`get_the_post_thumbnails($id, $size, $arguments)`: peut prendre en argument l’ ID d’un article/page

`get_the_author()`

`get_the_time($d, $id)`

`get_the_category($id)`

`get_the_tags($id)`

`get_edit_post_link($name, $before, $after, $id)`

### Classes wordpress

`WP_Roles` : gestion des rôles

`WP_USer` : gérer les rôles attribués aux utilisateurs

`WP_Post` : récupération des infos d’un article/page

`WP_Query` : requêtes sur les infos d’une article/page

`wpdb` : interaction avec la base de donnée

`WP_Widget` : gestion des widgets

`WP_Rewrite` : gestion des règles de réécritures pour les permaliens

`WP_Object_Cache` : mise en cache des résultats de requête

Beaucoup de fonctions Wordpress comme `have_posts()` utilise la classe `WP_Query`

### Menus

La fonction `wp_nav_menu($args)` permet d’afficher n’importe quel menu créé dans `Apparence -> Menus`. Elle applique automatiquement des classes CSS prédéfinies. Elle prend en argument un tableau associatif pour indiquer les différents arguments.

`theme_location` : emplacement du menu. Ce dernier est indiqué dans *Apparence -> Menus -> Gérer les emplacements*

`menu` : nom ou ID d’un menu. L’emplacement doit au préalable être défini avec la fonction `register_nav_menus()`

`container` : nom de la balise HTML contenant le menu. Par défaut `div`. Il faut indiquer `false` pour avoir aucune balise

`container_id` : nom d’ID pour la balise HTML contenant le menu

`menu_class` : nom de class de la balise `<ul>` du menu

`menu_id` : nom d’ ID de la balise `<ul>` du menu

`echo` : booléen indiquant si on veut afficher le menu ou juste le récupérer dans une variable. Par défaut `true`

`fallback_cb` : un nom retourné si le menu n’existe pas. Par défaut `wp_page_menu`. Il faut indiquer `false` pour désactiver ce paramètre

`before` : Texte à afficher avant chaque balise `<a>` du menu

`after` : Texte à afficher après chaque balise `<a>` du menu

`link_before` : Texte à afficher avant le texte du lien

`link_after` : texte à afficher après le texte du lien

`items_wrap` : chaine contenant des variables pour la personnalisation des liens

`depth` : niveau de menu.

`walker` : accepte un objet pour personnaliser le menu

`items_wrap` => variables pour créer une chaine (format `sprintf()`)

`%1$s` =>argument menu_id

`%2$s` => argument menu_class

`%3$s` => valeur de la balise HTML `<li>` contenant le lien de l’onglet

Par défaut :

```html
<ul id="%1$s" class="%2$s">%3$s</ul>
```

Exemple

`'items_wrap' => '%3$s'`

=> dans ce cas seule la liste avec les balises `<li>` sans les balises `<ul>` s’affiche . Il faut donc ajouter les balises `<ul>` dans le fichier appelant la fonction

Niveau :

0 : affiche tout le menu

1 : désactive tous les sous-menu à partir du niveau 1

2 : désactive tous les sous-menu à partir du niveau 2

- 1 : affiche tous les onglets au même niveau

### Fonctions pour les url

Ces fonctions retournent une adresse URL sous la forme d’une variable

`get_template_directory_uri()` : le dossier du thème parent dans le cas d’un thème enfant sinon celui du thème actif

`get_stylesheet_directory_uri()` : le dossier du fichier style.css du thème actif

`site_url()` : adresse du site

`home_url()` : racine de Wordpress

`admin_url()` : administration

`includes_url()` : dossier `wp-includes`

`content_url()` : dossier `content`

`plugins_url()` : dossier `plugins`

`theme_url()` : dossier `theme`

`wp_upload_dir()` : dossier `uploads`

### Shortcodes

balises de code entre crochet permettant d’insérer des fonctionnalités dans un article ou une page (galerie image, cartes interactives, etc…)

`[nom_du_shortcode]`

Il est possible d’utiliser des paramètres :

`[nom_du_shortcode attribut1="valeur1" attribut2="valeur2"]`

Un shortcode peut avoir du texte comme contenu. Dans ce cas on utilise une balise ouvrante et fermante

`[nom_du_shortcode]Contenu du shortcode[/nom_du_shortcode]`

Exemple :

`[ gallery columns="2" size="medium" ]`

=> insère une galerie d’image sur 2 colonnes en taille moyenne

Quelques shortcodes prédéfinies

- `[audio]`
- `[video]`
- `[caption]` : description
- `[embed]` : intégration de contenu en utilisant la balise HTML `embed`

Créer des shortcodes ;

`add_shortcode($nom, $fonction) :`

```php
function helloword_shortcode() {
	echo 'Hello World !'; 
}
add_shortcode('HelloWord' , 'helloword_shortcode')
/* pour utiliser le shortcode : [HelloWord] */
```
