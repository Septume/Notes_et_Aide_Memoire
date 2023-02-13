# Fonctionnement du contenu textuel et des éléments inline

## Quelques définitions

**Texte anonyme** : chaine de caractères qui ne se trouve pas dans un élément de type inline.

Par exemple :  
`<p>Je suis <em>tellement</em> content</p>` ⇒ "Je suis " et " content" correspondent à du texte anonyme

**Boite em (em box)** : Il s'agit d'un espace défini par le concepteur de la police et qui peut contenir toutes les lettres de la police, y compris les ascendants et les descendants. On utilise également le terme de **UPM (units per em)**. Dans une police OpenType, l’UPM est généralement fixé à 1000 unités. Dans les polices TrueType, l’UPM est par convention une puissance de deux, généralement définie à 1024 ou 2048. La propriété `font-size` permet de déterminer la hauteur de l'*em-box* de la police utilisée

**Zone de contenu (content area)** :
- Pour les éléments non remplacés : correspond aux *em-box* réunis de chaque caractères.
- Pour les éléments remplacés et les éléments de type *inline-block* : correspond à la hauteur intrinsèque de l'élément à laquelle est éventuellement ajouté les marges internes et externes ainsi que les bordures.  
La zone de contenu est analogue à la boite de contenu d'un élément de type bloc

**Interligne** : Espaces ajoutés au-dessus et en-dessous de la zone de contenu pour les éléments non remplacés et le texte anonyme. La taille dépend de la valeur de `line-height`  
Le calcul est : `(valeur de line-height - valeur de font-size) / 2 = hauteur de chaque espace`  
Par exemple : pour un `font-size` de 16px et un `line-height` de 18px la zone d'interligne est de 4px au total, avec 2px au dessus de la zone de contenu et 2px en dessous.

**Boite en ligne (inline box)** :
- Pour les éléments non remplacés : correspond à zone de contenu + les interlignes. La hauteur de la boite en ligne est fixée par la valeur de `line-height`.
- Pour les éléments remplacés : La hauteur est égale à la zone de contenu (puisque l'interligne n'est pas appliquée à ces éléments).

**Boite de ligne (line-box)** : englobe toute les *inline box* de la ligne. Ces dernières sont alignées verticalement dans la boite en ligne

## Lisibilité de la police

La lisibilité d'une police est influencée par le *aspect ratio.* Il s'agit du rapport entre la hauteur d'x de la police (hauteur des minuscules) et sa taille (hauteur de la police). Pour une taille égale, une police qui a une *aspect ratio* plus élevée sera plus lisible. Par exemple, le Verdena e un ratio de 0.58 tandis que le Times New Roman a un ratio de 0.45, ce qui a taille égal le rend moins lisible. (Voir [ce tableau comparatif](https://www.lifewire.com/aspect-ratio-table-common-fonts-3467385) des polices les plus courantes)

Par conséquent il est recommandé d'utiliser des polices de substitution dont le *aspect ratio* est semblable à la police principale. On peut également utiliser la propriété `font-size-adjust` qui permet de définir la hauteur d'x de la police de substitution en fonction du ratio de la police de premier choix.
