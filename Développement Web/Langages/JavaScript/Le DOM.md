# Le DOM

DOM = Document Object Model. Interface de programmation pour les documents HTML et XML. Standardisé par le W3C

## Structure du DOM HTML

Le DOM d'une page Web est créé automatiquement par le navigateur lors du chargement de la page.

Il représente le document sous la forme d'une arborescence hiérarchisée. Les éléments HTML sont considérés comme des objets de type `Node` (nœud) et possèdent donc des propriétés et méthodes. Un nœud peut avoir des nœuds enfants.

Le texte est aussi un nœud de type `#text` qui ne peut pas avoir de nœuds enfants. **Attention : les espaces et les retours à la ligne sont considérés par les navigateurs comme des nœuds textuels**

```html
 <!doctype html>
 <html>
     <head>
         <meta charset="utf-8" />
         <title>Le titre de la page</title>
     </head>
     <body>
         <div>
             <p>Un peu de texte <a>et un lien</a></p>
         </div>
     </body>
 </html>
```

![](DOM.png)

## Héritage

L'objet `Node` contient des propriétés et méthodes qui sont également disponible pour les objets enfants => les objets enfants héritent des propriétés et méthodes des objets parents

![](dom_heritage.png)

Les objets du DOM sont toujours accessibles par référence

## Propriétés

Chaque objet du DOM a une propriété `nodeType` qui renvoie un entier spécifiant le type de nœud. Cet entier correspond à une constante

- `Node.ELEMENT_NODE` : nœud *Element* (`<p>`, `<div>`…)
- `Node.TEXT_NODE` : nœud *Text*
- `Node.DOCUMENT_NODE` : nœud *Document*

```js
 console.log(document.nodeType === Node.DOCUMENT_NODE);  // true
```


Rappel : les objets du DOM sont accessibles par référence

## Accéder à des éléments html

On utilise l'objet `document` (qui est un sous objet de `window` ) et qui représente le document courant (élément `<html>`)

### Propriétés

`document.head` : renvoie l'élément `head`

`document.body` : renvoie l'élément `body`

`document.title` : renvoie le titre du document (élément `title`)

`document.links` : renvoie dans un tableau tout les éléments `a` et `area` qui possèdent un attribut `href`

### Méthodes

`document.getElementById()` : renvoie un élément spécifié par son id ou `null` si l'élément n'existe pas. Prend en paramètre une chaine de caractère correspondant à la valeur de l'id de l'élément.

`document.getElementsByTagName()` : renvoie un objet de type `nodeList` contenant tous les éléments de même nom (h1,p, div…) dans l'ordre d'apparition sur la page. Prend en paramètre une chaine de caractère correspondant au nom. **Cette méthode est accessible sur n'importe quel élément HTML** et pas seulement sur l'objet `document`. Si l'élément est l'objet `document`, la recherche se fait dans tout le document y compris le nœud racine. Si il s'agit d'un autre élément html la recherche porte sur les enfants de l'élément spécifié, à l'exception de l' élément lui-même. Il est possible de mettre en paramètre une astérisque qui récupérera tous les éléments HTML contenus dans l'élément ciblé.

`document.getElementsByName()` : Renvoie un objet contenant tout les éléments qui possèdent le même attribut `name`. Prend en paramètre une chaine de caractère correspondant à la valeur de l'attribut.

`document.querySelector()` : renvoie le premier élément trouvé correspondant à un sélecteur CSS. Prend en paramètre une chaine de caractère correspondant au sélecteur.

`document.querySelectorAll()` : renvoie dans un objet tout les éléments correspondant à un sélecteur CSS trouvés

Choix de la méthode de sélection **:**

- `getElementsByTagName` : Sélection de plusieurs éléments par nom de balise
- `getElementsByClassName` : Sélection de plusieurs éléments par nom de classe
- `querySelectorAll` : Sélection de plusieurs éléments autre que par nom de balise ou classe
- `getElementById` : Sélection d'un seul élément par nom d'id
- `querySelector` : Sélection d'un seul élément autre que par nom d'id

