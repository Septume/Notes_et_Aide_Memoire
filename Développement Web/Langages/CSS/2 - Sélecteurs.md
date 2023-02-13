# Sélecteurs

Remarque : pour indiquer plusieurs sélecteurs ont doit les séparer par une virgule.

## Sélecteurs basique

- `nomElement` : **sélecteur de type**. cible un élément en fonction de son nom
- `.nomClasse` : **sélecteur de classe.** cible les éléments qui ont pour attribut cette classe.
- `#nomId` : **sélecteur d’identifiant.** cible un élément en fonction de son attribut id
- `*`: **sélecteur universel.** cible tous les éléments

Remarque :

- Écrire `.nomClasse` ou `#nomId` revient à écrire `*.nomClasse` ou `*#nomId`.
- On peut faire précéder un sélecteur de classe ou d'identifiant par le nom d'un l'élément à cibler. Ex : `p.nomClasse`
- On peut chainer les classes, ce qui permet de sélectionner uniquement les éléments qui possèdent les classes en question. Ex : `.nomClasse1.nomClasse2` ⇒ sélectionne les éléments qui ont les classes *nomClasse1* ET *nomClasse2*

## Combinateurs

- `A B` : **sélecteur descendant**. cible un élément B qui est un descendant de l’élément A. (Un descendant peut être un enfant direct ou indirect)
- `A > B` : sélecteur enfant. cible un élément B qui est enfant direct de l’élément A
- `A + B` : sélecteur adjacent. Cible un élément B qui suit immédiatement un élément A au sein d’une même parent. (L’élément B est le premier frère situé après l’élément A)
- `A ~ B` : **sélecteur siblings** (ou sélecteur de voisins généraux). Cible un élément B qui suit directement ou non un élément A au sein d’une même parent. (L’élément B est un des frères situés après l’élément A)

## Sélecteur par attribut

Permet de cibler un élément en fonction de son attribut

- `element[Attr]` : éléments possédant l’attribut Attr . On peut faire aussi un chainage ( `element[Attr1][Attr2]`) ou utiliser le selecteur universel (`*[Attr]`)
- `element[Attr="val"]` : éléments possédant l’attribut Attr et dont la valeur est exactement égale à val
- `element[Attr~="val"]` : éléments possédant l’attribut Attr et qui contient une liste de valeurs séparées par des espaces donc une d’entre elles est exactement égal à val
- `element[Attr|="val"]` : éléments possédant l’attribut Attr et qui contient une liste de valeurs séparées par des tirets donc la première est exactement égale à val (utile pour cibler les codes de langue utilisant la sous-dénomination)
- `element[Attr\*="chaine"]` : éléments possédant l’attribut Attr et dont la valeur contient la chaîne spécifiée
- `element[Attr^="chaine"]` : élément possédant l’attribut Attr et dont la valeur commence par la chaîne spécifiée
- `element[Attr$="chaine"]` : éléments possédants l’attribut Attr et dont la valeur se termine par la chaîne spécifiée

## Pseudo-classes

mot-clé, précédé d’un `:` , ajouté au sélecteur et permettant de cibler un élément selon un état particulier, une caractéristique etc… (permet de cibler certains éléments sans avoir à ajouter une classe)

- `:link` : liens non visités (état par défaut)
- `:visited` : liens visités
- `:hover` : lorsque l’élément est survolé (la souris pointe sur l’élément)
- `:active` : lorsque l’élément est activé, c’est à dire au moment même où il est cliqué ou sélectionné avec le clavier, ce qui permet de donner un retour sur l’action (utilisé généralement pour les liens et les bouton)
- `:focus` : lorsque l’élément a le focus (élément sélectionné avec la souris ou le clavier)
- `:enabled` : élément pouvant être activé ou recevoir du contenu textuel
- `:disabled` : élément ne pouvant pas être activé ou recevoir du contenu textuel
- `:checked` : pour les boutons radio, cases à cocher ou options de liste qui sont cochés ou sélectionnés par défaut
- `:required` : élément de formulaire définis comme requis (attribut required)
- `:optional` : élément de formulaire non définis comme requis
- `:valid` : éléments de formulaire respectant le type de donnée attendu
- `:invalid` : éléments de formulaire ne respectant pas le type de donnée attendu
- `:read-write` : élément pouvant être édité comme les champs de texte
- `:default` : élément qui est celui par défaut parmi un groupe d’élément semblables (Ex : bouton radio par défaut)
- `:in-range`: élément input dont la valeur courante est comprise dans l’intervalle défini par les attributs min et max
- `:out-of-range` : élément input dont la valeur courante n’est pas comprise dans l’intervalle défini par les attributs min et max
- `:target` : élément qui est la cible d’un lien (ancre)
- `:lang(langue)` : cible un élément en fonction de sa langue (spécifiée par l’attribut lang)
- `:first-child` : élément qui est le premier enfant de son parent
- `:last-child` : élément qui est le dernier enfant de son parent
- `:nth-child(n)` : élément qui est le nième enfant de son parent
- `:nth-last-child(n)` : élément qui est le nième enfant de son parent en partant du dernier
- `:first-of-type` : élément qui est le premier enfant de son type parmi les enfant de son parent
- `:last-of-type` : élément qui est le dernier enfant de son type
- `:nth-of-type(n)` : élément qui est le nième enfant de son type
- `:nth-last-of-type(n)` : élément qui est le nième enfant de son type en partant du dernier
- `:only-child` : élément qui est le seul enfant de son parent
- `:only-of-type` : élément qui est le seul de son type parmi les enfant de son parent
- `:empty` : élément qui n’a pas d’enfants, ni contenu (espaces compris). Permet de cibler les paires de balises vides (ce qui peut se produire avec de l’HTML généré avec PHP)
- `:root` : Cible l’élément `<html>` ( Équivalent au sélecteur d’élément `html` mais avec une spécificité plus forte)
- `:not(selecteur)` : sélecteur de négation. Cible les éléments qui ne correspondent pas au sélecteur entre parenthèses. (Prend n’importe quel sélecteur en paramètre). N’a pas de spécificité d’une pseudo-classe mais celle du sélecteur en paramètre

