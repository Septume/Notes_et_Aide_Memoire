# Wordpress : starter theme underscores

[Site du projet](http://underscores.me/)

[Github du projet](https://github.com/automattic/_s)

## Mise en place du thème

### Configuration

Avant le téléchargement il faut indiquer un nom pour le thème. On peut également, dans les paramètres avancés, indiquer un nom de slug (sans espace, caractères accentués, etc…) qui sera utilisé comme préfixe dans certaines fonctions personnalisées (Si le slug n’est pas indiqué il sera automatiquement créé à partir du nom donné au thème)

### Les fichiers et dossier du thème

- `functions.php`
- `index.php`
- `header.php`
- `footer.php`
- `page.php` (template des pages)
- `single.php` (template des articles)
- `archive.php` (archives par mois, catégories, tags…)
- `comments.php`
- `search.php`
- `sidebar.php`
- `404.php`
- `style.css`
- `rtl.css` (feuille de style pour l’affichage du texte de droite à gauche)
- `screenshot.png`

`inc` : dossier contenant des fichiers inclus pour la personnalisation du thème

- `custom-header.php`: personnalisation du header
- `customizer.php` : pour paramétrer l’interface d’administration du thème
- `template-functions.php` : tweaks pour la personnalisation du thème
- `template-tags.php` : contient les templates tags personnalisés
- `jetpack.php` : fonctions de personnalisation du plugin JetPack

`js` :

- `customizer.js` : fonctions JS pour optimiser le paramétrage de personnalisation
- `navigation.js` : permet d’avoir une barre de menu responsive
- `skip-link-focus-fix.js` : fonctions dédié à l’accessibilité

`languages` : contient un fichier `.pot` pour permettre la traduction du thème

`layouts` : contient les fichiers css de mise en page pour la sidebar

- `content-sidebar.css` : CSS pour la sidebar de droite
- `sidebar-content.css` : CSS pour la sidebar de gauche

`template-parts` : contient les templates pour afficher les contenus

- `content.php` : contenu de type article
- `content-page.php` : contenu de type pages
- `content-search.php` : contenu des résultats de recherche
- `content-none.php` : pages sans contenu

### Traduction

Le thème est en anglais. Pour le traduire en français il faut utiliser le fichier *.pot* pour créer une traduction avec un logiciel comme Poedit :

- Copier le fichier *pot* et le renommer en `fr-FR.po`
- Ouvrir le fichier avec Poedit
- Régler les propriétés de traduction (*Catalogue -> Propriétés* )
- Faire les traduction et enregistrer. Un fichier `fr-FR.mo` sera généré pour être utilisé par Wordpress

Remarque : les chaines de caractères du code pouvant être traduites sont préfixées par deux underscores

Exemple : `printf( esc_html__( 'Proudly powered by %s', 'perso' ), 'WordPress' );`

### Fichier style.css

Utilise :

- `box-sizing: border-box`
- Normalize
- Des propriétés permettant l’accessibilité

### Structure html

![](wordpress_underscores_structure.png)

## Personnalisation du thème

### Header

Fichier header.php

Comportement :

- Sur les page `home.php` (page d’accueil du mode blog) et `front-page.php` (page d’accueil du mode site) le titre du site est affiché dans une balise `h1`. Pour les autres pages, le titre est affiché dans une balise `p`
- Le slogan est affiché dans une balise `p`

### Activer le custom header

[Documentation des Custom Headers](https://codex.wordpress.org/Custom_Headers)

Permet de personnaliser l’image de fond du header via l’ outil Customizer (interface de personnalisation de thème)

Ajouter dans le fichier `functions.php`:

`add_theme_support( 'custom-header' );`

Le fichier `inc/custom-header.php` du thème contient les paramètres de personnalisation du Custom Header

```php
add_theme_support( 'custom-header', apply_filters( 'mon_theme_custom_header_args', array(
	'default-image'          => '',
	'default-text-color'     => '000000',
	'width'                  => 1000,
	'height'                 => 250,
	'flex-height'            => true,
	'wp-head-callback'       => 'mon_theme_header_style',
) ) );
```

Il faut ensuite modifier le fichier `header.php` pour ajouter le code qui récupéra l’image du header pour l’afficher

```php
<?php if(get_header_image()) ?>
	<header id="masthead" class="site-header" style="background-image:url(<?php header_image()?>)">
<?php } else { ?>
	<header id="masthead" class="site-header">
<?php } ?>
```

### Page de démarrage index.php

![](wordpress_underscores_index.png)

### Fichier template-parts/content.php

Si l’article est affiché en page seule le titre est de niveau `h1`, Sinon il de niveau `h2`

Fonctions Underscores :

- `nom_theme_posted_on()` : Affiche la date de publication
- `nom_theme_posted_by()` : Affiche l’auteur
- `nom_theme_entry_footer()` : Affiche les categories/tags de l’article

=> Ces fonctions ont été définies dans le fichier `inc/template-tags.php`

**Nom fonction**

`nom_theme_posted_on()`

`nom_theme_posted_by()`

**Variable pour affichage avec echo**

`$posted_on`

`$byline`

**Classe CSS utilisée**

`posted-on`

`byline`

Fonctions Wordpress

- `the_content()` : affiche le contenu
- `wp_link_pages()` : affiche les liens des articles paginées

### Image à la une

Le fichier `functions.php` contient la fonction `add_theme_support( 'post-thumbnails' )` qui permet de prendre en charge l’image à la une. Par défaut l’image s’affiche dans sa taille d’origine. Pour changer utiliser la fonction Wordpress `set_post_thumbnail_size(largeur,hauteur)` Par exemple : `set_post_thumbnail_size(600,250`) . Une des deux dimensions sera utilisé en fonction de l’orientation de l’image

L’affichage de l’image est gérer dans le fichier `template-parts/content.php` avec la fonction `nom_theme_post_thumbnail()`

### Affichage des extraits

```php
<?php
if (is_home() && has_excerpt( $post->ID ) ) : 
    echo ('<div class="excerpt">'.get_the_excerpt().'<div>');
endif; 
?>
```

### Page single.php

![](wordpress_underscores_single.png)

### Personnaliser la navigation

La navigation est gérer par la fonction `the_post_navigation()`

On peut indiquer en argument un array indiquant des options

Par exemple : pour personnaliser les libellés des liens

```php
the_post_navigation(
    array(
        'prev_text' => '<span>Article précédent : %title<span>',
        'next_text' => '<span>Article suivant : %title<span>'
    )
};
```

### Menu de navigation

Le thème propose un seul emplacement de menu (avec pour nom Primary)

Le code se trouve dans le fichier `functions.php`

```php
register_nav_menus( array(
	'menu-1' => esc_html__( 'Primary', 'nom-theme' ),
) );
```

Le menu est affiché dans le template `header.php`

```php
wp_nav_menu( array(
	'theme_location' => 'menu-1',
	'menu_id'        => 'primary-menu',
) );
```