Les méthodes `querySelector()` et `querySelectorAll()` sont plus pratiques mais moins performantes que les méthodes `getElementsByTagName()`, `getElementsByClassName()` et `getElementById()`

## Informations sur les éléments

Une fois un élément récupéré, on peut utiliser des propriétés et méthodes afin d'obtenir des informations

### Propriétés

`parentNode` : renvoie le parent de l'élément

`nodeName` : renvoie le nom de l'élément (en majuscule)

`childNodes` : renvoie la liste des enfants de l'élément.  
(attention : les "blancs" comme les espaces et tabulations sont considérés comme des nœuds textuels)

`firstChild` : renvoie le premier premier enfant de l'élément

`firstElementChild` : renvoie le premier enfant, en prenant en compte que les éléments HTML et pas les nœuds textuels

`lastChild` : renvoie le dernier enfant de l'élément

`lastElementChild` : renvoie le dernier enfant, en prenant en compte que les éléments HTML et pas les nœuds textuel

`nextSibling` : renvoie le nœud suivant de l'élément

`nextElementSibling` : renvoie le nœud suivant de l'élément, en prenant en compte que les éléments HTML et pas les nœuds textuels

`previousSibling` : renvoie le nœud précédent de l'élément

`previousElementSibling` : renvoie le nœud précédent de l'élément, en prenant en compte que les éléments HTML et pas les nœuds textuels

`classList` : renvoie dans un tableau la liste des classes de l'élément.

### Méthodes

`hasChildNodes()` : permet de vérifier la présente d’éléments enfants. Renvoie true si l'élément possède au moins un enfant

`contains()` : teste si le nœud indiqué en paramètre est un descendant de l'élément, c’est-à-dire l'élément lui-même, un des ses enfants directs (`childNodes`) ou indirects

Exemple

```html
 <body>
     <div id="div">
         <h1>Ceci est un titre</h1>
         <p id="p">ceci est un paragraphe avec un <a href="#">lien</a>.</p>
     </div>
```

```jsx
 var div = document.getElementById("div");
 console.log(div.nodeName); // DIV
 console.log(div.parentNode); // <body>
 console.log(div.childNodes); // NodeList(5) [ #text, h1, #text, p#p, #text ]
 console.log(div.firstChild); // #text
 console.log(div.firstElementChild); // <h1>
 console.log(div.lastChild); // #text
 console.log(div.lastElementChild); // <p id="p">
 console.log(div.lastElementChild); // <p id="p">
 
 var p = document.getElementById("p");
 console.log(p.nodeName); // P
 console.log(p.parentNode); // <div>
 console.log(p.childNodes); // NodeList(3) [ #text, a, #text ]
 console.log(p.firstChild); // #text "ceci est un paragraphe avec un "
 console.log(p.firstElementChild); // <a href="#">
 console.log(p.previousSibling); // #text
 console.log(p.previousElementSibling); // <h1>
 
 console.log(div.contains(p)); // true
```

## Récupérer et modifier le contenu d'un élément

### Propriétés

`innerHTML` : permet de récupérer ou de modifier tout le contenu (balise HTML et texte) de l'élément  
Remarque : pour ajouter du contenu sans modifier celui déjà présent on peut utiliser +=

`textContent` : permet de récupérer ou modifier le contenu de l'élément sans les balises HTML

`nodeValue` : permet de récupérer ou de modifier la valeur d'un nœud textuel. Retourne `null` si le nœud n'est pas de type textuel

Exemple :

```html
 <p id='p'>ceci est un paragraphe et <a href="#">ceci est un lien</a>.</p>
```

