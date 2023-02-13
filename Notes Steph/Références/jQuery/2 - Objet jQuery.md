# Objet jquery

Contient une collection d'éléments DOM.

Pour connaître le nombre d'éléments l'objet on utilise la propriété `length`

`$(param).length`

Si l'objet est vide (aucun éléments) `length` renvoie la valeur 0

### **Accéder à un élément**

Deux possibilités :

- via un indice : `$(param)[indice]`
- méthode `get()` : retourne la liste des éléments dans un array. Il est possible d'indiquer en argument un indice pour obtenir un seul élément de la liste

```jsx
 // on sélectionne le titre et le paragraphe
 var collection = $('h1, p');
 
 // nombre d'élément
 console.log(collection.length) // 2
 
 // acceder à un élément via un indice
 console.log(collection[0]) // <h1>
 console.log(collection[1]) // <p>
 
 // acceder à un élément via la méthode get()
 console.log(collection.get(0)); // <h1>
 console.log(collection.get(1)); // <p>
 
 // retourne dans un array tout les éléments 
 var tab = collection.get(); 
 
 //parcours du tableau avec du JS classique 
 tab.forEach(function(element, indice){
     console.log(indice + " : " + element);
     /*
     0 : [object HTMLHeadingElement]
     1 : [object HTMLParagraphElement]
     */
 });
 
```

### **Faire référence à l'objet courant**

On utilise : `$(this)`

```jsx
 $("#myId").fadeOut("slow",function(){
     $(this).fadeIn("slow");
     // méthode appliqué à l’objet retourné par le selecteur $("#myId")
 }); 
 // fait disparaître puis réapparaître progressivement l'élément
```

### **Parcourir un objet jquery**

Méthode : `each()`

Prend une fonction anonyme en argument qui permet d'appliquer un traitement sur chaque élément

cette fonction anonyme peut prendre deux paramètres (facultatifs) correspondant :

- à l'indice de l'élément
- à l'objet élément

`$(param).each (function(index, element){})`

```html
 <div id='container'>
     <p>ceci est un paragraphe</p>
     <p id="test">ceci est du texte et <a href="http://perdu.com">ceci est un lien</a>.</p>
 </div>
```

```jsx
 var $paragraph = $('p');
 var $link = $('a');
 var $ul = $('ul');
 
 // nombre d'éléments dans chaque objet jQuery
 
 console.log($paragraph.length); // 2
 console.log($link.length); //1
 console.log($ul.length); // 0
 
 // liste des éléments dans chaque objet
 
 $paragraph.each(function (index, element) {
     console.log(index + " : " + element);
     /*
     0 : [object HTMLParagraphElement]
     1 : [object HTMLParagraphElement]
     */
 });
 
 
 $link.each(function (index, element) {
     console.log(index + " : " + element); // 0 : http:/•/perdu.com/
 });
```

Le mot clé `this` permet de faire référence à l'élément courant sur lequel on peut appliquer une méthode JS classique.

On peut également utiliser `$(this)` qui permet de convertir l'élément en cours en objet jQuery sur lequel on utilise des méthodes spécifiques à ce dernier

```jsx
 $('p').each(function() {
     // affiche le contenu de chaque élément de la selection
 console.log($(this).text(); 
 });
```

### **Créer des objets jquery**

En plus des sélecteurs, la fonction `$()` peut prendre d'autre argument pour créer des objets jQuery

### **Convertir des éléments du dom en objet jquery**

`var variable = $(element)`

```html
 <div id='container'>
     <p>Ceci est un paragraphe</p>
     <p>ceci est un deuxième paragraphe</p>
 </div>
```

```jsx
 var container = document.getElementById('container');
 var p = document.querySelectorAll('p');
 
 // conversion en objet jQuery
 var $container = $(container);
 var $p = $(p);
 
 console.log($container.length); // 1
 console.log($p.length);// 2
```

### **Cloner un objet jquery**

`var nvObjet = $(objet)`

Le nouvel objet référence les même éléments du DOM que l'objet initial

### **Créer un objet vide**

On appelle la fonction sans argument

`$()`

### **Créer des éléments du dom à la volée**

On indique en argument de la fonction `$()` une chaine de caractère représentant un élément du DOM. Cette chaine doit obligatoirement commencé par une balise pour être considérée comme de l'HTML

```jsx
 var paragraph = $('<p>ceci est un paragraphe</p>')
```
