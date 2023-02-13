# Attributs généraux

`hidden` : Booléen. L'élément est désactivé et ne sera pas affiché  
 **Cet attribut doit être utilisé dans un cadre sémantique**. (Par exemple l’affichage d’une information en cas d’erreur de saisie dans un formulaire). Si le but est purement graphique (Par exemple un diaporama ou un système d’onglet) il faut utiliser à la place des propriétés CSS comme`display:none` ou `visibility: hidden`

`accesskey` : Associe un raccourci clavier à un élément. La combinaison de touche pour l’activer dépend du système et du navigateur. La valeur doit être un caractère ou une liste de caractères séparés par des espaces (Le navigateur utilisera le premier caractère disponible). **Cette fonctionnalité étant peu pratique (notamment à cause d’un risque de conflit avec les raccourcis du navigateur ou du système, ainsi qu’une prise en charge hétérogène par les navigateurs), il n’est pas conseillé de l’utiliser.**

`autocapitalize` : Permet la conversion en majuscule du contenu saisi avec un clavier virtuel (comme celui d’un smartphone). Cette attribut n’a pas d’effet sur les `<input>` de type `url`, `email` ou `password`. Les valeurs possibles sont :

- `off` ou `none` : aucune conversion automatique
- `on` ou `sentences` : la première lettre de chaque phrase est automatiquement écrite en majuscule.
- `words` : la première lettre de chaque mot est automatiquement écrite en majuscule.
- `characters` : toutes les lettres sont converties en majuscules.

`class` : Catégorisation de l’élément. Les valeurs sont des mots séparés par des espaces. À utiliser plutôt pour le code CSS

`contenteditable` : Zone de contenu éditable. À utiliser conjointement avec du JS pour traiter les données éditées. Si non définie, la valeur est héritée du parent. Les valeurs possibles sont `true` ou `false`. La propriété CSS `caret-color` permet de modifier la couleur du curseur d’insertion.

`draggable` : Élément pouvant être glissé-déposé lorsqu’on utilise l’API `Drag & Drop`. Les valeurs possibles sont `true` ou `false`. Par défaut, seules les sélections de texte, les images et les liens peuvent être déplacés à la souris. Pour les autres éléments, il faudra définir le gestionnaire d’événements pour `ondragstart` afin de faire fonctionner le glisser-déposer

`id` : Identifiant unique associé à un élément. À utiliser plutôt pour le JS et les ancres

`inputmode` : Permet d’indiquer le type de donnée qui peut être saisie lors de l’édition du contenu d’un élément et afficher un clavier virtuel avec une disposition adaptée à ce type. Les valeurs possibles sont `text` (défaut) , `decimal`, `numeric`, `tel`, `search` et`url`. La valeur `none` indique qu’aucun clavier virtuel ne doit être affiché (Utile si la page Web implémente son propre outil de saisie)

`lang` : Indique la langue de l’élément. La valeur est un code langue conforme au standard BCP47 de l’IETF

`spellcheck` : Indique si le contenu de l’élément doit être vérifié par le correcteur orthographique du navigateur. Les valeurs possible sont `true` et `false` . La valeur par défaut dépend du navigateur. À utiliser pour les champs de formulaire ou les zones de contenus éditables.

`style` : Pour indiquer des propriétés CSS spécifique à l’élément. Les propriétés doivent être séparées par un point-virgule. À utiliser notamment lorsqu’on a besoin de modifier les styles via du code JavaScript

`tabindex` : Pour une navigation au clavier avec la touche tab qui permet de donner le focus à l’élément. La valeur doit être un entier indiquant le numéro d’ordre de élément (Il n’est pas obligatoire de mettre des nombres qui se suivent.). Si plusieurs éléments partagent la même valeur, l’ordre dépend de celui de l’arbre DOM. Un entier négatif permet d’indiquer que l’élément peut capturer le focus mais ne peut pas être atteint via la navigation au clavier. La valeur 0 indique que l’ordre de l’élément dépend de son ordre dans l’arbre DOM. Remarque : la touche TAB permet de naviguer dans les liens, boutons et champs de formulaire

`title` : Intitulé ou libellé de l’élément. Ou dans le cadre d’un élément `<abbr>` , permet d’indiquer la description de l’abréviation. Affiche généralement une infobulle. Si l’élément n’a pas de titre, il hérite de celui de l’ancêtre le plus proche. **Cet attribut est très problématique pour l’accessibilité à cause d’une prise en charge hétérogène de la part des navigateurs et terminaux**. Pour les abréviations il est préférable d’indiquer la description complète dans le texte visible directement par l’utilisateur. A noter que dans le cadre d’un élément `<link>` avec pour relation `stylesheet` , cette attribut permet de définir une feuille de style alternative ou préférée.

`data-*` : Attributs de donnée. Permet d’associer des données personnalisées à un élément HTML. L'astérisque doit être remplacé par n’importe quel nom valide (Pas de majuscules, de point-virgule et ne doit pas commencer par “xml”). La valeur est une chaine de caractères. La propriété JavaScript `HTMLElement.dataset` permet de manipuler ces données

```html
<!-- exemple d'attributs data-* -->
<img src="file.jpg" alt="Une image" data-author="alice" data-place="Paris" />
```

Autres attributs généraux :

- Attributs dédiés à l’accessibilité (`aria-*` et `role` )
- Attributs microdata
- Attributs pour les gestionnaires d'évènements (Par exemple : `onclick`)
