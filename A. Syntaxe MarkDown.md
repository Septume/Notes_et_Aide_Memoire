## Histoire

MarkDown est un petit projet lancé en 2004 par le bloggeur [John Gruber](https://fr.wikipedia.org/wiki/John_Gruber). C’est une syntaxe minimale permettant d’écrire du texte pour le web, puis de le convertir en HTML.

Elle a été adoptée par des sites comme StackOverflow, Github (pour la rédaction de commentaires, ou dans le README). Depuis 2016, WordPress.com permet d’écrire en MarkDown.


# [La syntaxe markdown](https://docs.framasoft.org/fr/grav/markdown.html#styles-de-texte)

Pour formater votre texte vous avez la possibilité d'utiliser la barre d'outils située au-dessus de la zone de texte, ou vous pouvez utiliser la syntaxe markdown.

## Styles de texte

Vous pouvez utiliser `_` ou `*` autour d'un mot pour le mettre en italique. Mettez-en deux pour le mettre en gras.

-   `_italique_` s'affiche ainsi : _italique_
-   `**gras**` s'affiche ainsi : **gras**
-   `**_gras-italique_**` s'affiche ainsi : **_gras-italique_**
-   `~~barré~~` s'affiche ainsi : ~~barré~~
-   `<u>souligner</u>` s'affiche ainsi : <u>souligner</u>

## Blocs de code

Créez un bloc de code en indentant chaque ligne avec quatre espaces, ou en mettant trois accents graves sur la ligne au dessus et en dessous de votre code. Exemple :

` ```bloc de code``` ` 

s'affiche ainsi :

```
bloc de code
```

## Liens

Créez un lien intégré en mettant le texte désiré entre crochets et le lien associé entre parenthèses.

`Aidez-vous avec [la documentation de Framasite](https://docs.framasoft.org/fr/grav/) !`

s'affichera :

Aidez-vous avec [la documentation de Framasite](https://docs.framasoft.org/fr/grav/) !

Vous pouvez ajouter aux liens des attributs `id` et `class` de cette manière :

```
[la documentation de Framasite](https://docs.framasoft.org/fr/grav/){#id .class1 .class2}
```

Les liens peuvent ainsi être mis sous forme de boutons à l’aide des classes CSS de Bootstrap :

Default Primary Success Info Warning Danger Link

```
[Default](#){.btn .btn-default}
[Primary](#){.btn .btn-primary}
[Info](#){.btn .btn-info}
[Success](#){.btn .btn-success}
[Warning](#){.btn .btn-warning}
[Danger](#){.btn .btn-danger}
[Link](#){.btn .btn-link}
```

Dans les modules et autres composants du thème GravStrap, [la syntaxe est plus détaillée](https://docs.framasoft.org/fr/grav/composants-de-base.html#boutons).

## Images

Utilisez une image en ligne en copiant son adresse (finissant par `.jpg`, `.png`, `.gif` etc…) avec un texte alternatif entre crochets (qui sera affiché si l'image n'apparaît pas) et le lien entre parenthèses. Vous pouvez aussi ajouter un texte qui apparaîtra au survol de la souris grâce aux `"`.

```
![le logo de Framasoft](https://framasoft.org/nav/img/logo.png)
```

donnera :

![le logo de Framasoft](https://framasoft.org/nav/img/logo.png)

On peut ajouter un texte au survol :

```
![Le logo de Framasoft](https://framasoft.org/nav/img/logo.png "Un bien beau logo !")
```

Qui donnera (survolez l'image avec votre souris pour voir apparaître le texte) :

![Le logo de Framasoft](https://framasoft.org/nav/img/logo.png "Un bien beau logo !")

## [](https://docs.framasoft.org/fr/grav/markdown.html#citation)Citation

Les citations se font avec le signe `>` :

```
> Oh la belle prise !
```

> Oh la belle prise !

## [](https://docs.framasoft.org/fr/grav/markdown.html#listes)Listes

Vous pouvez créer des listes avec les caractères `*` et `-` pour des listes non ordonnées ou avec des nombres pour des listes ordonnées.

Une liste non ordonnée :

```
* une élément
* un autre
 * un sous élément
 * un autre sous élément
* un dernier élément
```

-   une élément
-   un autre
    -   un sous élément
    -   un autre sous élément
-   un dernier élément

Une liste ordonnée :

```
1. élément un
2. élément deux
```

1.  élément un
2.  élément deux

## [](https://docs.framasoft.org/fr/grav/markdown.html#titres)Titres

Pour faire un titre, vous devez mettre un `#` devant la ligne. Pour faire un titre plus petit, ajoutez un `#` (jusque 6) :

```
# Un grand titre
## Un titre un peu moins grand
### Un titre encore moins grand
```

Vous pouvez également souligner le texte en utilisant `===` ou `---` pour créer des titres.

```
Un grand titre
=============
```

## [](https://docs.framasoft.org/fr/grav/markdown.html#tableaux)Tableaux

Pour créer un tableau vous devez placer une ligne de tirets (`-`) sous la ligne d'entête et séparer les colonnes avec des `|`. Vous pouvez aussi préciser l'alignement en utilisant des `:`. :

```
| Aligné à gauche  | Centré          | Aligné à droite |
| :--------------- |:---------------:| -----:|
| Aligné à gauche  |   ce texte        |  Aligné à droite |
| Aligné à gauche  | est             |   Aligné à droite |
| Aligné à gauche  | centré          |    Aligné à droite |
```

| Aligné à gauche  | Centré          | Aligné à droite |
| :--------------- |:---------------:| -----:|
| Aligné à gauche  |   ce texte        |  Aligné à droite |
| Aligné à gauche  | est             |   Aligné à droite |
| Aligné à gauche  | centré          |    Aligné à droite |

# Les codes raccourcis (shortcodes)

## Alignements

La syntaxe markdown seule ne permet pas d’aligner du texte mais Grav inclus quelques shortcodes :

```
[left]Texte àligné à gauche[/left]
[center]Texte centré[/center]
[right]Texte algné à droite[/right]
```

Après il reste possible d’utiliser du HTML et les classes CSS de Bootstrap :

```
<p class="text-center">Texte centré</p>
```

Les classes de Bootstrap sont : `text-left¦text-center¦text-right¦text-justify`

## Couleurs

La syntaxe markdown seule ne permet pas non plus d’utiliser des couleurs mais vous pouvez utiliser ce shortcode :

```
Texte normal suivi d’un [color=#26B260]texte coloré en vert[/color] dans un paragraphe.
```

Vous pouvez utiliser du code html :

```
Texte normal suivi d’un <span style="color: #26B260">texte coloré en vert</span> dans un paragraphe.
```

Les classes Bootstrap de couleurs « contextuelles » sont aussi disponibles :

-   <span style="color: grey">text-muted</span>
-   <span style="color: blue">text-primary</span>
-   <span style="color: cyan">text-info</span>
-   <span style="color: #26B260">text-success</span>
-   <span style="color: yellow">text-warning</span>
-   <span style="color: red">text-danger</span>

Même chose avec l’arrière plan

-   <span class="bg-info text-success">bg-primary</span>
-   <span class="bg-info text-success">bg-info</span>
-   bg-success<span class="bg-info text-success"></span>
-   <span class="bg-info text-success">bg-warning</span>
-   <span class="bg-info text-success">bg-danger</span>

Exemple :

```
Texte normal suivi d’un <span class="bg-info text-success">texte coloré en vert sur fond bleu</span> dans un paragraphe.
```

## Icônes

La manière la plus simple d’ajouter des [icônes FontAwesome](https://fontawesome.com/v4.7.0/icons/) (version 4) est d’utiliser ces shortcodes :

   [Avec un lien](https://www.mozilla.org/fr/firefox/new/) 

```
    [fa=firefox /]
    [fa=firefox extras=fa-2x /]
    [[fa=firefox extras=fa-3x /] Avec un lien](https://www.mozilla.org/fr/firefox/new/)
    [fa=firefox extras=fa-4x,fa-spin /]
```

Dans les modules et autres composants du thème GravStrap, [la syntaxe est plus détaillée](https://docs.framasoft.org/fr/grav/composants-de-base.html#ic%C3%B4nes).