# Plugins jquery

Les plugins peuvent être inclus individuellement via leur fichier JS  
ou tous en même tout en utilisant le fichier `bootstrap.js`

Attention : certains plugins ont besoin d'un autre en dépendance

Deux façon d'utiliser les plugins :

- en utilisant un attribut `data` dans le code HTML
- en utilisant un objet jQuery dans le code JS

Exemple avec l'attribut data :

```html
<button type="button" class="btn btn-primary" data-toggle="collapse" data-target="#item">Afficher</button>

<div class="collapse" id="item">
    <div class="well">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Corporis quis illo sunt, cumque voluptate consequuntur minus, blanditiis reiciendis suscipit asperiores. Quisquam eligendi aut quo et saepe sint, temporibus repellendus quas?
    </div>
</div>
```

Le `data-target` contient une ancre vers l'élément à afficher

Exemple avec un objet jQuery :

```html
<button type="button" class="btn btn-primary">Afficher</button>
<div class="collapse"id="item">
    <div class="well">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Corporis quis illo sunt, cumque voluptate consequuntur minus, blanditiis reiciendis suscipit asperiores. Quisquam eligendi aut quo et saepesint,temporibus repellendus quas?
    </div>
</div>
```

```jsx
$('button').click(function() {
	$('#item').collapse('toggle');
});
```
