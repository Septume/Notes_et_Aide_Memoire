# Sass

Le code SASS est compilé pour pouvoir générer un fichier CSS. Des options sont disponibles lors de la compilation comme la possibilité de minifier le code CSS

Fonctionnalités:

- Imbrication de code
- Variables avec possibilité d'effectuer des opérations arithmétiques.
- Mixins
- Conditions et boucles
- Fonctions

Il existe deux syntaxes :

- **Syntaxe SCSS (Sassy CSS)** : Nouvelle syntaxe plus proche du CSS. Le code CSS déjà écrit est considéré comme du code SCSS valide => fichier .scss
- **Syntaxe SASS (ou syntaxe indenté)** : Ancienne syntaxe qui utilise l’indentation et le retour à la ligne à la place des crochets et du point virgule => fichier .sass . Cette syntaxe est très peu utilisée

## Compilation

Pour compiler un fichier SCSS en CSS

`sass filename.scss filename.css`

Options :

`-- watch` : Permet de générer le fichier CSS à la volée (à chaque modification du code SCSS)

`--style` ou `-t` : Permet de préciser le format de sortie

- `nested` : Défaut. Les règles CSS sont indentés selon l'imbrication du code SCSS. Une déclaration par ligne
- `expanded` : Pas d'indentation des règles. Une déclaration par ligne
- `compact` : Les déclarations de chaque règle sont compactées sur une seule ligne
- `compressed` : Retire tout les espaces et retours à la ligne inutiles. Tout le code se trouve sur une seule ligne ⇒ fichier CSS minifié

## Commentaires scss

### Commentaires silencieux

Commentaires qui ne seront pas inclus dans le fichier CSS lors de la compilation

```scss
// Commmentaire silencieux
```

### Commentaires importants

Commentaires qui ne seront pas supprimés lors de la compilation quelque soit l'option. Utile pour les informations de licence. On utile la syntaxe classique des commentaires CSS en ajoutant un point d'exclamation.

```scss
/*! Commentaire important */
```
