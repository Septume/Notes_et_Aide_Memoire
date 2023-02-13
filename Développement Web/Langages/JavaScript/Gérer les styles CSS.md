# Gérer les styles css

## **Modifier le style d'un élément**

On utilise la propriété `style` qui renvoie un objet correspondant à l'attribut `style` d'un élément.  
Les propriétés de cet objet correspondent au propriétés CSS de l'élément.

**Attention : Les propriété CSS qui ont un nom composé doivent être écrites de manière différence en JS. Il faut supprimer le tiret et mettre en majuscule la première lettre du deuxième mot (norme camelCase)**. Ex : `font-family` => `fontFamily`

```html
<p>ceci est un paragraphe</p>
```

```jsx
// mettre le fond du paragraphe en rouge
document.querySelector('p').style.backgroundColor = "red";
```

## **Acceder à un style css (lecture seule)**

On utilise la fonction `getComputedStyle()` qui prend en paramètre un nœud du DOM et qui renvoie un objet représentant son style

Exemple

```css
p {
    color: red;
    font-style: italic;
}
```

```jsx
var p = getComputedStyle(document.querySelector('p'));
console.log(p.color); // rgb(255, 0, 0)
console.log(p.fontStyle); // italic
```

## **Propriétés de type offset**

Permet d'obtenir certaines valeurs de taille ou de positionnement des éléments. S'applique sur un élément

`offsetWidth` : retourne une valeur numérique correspondant à la largeur complète (width + padding + border) en pixel de l'élément

`offsetHeight` : retourne une valeur numérique correspondant la hauteur complète (height + padding + border) en pixel de l'élément.

`offsetLeft` : retourne une valeur numérique correspondant la position en pixel de l'élément par rapport au bord gauche de son élément parent. Surtout utile pour les éléments en position absolue

`offsetTop` : retourne une valeur numérique correspondant la position en pixel de l'élément par rapport au bord supérieur de son élément parent.

`offsetParent` : retourne l'élément parent par rapport auquel est positionné l'élément. Utile que pour un élément en position absolue ou relative.

```css
#div {
    width: 200px;
    height: 100px;
    border: 2px solid black;
    margin: 10px;
    padding: 10px;
}
```

```jsx
var div = document.getElementById('div');
console.log(div.offsetWidth); // 224
console.log(div.offsetHeight); // 124
```
