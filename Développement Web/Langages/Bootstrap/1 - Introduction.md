# Introduction

**Différences avec la version 3**

- Abandon des panels, well, thumbnail et glyph icons
- Utilisation de SASS à la place de LESS
- Utilisation d'un fork de Normalize.css
- Utilisation des flexblox à la place des floats
- Taille des polices en rem

**Utilise**

- jQuery (dans sa version slim c’est-à-dire sans les modules ajax et effets)
- poper.js (permet de créer des tooltips)

**Caractéristiques**

- Mobile first ( pas de media queries pour les smartphones en mode portait => valeurs par défaut de Bootstrap)
- `box-sizing : border-box` (présent également dans `bootstrap-reboot.css`)
- Pour les marges verticales, utilise uniquement `margin-bottom`et déconseille l'utilisation de`margin-top` pour éviter les problèmes de fusion des marges.

**Les fichiers**

- `bootstrap.css` : fichier complet contenant toutes règles CSS
- `bootstrap-grid.css` : contient uniquement le code pour le système de grille et les classes utilitaires flexbox
- `bootstrap-reboot.css` : contient uniquement le code du reboot CSS (Fork de normalize.css)
- `bootstrap.js` : code JavaScript des composants (nécessite JQuery et popper.js)
- `bootstrap.bundle.js` : version incluant popper.js

**Exemple de code minimal**

```html
 <!DOCTYPE html>
 <html lang="fr">
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">
     <title>Titre du site</title>
     <link rel="stylesheet" href="bootstrap.min.css">
     <link rel="stylesheet" href="style.css">
 </head>
 <body>
     <!--------- Scripts JS (respecter l'ordre) -------->
     <script src="jquery.slim.min.js"></script>
     <script src="popper.min.js"></script>
     <script src="bootstrap.min.js"></script>
 </body>
 </html>
```
