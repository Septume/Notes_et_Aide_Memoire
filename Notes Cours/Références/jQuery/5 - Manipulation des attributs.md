# Manipulation des attributs

### **Attributs généraux**

`attr(nomAttribut)` : Retourne la valeur de l' attribut du premier élément de la sélection. Retourne `undefined` si l'attribut est absent

`attr(nomAttribut, valeur)` : modifier ou créer un attribut.

`removeAttr(nomAttribut)` : supprime un attribut

Exemple

```html
<div>Ceci est du texte</div>
```

```jsx
var div = $('div');
console.log(div.attr('id')); // undefined

//créé l'id "container"
div.attr('id', 'container');

// affiche la valeur de l'id 
console.log(div.attr('id')); // container
```

Pour indiquer plusieurs attributs on peut utiliser un objet

### **Attribut class**

`addClass(nomClasse)` : ajoute une classe dans les éléments sélectionnés

`removeClass(nomClasse)` : supprime une classe (si elle existe) des éléments sélectionnés

`toogleClass(nomClasse)` : si la classe existe elle est supprimée. Si elle n'existe pas elle est ajoutée

`toogleClass(nomClasse, booleen)` : si `true` la classe est ajoutée. Sinon elle est supprimée

`hasClass(nomClasse)` : teste la présence d'une classe dans un ou plusieurs éléments de la sélection

Exemple

```json
/* supprime des paragraphes la classe "vert"
et ajoute les classes "rouge" et "important" */
$('p').removeClass('vert').addClass('rouge important');
```

### **Propriétés**

`prop(nomPropriete)` : retourne la valeur de la propriété du premier élément de la sélection.

`prop(propriete, value)` : modifie la valeur de la propriété du premier élément de la sélection.

Exemple de propriétés :

- `autofocus`
- `autoplay`
- `checked`
- `controls`
- `disabled`
- `hidden`
- `loop`
- `readonly`
- `required`
- `selected`

Exemple

```html
<button>Cliquez</button>
<p hidden>Ceci est du texte</p>
```

```jsx
/* fait apparaitre/disparaitre le texte
quand on clique sur le bouton */

var text = $('p');
$('button').on('click', function () {
    if (text.prop('hidden')) {
        text.prop('hidden', false);
    } else {
        text.prop('hidden', true);
    }
});
```
