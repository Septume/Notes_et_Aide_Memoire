# Groupement de contenus

### Paragraphes et blocs de texte

`<p>` : Paragraphe

`<blockquote>` : Bloc de citation longue

- `cite` : URL de la source

`<pre>` : Bloc de texte préformaté. Permet de conserver les espaces blancs (par exemple pour afficher du code informatique). Attention : penser à échapper les caractères `<` en `&lt`

### Listes

`<ol>` : Liste ordonnée. La numérotation peut être modifiée en CSS avec la propriété `list-style-type`

- `reversed` : Attribut booléen. Ordre descendant
- `start` : Valeur de départ pour la numérotation. Doit être un nombre entier.

`<ul>`: Liste non ordonnée. L’apparence des puces peut être modifier en CSS avec la propriété `list-style-type`

`<li>` : Élément d’une liste. Doit être enfant direct d’un élément `ol` ou `ul`. Peut contenir n’importe quel élément textuel (paragraphe, titre, etc…)

- `value` : Valeur ordinale de l’élément. Doit être un nombre entier. Cela permet de contrecarrer l’incrémentation automatique d’une liste ordonnée `ol`

Les éléments `ol` et `ul` ne peut contenir directement que des éléments `li`. (Pas de contenu intermédiaire)

Pour créer des listes imbriquées on ouvre une seconde balise `ul` ou `ol` à l’intérieur d’un élément `li`

```html
<ul>
	<li>item 1</li>
	<li>item 2
		<ul>
			<li>sous item 1</li>
			<li>sous item 2</li>
		</ul>
	</li>
	<li>item 3</li>
</ul>
```

### Liste de définitions

`<dl>` : Pour créer une liste de définition

`<dt>` : Pour indiquer le terme à définir dans une liste de définition. Doit être enfant d’un élément `dl`

`<dd>` : Pour indiquer la description correspondant à un terme dans une liste de définition. Doit être enfant d’un élément `dl`

Il est possible d’associer plusieurs définitions à un terme ou de de définir plusieurs termes via une seule définition. Dans tout les cas le ou les éléments `dd` devront obligatoirement se trouver après le ou les éléments `dt` correspondant

```html
<!-- un seul terme et une seule définition --> 
<dl>
	<dt>Firefox</dt>
	<dd>navigateur Web libre, open-source, multi-plateforme dévelopé par la Mozilla Corporation</dd>
</dl>

<!-- Plusieurs termes avec une même définition --> 
<dl>
	<dt>Firefox</dt>
	<dt>Mozilla Firefox</dt>
	<dd>navigateur Web libre, open-source, multi-plateforme dévelopé par la Mozilla Corporation</dd>
</dl>

<!-- Un seul terme, plusieurs définitions -->
<dl>
	<dt>Firefox</dt>
	<dd>navigateur Web libre, open-source, multi-plateforme dévelopé par la Mozilla Corporation</dd>
	<dd>Le panda roux est un mammifère originaire de l'Himalaya et de la Chine méridionale.</dd>
</dl>
```

### Figures

`<figure>` : Contenus supplémentaires d’enrichissement, généralement accompagné d’une légende (image, illustration, diagramme, schéma, fragment de code, vidéo,…). Peut contenir plusieurs éléments.

`<figcaption>`: Légende associée à une figure. Cet élément doit être le premier ou le dernier enfant de l’élément `figure`

```html
<figure>
	<img src="images/paris.jpg" alt="photo de Paris vue du ciel">
	<figcaption>La ville de Paris</figcaption>
</figure>
```

### Autres éléments

`<hr />` : Indique une séparation thématique

`<div>` : Groupement non sémantique pour l’application de style CSS ou autre.
