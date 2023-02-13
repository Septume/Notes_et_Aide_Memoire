# Pattern mvc

**Modèle** : gère le traitement des données (récupération des données, organisation, assemblage…). Contient du code PHP + requêtes SQL. Ne contient pas de code HTML

**Vue** : gère l’affichage des données. Contient essentiellement du code HTML ainsi que du code PHP permettant l’affichage

**contrôleur** : gère la logique en faisant le lien entre le modèle et la vue. Le contrôleur demande au modèle les données, les analyse et décide (ou non) de les envoyer à la vue. Gère les requêtes utilisateurs et les droits d’accès. Contient exclusivement du code PHP. (Pas de requête SQL)

![](mvc.png)

### Créer un template

On utilise des variables dans le template pour les différent éléments comme le titre de la page, le contenu, etc…

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title><?= $title ?></title>
        <link href="style.css" rel="stylesheet" /> 
    </head>
    <body>
        <?= $content ?>
    </body>
</html>
```

Pour utiliser le template on créé les variables et on inclus ensuite le template dans le fichier

```php
<?php $title = 'Mon super site'>
<?php ob_start() ?>
// contenu HTML
<?php $content = ob_get_clean(); ?>
<?php require('template.php') ?>
```

`ob_start()` : enregistre toute la sortie HTML qui suit (balises PHP compris)

`ob_get_clean()` : retourne le contenu enregistré

### Créer un routeur

Il s’agit d’un contrôleur utilisé en amont chargé d’appeler le bon contrôleur en routant les requêtes Le routeur appelle le bon contrôleur, qui récupère des informations depuis le modèle qu’il passe ensuite à la vue

![](mvc_router.png)

Le routeur est en général le fichier `index.php`. On utilise des paramètres dans l’URL pour appeler la bonne page

Par exemple :

- `index.php?action=listPosts` : Affiche la liste des billets d’un blog
- `index.php?action=post&id=1` : Affiche le billet d’id 1

Remarque : il est conseiller de regrouper dans le routeur tous les tests concernant la présence de paramètres dans l’URL

### Organiser les fichiers

Classement par dossier :

- controller : dossier qui contient les contrôleurs.
- view : les vues
- model : les modèles
- public : tous les fichiers statiques publics. Contient les dossiers pour les images, CSS, JS etc…

Regroupement par sections : on regroupe les éléments dans des sous-dossiers en fonction des espaces du site (news, forum, espace membre…)

### Ajouter des fonctionnalités

Étapes :

1. créer le modèle (et créer au besoin des nouvelles tables dans la bd)
2. créer le contrôleur, pour récupérer les informations et les envoyer à la vue
3. créer la vue pour afficher les informations
4. mettre à jour le routeur pour envoyer vers le bon contrôleur
