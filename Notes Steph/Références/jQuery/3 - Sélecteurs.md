# Sélecteurs

Permet de sélectionner des éléments du DOM.

Retourne un objet qui contient l'ensemble des éléments trouvés.

Si aucun éléments est trouvés, retourne un objet vide (length: 0)

### **Utilisation des sélecteurs css**

jQuery utilise en parti les sélecteurs CSS :

- sélecteurs basiques
- combinateurs
- sélecteurs d'attributs
- pseudo-classes

```jsx
$('*'); // tout les éléments
$('p'); // les éléments de type paragraphe
$('#container'); // l'élément qui a l'id "container"
$('.item'); // les éléments qui ont pour classe "item"
$('div p'); // les élément p qui sont descendant d'un élément div
$('div[id]'); // les éléments div ayant un attribut id
$('p:first-child'); // les éléments p qui sont le premier enfant de leur parent
```

Il est possible  
d'indiquer plusieurs sélecteurs séparés par des virgules

```jsx
/* sélectionne : 
l'élément qui a l'id "container
les éléments qui ont la class "item"
les éléments p
*/

var selection = $('#container, .item, p');
```

On peut également utilisés plusieurs sélecteurs d'attributs

```jsx
/* les champ input de type text qui ont un id */
var selection = $('input[type="text"][id]');
```

### **Sélecteurs spécifiques à jquery**

Il existe un sélecteur d'attribut spécifique à jQuery

`[attr!='val']` : attribut qui n'a pas la valeur indiqué

```jsx
/*
tout les élément de liste qui n'ont 
pas pour id "vert"
*/
var selection = $('li[id!="vert"]');
```

JQuery propose également des filtres de sélection supplémentaire

- `$(':first')` : premier élément trouvé
- `$(':last')` : dernier élément trouvé
- `$(':eq(index)')` : élément correspondant à l'indice spécifiée (il s'agit de l'indice de l’élément dans l'objet retourné)
- `$(':lt(index)')`: éléments d'indice inférieur à celui spécifiée
- `$(':gt(index)')`	: éléments d'indice supérieur à celui spécifiée
- `$(':has(element)')`: éléments qui contient au moins une fois l’élément spécifié en argument dans l'ensemble de ses descendants. Prend comme argument n'importe quel sélecteur
- `$(':even')`: éléments dont l'indice est pair
- `$(':odd')` : éléments dont l'indice est impair
- `$(':hidden')`: éléments cachés ( attribut : `hidden`)
- `$(':visible')`: éléments visibles
- `$(':header')`: éléments de titre (`h1`, `h2`, etc.)
- `$(':parent')` : éléments qui ont au moins un enfant (en incluant les nœuds textuels)
- `$(':animated')`: éléments actuellement animés (via une méthode jQuery)
- `$(':input')` : éléments `input`, `textarea`, `select` et `button`
- `$(':button')` : éléments `button` ou `input` de type `button`
- `$(':checkbox')` : éléments input de type `checkbox`
- `$(':file')` : éléments input de type `file`
- `$(':image')` : éléments input de type `image`
- `$(':password')` : éléments input de type `password`
- `$(':radio')` : éléments input de type `radio`.
- `$(':text')` : éléments input de type `text`
- `$(':submit')` : éléments input de type `submit`
- `$(':reset')` : éléments input de type `reset`
- `$( ':selected')` : éléments sélectionnés (fonctionne avec l’élément `<option>`)

```jsx
$('p:first'); // premier paragraphe de la page
$('a:last'); // dernier lien de la page
$('p:eq(2)'); // troisième paragraphe de la page
$('div:has(p)'); // div contenant un p
```

### **Contexte**

Par défaut les sélecteurs effectuent la recherche à partir de la racine du document. Il est toutefois possible de restreindre la recherche à un contexte indiqué en deuxième argument

Exemple 1

```jsx
/* les paragraphes de classe "elements"
à chercher dans l'élément d'id "container" */
$('p.elements', '#container');
```

Exemple 2

```html
<div id="foo">
	<p class="bar">Ceci sera en rouge</p>
	<p class="bar">Ceci sera en rouge</p>
	<p>Ceci reste en noir</p>
</div>
<p class="bar">Ceci reste en noir</p>
```

```jsx
$('#foo').on('mouseover', function(){
	/* le changement se fait que dans
	l'élément d'id "foo" */
	$('p.bar', this).css('color', 'red');
});

```