```jsx
 var p = document.getElementById('p');
 console.log(p.innerHTML); // ceci est un paragraphe et <a href="#">ceci est un lien</a>.
 console.log(p.textContent); //ceci est un paragraphe et ceci est un lien
 console.log(p.nodeValue); // null
 console.log(p.firstChild.nodeValue); // ceci est un paragraphe et
```

`dataset` : Permet de manipuler les données des attributs `data-*`. On utilise le nom donné à l'attribut (sans le préfixe data-) comme propriété de `dataset`

```html
 <img src="photo.jpg" alt="photo" id="photo" data-author="Toto"  data-date="01/01/2001" data-place="Neverland">
```

```jsx
 var element = document.getElementById('photo');
 
 // Lecture d'une valeur 
 var place = element.dateset.place; 
 
 // modification d'une valeur
 element.dataset.author = "poum"; 
 
 // suppression 
 element.dataset.date = null;
```

### Méthodes

**Pour les attributs**

`getAttribute()` : permet de récupérer la valeur d'un attribut. Prend en paramètre le nom d'un attribut.

`hasAttribute()` : Permet de vérifier la présence d'un attribut. Prend en paramètre le nom d'un attribut et renvoie un booléen.

`setAttribute()` : Permet d'ajouter un nouveau attribut ou de modifier la valeur d'un attribut existant. Prend en paramètre le nom de l'attribut et la nouvelle valeur (Pour un attribut booléen, il faut indiquer une chaine vide `""` comme valeur)

`removeAttribute()` : Permet de supprimer un attribut. Prend en paramètre le nom de l'attribut et retourne aucune valeur

Exemple

```html
<body>
    <header>
        <p>Quelques langages de programmation</p>
    </header>
    <ul id="langages">
        <li id="cpp">C++</li>
        <li id="java">Java</li>
        <li id="php">PHP</li>
    </ul>
</body>
```

```jsx
// Remplace le paragraphe par un titre
document.querySelector('header').innerHTML = '<h1>Quelques langages de programmation</h1>'

// ajoute JavaScript dans la liste
document.getElementById('langages').innerHTML += '<li id="js" class="interprete objet">JavaScript</li>';

// modifie PHP par Python
var element = document.getElementById('php');
element.textContent = 'Python';
element.setAttribute('id', 'Python');
console.log(element.id); // Python
```

Certains attributs sont directement accessibles sous la forme d'une propriété

- `id` ⇒ `element.id`
- `href` ⇒ `element.href`
- `class` ⇒ `element.className` (renvoie une chaine contenant la liste des valeurs) ou `element.classList` (renvoie la liste des valeurs sous forme de tableau)
- `for` ⇒ `element.htmlFor`

**Attention : `getAttribute()` renvoie toujours la valeur exacte de l'attribut , ce qui n'est pas forcément le cas lors de l'accès via une propriété**

Exemple

```html
<a id="lien" href="/">Retour à l'accueil du site</a>
```

```jsx
var lien = document.getElementById("lien");
console.log(lien.getAttribute("href")); // affiche " / "
console.log(lien.href); // affiche  l'url du site
```

**Pour les class**

La propriété `classList` qui retourne la liste des classes d'un élément peut être utilisé avec les méthodes :

`classList.remove()` : supprime la classe indiquée en paramètre

`classList.add()` : ajoute la classe indiquée en paramètre (chaine de caractère)

`classList.contains()` : teste si l'élément contient la classe indiquée en paramètre

`classList.replace()` : pour remplacer une classe par une autre. Prend en paramètre l'ancienne classe suvi de la nouvelle

## Modifier les éléments

### Créer et ajouter un nouvel élément

3 étapes :

1. création de l'élément
2. Définition des information de l'élément
3. Insertion de l'élément dans le DOM

`document.createElement()` : permet de créer un élément HTML. Prend en paramètre une chaine de caractères correspondant à l'élément (ex : 'p') .

`document.createTextNode()` : permet de créer un élément textuel. Prend en paramètre une chaine de caractères correspondant au contenu textuel.

