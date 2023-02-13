# Emmet

## Raccourcis HTML

| **Commande (suivi de la touche TAB)**             | **Description**                                              |
| ------------------------------------------------- | ------------------------------------------------------------ |
| `!`                                               | Squelette  HTML                                              |
| `lorem`                                           | Insérer un lorem ipsum. On peut indiquer le nombre de mot. Ex:`lorem20` |
| `balise#idName`<br />`balise.className.className` | créer une  balise avec un ID / classe. Si on ne précise pas la balise, créé un balise `div` |
| `balise>balise>balise>`                           | créer une  hiérarchie d'éléments HTML                        |
| `balise:`                                         | Pour certaines balises permet de spécifier les attributs les plus courant. Par exemple : `input:number`> créé un `input` de type `number` |
| `balise*N`                                        | créer *N* balises de même type                               |
| `balise+balise`                                   | Créer des  éléments frères                                   |
| `^`                                               | Remonter  d'un niveau. Ex: ` ul>li*3^p` => crée un `ul` avec 3 `li` puis on remonte d'un niveau pour créer un `p` (qui sera frère du `ul`) On peut indiquer plusieurs `^` pour remonter de plusieurs niveaux |
| `[nom_attr="valeur"]`                             | Ajouter un  attribut  Ex :   `img[src="photo.jpg"]`          |
| `{}`                                              | pour  insérer du texte  Ex :   `h1{ceci  est un titre}`      |
| `$*N`                                             | pour  ajouter une numérotation (dans les intitulés, nom d'attribut) . Ex :   `ul>li.item$*5`  (les 5  classes seront nommées item1, item2,…) |
| `$@X*N`                                           | commencer  la numérotation à `X`Ex ;   `ul>li.item$@3*5`  (les 5  classes seront nommées item3, item4,…) |
| `$@-*N`                                           | numérotation  décroissante . Ex :  `ul>li{élément $@-}*5`  les  intitulés des 5 éléments de liste seront nommées élément 5, élément 4, …) |
| `( )`                                             | Permet de  faire des groupements  Ex :   `(ul>li*2>a)+p`     |

## Raccourcis CSS

| Commande                             | Description                                                  |
| -----------------------------------  | ------------------------------------------------------------ |
| `c#f,` , `bc#f`                     | `color: #fff` ,` background-color: #fff`                     |
| `posa`, `posr`, `posf`             | position absolu, relatif,  etc.                              |
| `w`, `h`, `p`, `m`                  | `width`, `height` , `padding`, `margin`                      |
| `w100`, `w100p`, `w100e`, `w100rem` | pour indiquer une valeur en px, %, em ou rem                 |
| `mt`, `mb`                          | margin top, bottom                                           |
| `df`, `db`                            | display flex, block                                          |
| `ff`,  `fz`, `ta`, `tar`            | `font-family`, `font-size`, `text-align`, `text-align:right` |
| `lg`                                | `linear-gradient()`                                          |
