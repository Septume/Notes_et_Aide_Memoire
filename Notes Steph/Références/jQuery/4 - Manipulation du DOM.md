# Manipulation du dom

### **Insérer des éléments dom**

`prependTo(cible)` : insérer un élément au début des éléments correspondant à la cible

`appendTo(cible)` : insérer un élément à la fin des éléments correspondant à la cible

`insertBefore(cible)` : insérer un élément avant les éléments correspondant à la cible

`insertAfter(cible)`: insérer un élément après les éléments correspondant à la cible

La cible est un élément du DOM présent sur la page (indiquer par un sélecteur)

L'élément DOM à insérer est indiqué sous forme d'une chaine de caractère qui doit obligatoirement commencée par une balise

Exemple

```html
<ul>
    <li>Combien font 4 * 2 ?</li>
    <li>Combien de pattes a une araignée ?</li>
    <li>Quelle est la première planète du système solaire ?</li>
</ul>

```

```jsx
// insère l'élément avant le contenu de chaque élément li
$('<strong>Question : </strong>').prependTo('li');
```

Il est possible d'indiquer un élément qui est déjà présent sur la page. Dans ce cas l'élément sera déplacer

```html
<p>ceci est du texte</p>
<img src="image.png" />
```

```jsx
// déplace le parapgraphe après l'image
$('p').insertAfter('img');
```

on peut également copier un élément avec la méthode `clone()`

```jsx
// copie le parapgraphe après l'image
$('p').clone().insertAfter('img');
```

### **Insérer du contenu**

`append(contenu)` : insérer du contenu au début de chaque élément de la sélection

`prepend(contenu)` : insérer du contenu à la fin de chaque élément de la sélection

`before(contenu)` : insérer du contenu avant chaque élément de la sélection

`after(contenu)` : insérer du contenu après chaque élément de la sélection

Le contenu doit être indiqué sous forme d'une chaine de caractère et peut contenir des balises HTML

Exemple

```html
<ul>
    <li>Combien font 4 * 2</li>
    <li>Combien de pattes a une araignée</li>
    <li>Quelle est la première planète du système solaire</li>
</ul>
```

```jsx
// ajoute "Question" avant le contenu de chaque éléments li
$('li').prepend('Question : ');

// ajoute "?" après le contenu de chaque éléments li
$('li').append(' ?');

// insère un élément <hr> après la liste
$('ul').after('<hr>');
```

Il est également possible d'indiquer un élément qui est déjà présent sur la page. Dans ce cas l'élément sera déplacer.  
Ou si on utilise la méthode `clone()`, l'élément sera copié.

```html
<input type="text">
<input type="submit">
```

```jsx
var input = $('input:text');
var submit = $('input:submit');
// le bouton d'envoi est déplacé avant le champ
 input.before(submit);
```

### **Remplacer des éléments**

`replaceWith(nouvelElement)`

Le nouvel élément doit être indiqué par une chaine de caractère

Exemple

```html
<h1>ceci est du texte</h1>
```

```jsx
// remplace le titre par un paragraphe
 $('h1').replaceWith('<p>ceci est du texte</p>');
```

SI on souhaite remplacer l'élément sans modifier son contenu on peut procéder ainsi

```jsx
$('h1').each(function(){
    var element = $(this);
    element.replaceWith('<p>' + element.text() + '</p>');
});
```

### **Entourer un élément**

`wrap()` : entourer un élément avec un autre élément

`wrapInner()` : entourer le contenu d'un élément

`wrapAll()` : entourer de manière globale les éléments sélectionnés

Exemple 1

```html
<p>Ceci est du texte </p>
```

```jsx
// met le pagraphe en strong
$('p').wrap('<strong></strong>');

// transforme le contenu en lien 
$('p').wrapInner('<a href="#"></a>');

/* 
résultat : 
<strong><p><a href="#">ceci est du texte</a></p></strong>
*/
```

Exemple 2

```html
<p>Paragraphe 1</p>
<p>Paragraphe 2</p>
<p>Paragraphe 3</p>

un texte isolé

<p>Paragraphe 4</p>

un autre texte isolé
```

```jsx
/* Les paragraphes seront rassemblés
et entourés dans l'ensemble par une div */
$('p').wrapAll('<div></div>');

/*
résultat : 
<div><p>Paragraphe 1</p><p>Paragraphe 2</p><p>Paragraphe 3</p><p>Paragraphe 4</p></div>
un texte isolé un autre texte isolé
*/
```

### **Supprimer un élément**

On utilise la méthode `remove()`

```html
<h1>Titre</h1>
<p>Ceci est du texte</p>
```

```jsx
// supprime le paragraphe 
$('p').remove();
```

### **Supprimer les descendants d'un élément**

On utilise la méthode `empty()`  
Remarque : les nœuds textuels seront également supprimer

Exemple

```jsx
/* supprime tout ce qui a dans la div
y compris les noeuds textuels */

$('div').empty();
```
