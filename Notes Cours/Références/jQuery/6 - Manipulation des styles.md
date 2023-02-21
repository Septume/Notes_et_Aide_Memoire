# Manipulation des styles

### **Propriétés css**

`css(nomPropriete)` : retourne la valeur de la propriété

`css(nomPropriete, nouvelleValeur)` : modifie la valeur de la propriété

```html
<p>Ceci est du texte</p>
```

```jsx
// met le texte en gras et en bleu
$('p').css('font-weight', 'bold').css('color', 'blue');
```

### **Positions des éléments**

`offset()` : retourne/modifie les coordonnées d'un élément en position absolu

`position()` : retourne les coordonnées d'un élément en position relative

Ces méthodes retourne deux propriétés `top` et `left` indiquant les coordonnées de l'élément

```jsx
$('div').offset({top: 50, left: 100});
console.log($('div').offset().top); // 50
console.log($('div').offset().left); // 100
```

### **Dimensions des éléments**

`width()`: largeur de l'élément

`innerWidth()` : hauteur en prenant en compte le padding

`outerWidth()` : hauteur en prenant en compte le padding et les bordures.

- `true` : (argument facultatif) prendre en compte également le margin (fonctionne uniquement pour le getter)

`height()` : hauteur de l'élément

`innerHeight()` : hauteur en prenant en compte le padding

`outerHeight()` : hauteur en prenant en compte le padding et les bordures

- `true` : (argument facultatif ) prendre en compte également le margin (fonctionne uniquement pour le getter)

Ces méthodes peuvent prendre en argument une valeur sous la forme :

- d'un nombre entier : représentant le nombre de pixels
- d'une chaine de caractère : représentant une valeur dans une autre unité de mesure (exemple : '100%')