`element.appendChild()` : Permet d'insérer l'élément indiqué en paramètre en tant que dernier enfant dans un autre element.

`element.insertBefore()` : prend comme paramètres l'élément à insérer en tant qu'enfant et l’élément avant lequel le nouvel élément sera inséré. Remarque : il n'existe pas de méthode "insertAfter()"

Toutes ces méthodes retournent la référence de l'objet créer.

Pour des meilleures performances, il est conseillé de créer d'abord tous les éléments, puis de les insérer les uns dans les autres avant insérer le tout dans le document

Exemple

```html
<ul id="langages">
	<li id="cpp">C++</li>
	<li id="java">Java</li>
	<li id="php">PHP</li>
</ul>
```

```jsx
// création élément JavaScript
var jsElement = document.createElement('li');
jsElement.id = 'js';
jsElement.textContent = 'JavaScript';

// création élément Python
var pythonElement = document.createElement('li');
pythonElement.id = 'python';
pythonElement.textContent = 'Python';

// insertion de l'élément JavaScript en dernier enfant
var js = document.getElementById('langages').appendChild(jsElement);

// insertion de l'élément Python avant l'élément PHP
var python = document.getElementById('langages').insertBefore(pythonElement, document.getElementById('php'));

console.log(jsElement === js) // true (pointent vers le même objet)
console.log(pythonElement === python) // true (pointent vers le même objet)
```

### Autre méthode pour créer et ajouter un nouvel élément

`element.insertAdjacentHTML()` : prend en paramètre une position et une chaine de caractère contenant le code HTML à insérer . S'applique sur un élément existant. Retourne `undefined`

Valeurs possible pour la position :

- `beforebegin` : avant l'élément
- `afterbegin` : à l'intérieur de l'élément , avant son premier enfant.
- `beforeend` : à l'intérieur de l'élément, après son dernier enfant.
- `afterend` : après l'élément

Exemple

```html
<ul id="langages">
    <li id="cpp">C++</li>
    <li id="java">Java</li>
    <li id="php">PHP</li>
</ul>
```

```jsx
// insertion C en premier enfant
document.getElementById('langages').insertAdjacentHTML('afterbegin', '<li id="c">C</li>');

// insertion JavaScript en dernier enfant
document.getElementById('langages').insertAdjacentHTML('beforeend', '<li id="js">JavaScript</li>')
```

### Modifier ou supprimer un élément

`replaceChild()` : prend deux paramètres, le nouvel élément et l'élément à remplacer. La méthode est exécuter sur le parent du nœud à remplacer.

`removeChild()` : Permet de supprimer l' élément enfant indiqué en paramètre.

Les deux méthodes Retourne la référence de l'élément supprimé ce qui permet de le réutiliser pour l’insérer ailleurs dans le DOM avec la méthode `appendChild()`

Exemple

```html
<ul id="langages">
    <li id="cpp">C++</li>
    <li id="java">Java</li>
    <li id="php">PHP</li>
</ul>
```

```jsx
// création élément python
var pythonElement = document.createElement('li');
pythonElement.id = 'python';
pythonElement.textContent = 'Python';

// remplace PHP par Python 
document.getElementById('langages').replaceChild(pythonElement, document.getElementById('php'));

// supprimer C++
document.getElementById('langages').removeChild(document.getElementById('cpp'));
```

### Cloner un élément

Les objets du DOM étant toujours accessibles par référence il n'est pas possible de copier un élément en l'affectant à une nouvelle variable, car les deux variables pointeront vers la même référence.

A la place il faut donc utiliser la méthode `cloneNode()` qui permet de cloner un élément . Cette méthode prend  
en paramètre un booléen :

- `true` : cloner le nœud avec ses enfants et ses différents attributs
- `false` : sans les enfants et les attributs

Une fois l'élément cloné il faut ensuite l’insérer avec `appendChild()`
