# Navigation de base

Classes de navigation :

- `nav` : créer une navigation avec un display flex. A placer dans un élément`<ul>` ou `<nav>`
- `nav-items`: mise en forme des éléments de liste. A placer dans un élément `<li>`
- `nav-link`: mis en forme des liens. A placer dans un élément `a`
- `active` : lien actuellement actif
- `disabled` : lien désactivé

Options pour nav :

- `nav-tabs`: lien actif sous forme d'onglet
- `nav-pills` : lien actif sous forme de bouton
- `nav-justified` : la navigation prend toute l'espace disponible avec des éléments de largeur égal (Pour que cela fonctionne sur un élément `<nav>`, il faut la class `nav-item` sur chaque élément `<a>`)
- `nav-fill` : idem mais les éléments n'ont pas de largeur égal

Exemple 1

```html
<ul class="nav nav-tabs">
    <li class="nav-item"><a href="" class="nav-link active">Link</a></li>
    <li class="nav-item"><a href="" class="nav-link">Link</a></li>
    <li class="nav-item"><a href="" class="nav-link">Link</a></li>
    <li class="nav-item"><a href="" class="nav-link">Link</a></li>
    <li class="nav-item"><a href="" class="nav-link disabled">Link</a></li>
</ul>
```

Exemple 2

```html
<nav class="nav nav-pills nav-justified">
    <a href="" class="nav-item nav-link active">Link</a>
    <a href="" class="nav-item nav-link">Link</a>
    <a href="" class="nav-item nav-link">Link</a>
    <a href="" class="nav-item nav-link">Link</a>
    <a href="" class="nav-item nav-link">Link</a>
</nav>
```

Les `nav` étant des conteneur Flex, on peut utiliser les classes pour les Flexbox

```html
<nav class="nav nav-pills flex-column flex-md-row">
```

Barre de navigation

`navbar` : Active la barre de navigation

Les options :

- `navbar-light` : en combinaison avec un background clair
- `navbar-dark` : en combination avec un background sombre
- `navbar-expand[-breakpoint]`: Etendre les liens à l' horizontal

Les classes à utiliser à l'intérieur de la `navbar` :

- `navbar-brand` : Marque- A utiliser sur un lien ou un texte
- `navbar-nav` : liste de liens de navigation
