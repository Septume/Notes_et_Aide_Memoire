# Jekyll

## Créer un projet Jekyll

```
jekyll new project-folder-name
cd project-folder-name
bundle add webrick
bundle exec jekyll serve --livereload
```

Le site se trouve à l'adresse : `http://localhost:4000`

## Structure de base

- `_posts/` : articles de blog
- `_site/`: fichiers du site une fois généré
	- `assets/` : fichiers CSS et JS, images
- `_config.yml` : fichier de configuration du projet
- `Gemfile` : fichier de configuration des extensions

Autres dossiers

- `_data`: fichiers de données
- `_drafts`: brouillons non publiés
- `_layouts`
- `_includes` : extrait de code HTML à inclure
