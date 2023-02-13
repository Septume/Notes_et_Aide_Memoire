# Texte et typographie

Caractéristiques :

- Utilisation par défaut d'une liste de polices natives qui sélectionne la famille de polices la mieux adaptée à chaque système d'exploitation et à chaque périphérique
- utilisation de valeurs en rem
- `<small>` : Le texte est réduit de 85% (à utiliser dans un balise de titre pour créer un sous-titre)
- `<mark>` : soulignement jaune clair

Titres :

- `display-1`, `display-2`, `display-3,` `display-4` : permet d'augmenter la taille des titres

Paragraphes :

- `lead` : met en avant un paragraphe en augmentant la taille de la police
- `text[-breakpoint]-nowrap` : Le texte ne va pas à la ligne s’il dépasse du conteneur. (un scrolling horizontal apparait)

Caractères :

- `h1`,`h2`… `h6` : permet d'appliquer à un élément un des style de titre en dehors de la sémantique
- `small` : permet d'appliquer à un élément le style de `<small>` en dehors de la sémantique
- `mark` : permet d'appliquer à un élément le style de `<mark>` en dehors de la sémantique

Alignement :

- `text[-breakpoint]-left`
- `text[-breakpoint]-right`
- `text[-breakpoint]-cente`
- `text[-breakpoint]-justify`

Casse :

- `text-lowercase` : mettre en minuscule
- `text-uppercase` : mettre en majuscule
- `text-capitalize` : mettre la première lettre des mots en majuscule

Blockquote :

Par défaut l'élément `<blockquote>` n'a pas de retrait à gauche sur Bootstrap

- `blockquote` : met en forme la citation
- `blockquote-footer` : met en forme le footer d'un blockquote

Exemple

```html
 <blockquote class="blockquote">
     Les cons, ça ose tout. C'est même à ça qu'on les reconnaît.
     <footer class="blockquote-footer">Michel Audiard</footer>
 </blockquote>
```

Listes :

- `list-unstyled` (à placer dans les balises `<ul>` ou `<ol>`) : supprime le style des listes. Attention la classe s'applique uniquement aux éléments de liste qui sont des enfants direct. Cela signifie qu'il faudra aussi ajouter la classe pour toute liste imbriquée
- `list-inline` (à placer dans les balises `<ul>` ou `<ol>`) : supprime le retrait et le style de la liste
- `list-inline-item` (à placer dans les balises `<li>`) : affiche les items avec un display `inline-block` ( à utiliser conjointement avec `list-inline`)