Remarques :

- **Attention**. un lien peut avoir deux états en même temps (par exemple : visited et focus). Il est donc important de définir une priorité lorsqu’on utilise les pseudo-classe. L’ordre classique (par priorité croissante) est : `link` `visited` `hover` `focus` `active`
- `link` et `visited` sont réservés aux liens tandis que `hover`, `focus` et `active` peuvent s’appliquer à d’autres éléments.
- pour `nth-child(n)` , etc. il est possible d’utiliser à la place d’un nombre une formule sous la forme `xn + a.` Le style s’applique d’ abord à l’élément en position `a` puis à tout les éléments tout les `x` fois. Exemple : `p:nth-of-type(2n+1)`=> Le style s’applique d’ abord au paragraphe en 1ere position, puis au paragraphe en troisième position etc…)

	on peut également utilisé les valeurs :

	- `even` : pour cibler les enfants paires
	- `odd` = pour cibler les enfants impaires
- il est possible de faire des combinaisons avec le sélecteur de négation `:not()`. Exemple :

	`input:not([type="password"]):not([type="url"])`=> cible toutes les éléments `input` à l’exception des éléments dont l’attribut `type` a pour valeur `password` ou `url`

## Pseudo-éléments

mot-clé, précédé de `::` , ajouté au sélecteur et permettant de cibler un élément virtuel ( qui n’a pas d’existence dans l’arbre DOM)

- `::before` : Premier enfant virtuel de l’élément. Cela créé un élément virtuel (de type inline) qui sera enfant de cet élément. Utiliser essentiellement pour rajouter du contenu visuel avant l’élément via la propriété `content` (dont la valeur peut être une chaine de caractère ou une image)
- `::after` : Dernier enfant virtuel de l’élément
- `::first-letter` : Première lettre de la première ligne de l’élément
- `::first-line` : Première ligne de l’élément
- `::selection` : Texte sélectionnée par l’utilisateur. Permet de changer l'apparence de la sélection avec les propriété comme `color`, `background-color`,…

Remarque : La syntaxe avec deux caractères deux-points `::` a été introduite en CSS3 pour permettre de mieux distinguer les pseudo-éléments des pseudo-classes. L’ancienne syntaxe avec un seul caractère deux-points `:` reste supportée par les navigateurs.

Exemple 1

```css
h1::before {
	content: url(img/puce.png) " ";
}
```

Exemple 2

```css
a[hreflang="eng"]::after {
	content: " [" attr(hreflang) "]";
}
```

Pour la propriété `content` il est possible d'utiliser la fonction `attr()` qui permet de récupérer la valeur d'un attribut (en général on l'utilise pour les attributs `data-*`)

Exemple

```css
/* <div data-line="1"></div> */

div[data-line]:after { 
	content: "[line " attr(data-line) "]"; 
}
```

## Conseils d’utilisation des sélecteurs pour une meilleure performance

- Éviter le sélecteur universel
- Éviter d’utiliser le sélecteur d’id car son poids est trop important. Préférer le sélecteur de classe.
- Éviter les sélecteurs associés à la structure HTML, un élément doit pouvoir être ciblé quel que soit son conteneur ou son emplacement dans le DOM. Utiliser des classes pour chaque élément à styliser plutôt que le nom de l’élément
- Limiter le nombre de sélecteurs de descendance . Par exemple, privilégier `#header a` à `#header ul li a`
- Choisir si possible le sélecteur d’enfant plutôt que le sélecteur de descendance. Par exemple préférer `#header > img` à `#header img`
- Autant que possible, utiliser un identifiant, une classe ou un sélecteur d’élément, mais pas une combinaison de deux ou trois
- Éviter de faire précéder un identifiant par le nom de l’élément ciblé (idem pour les classes). Par exemple, utiliser `#nav` plutôt que `ul#nav`
