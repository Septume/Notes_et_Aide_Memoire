# Les évènements

Les événements correspondent à des actions de l'utilisateur via la souris ou le clavier et permettent de conditionner l'exécution du code JS (Programmation événementielle)

## **Liste des évènements principaux**

- `click` : cliquer sur l'élément
- `dbclick` : double-cliquer sur l'élément
- `mouseover` : faire entrer le curseur sur l'élément
- `mouseout` : faire sortir le curseur sur l'élément
- `mousedown` : appuyer (sans relâcher) sur le bouton souris sur l'élément
- `mouseup` : relâcher le bouton souris sur l'élément
- `mousemove` : faire déplacer le curseur sur l'élément
- `keydown` : appuyer (sans relâcher) sur une touche du clavier sur l'élément
- `keyup` : relâcher une touche du clavier sur l'élément
- `keypress` : frapper sur une touche du clavier sur l'élément correspondant à un caractère
- `focus` : cibler l'élément
- `blur` : annuler le ciblage de l'élément
- `change` : changer la valeur d'un élément de formulaire (se déclenche lorsque l'élément qui a été modifié perd le focus)
- `input` : modifier la valeur d'une zone de saisie d'un formulaire (se déclenche à chaque modification de valeur.)
- `select` : sélectionner le contenu d'un champ texte ou une zone de texte d'un formulaire
- `submit` : envoyer le formulaire (spécifique à l'élément form)
- `reset` : réinitialiser le formulaire (spécifique à l'élément form)
- `load` : quand le chargement de la page web est entièrement terminé (toutes les ressources externes comme les images, CSS, etc. sont chargées)

Ordre des évènements :

- clic de souris : `mousedown` -> `mouseup` -> `click`
- double clic de souris : `mousedown` -> `mouseup` -> `click` -> `dbclick`
- survol du curseur : `mouseover` -> `mousemove` -> `mouseout`. L'événement `mousemove` se déclenche à chaque mouvement de souris sur l'élément
- frappe d'une touche correspondant à un caractère : `keydown` -> `keypress` -> `keyup`
- frappe d'une autre touche : `keydown` -> `keyup`. S’il y a un appuie prolongé, l'événement `keydown` est déclenché plusieurs fois

Remarque :

- `keypress` permet uniquement de capter les touches écrivant un caractère. Son avantage est de pouvoir détecter les combinaisons de touches. Par exemple si on tape MAJ + A, ce sera un A majuscule qui sera détecté, alors que pour `keyup` et `keydown`, ces derniers seront déclenchés deux fois, une par la touche MAJ et l'autre par la touche A
- `keyup` et `keydown`: si la touche est un caractère celui-ci sera toujours retourner en majuscule.
- le ciblage d'un élément (focus) peut se faire en cliquant dans un champ de texte, ou en utilisant la touche tab du clavier. Lorsqu'un élément est ciblé, il va recevoir tous les événement du clavier.

**Attention : Certains événements ( `mousemove`, `click`, etc.) déclenchés sur un élément parent, se déclenchent également sur ses éléments enfants.**

## **Utiliser les évènements directement dans le code html**

On utilise en attribut de la balise le nom de de l'événement précédé de "on". Par exemple `onclick` pour un événement `click`. Cet attribut a pour valeur le code JS à exécuter.

```html
<p onclick="alert('Vous avez cliqué !');">Cliquez-moi !</p>
```

L 'instruction `return false`, permet de bloquer le comportement par défaut d'un événement.

```html
<!-- le comportement par défaut (redirection tout en haut de la page web via le "#") est bloqué par le return false.
Cela permet de créer un lien uniquement pour lui attribué un événement -->

<a href="#" onclick="alert('Vous avez cliqué !'); return false;">Cliquez-moi !</a>
```

## **Les évènements avec le dom-0**

Ancienne manière de gérer les évènements. On utilise le nom de l'évènement (avec le préfixe "on") comme propriété de l'élément à laquelle on affecte une fonction. On peut indiquer le nom d'une fonction (sans les parenthèses) ou une fonction anonyme

```html
 <a href="#" id="lien">Cliquez-moi !</a>
```

```jsx
lien.onclick = function () {
    this.textContent = "Vous avez cliqué !";
    return false; // bloque le comportement par défaut
};
```

Pour annuler il faut affecter une fonction anonyme vide

```jsx
lien.onclick = function (){};
```

## **Utiliser un gestionnaire d'évènement (dom-2)**

On utilise la méthode `addEventListener()` sur l'élément cible de l'évènement. Cette méthode prend 2 paramètres obligatoires et 1 paramètre facultatif

- le nom de l'évènement entre guillemets
- le nom d'une fonction à exécuter (sans les parenthèses, afin qu'elle ne soit exécutée qu'au moment du déclenchement de l'évènement) ou directement une fonction anonyme (qui sera exécutée par le gestionnaire d'évènement)
- facultatif : un booléen qui spécifie si on souhaite utiliser la phase de capture (`true`) ou la phase de bouillonnement (`false`). Par défaut : `false`

Remarque : il est possible d'utiliser plusieurs gestionnaires d'évènements pour le même élément et le même type d'évènement.

Pour supprimer un gestionnaire d'évènement on utilise la méthode `removeEventListener()` qui prend les même paramètres que la méthode `addEventListener()`. Dans ce cas, la fonction utilisée ne peut pas être anonyme

```html
<p id="elt">Cliquez moi !</p>
```

```jsx
var element = document.getElementById("elt");

function mouseOver() {
    /* le survol avec le curseur de la souris
	met le texte en rouge souligné */
    element.style.textDecoration = "underline";
    element.style.color = "red";
}

function mouseOut() {
    /* le retrait du curseur remet
	le style par défaut */
    element.style.textDecoration = "none";
    element.style.color = "black";
}

element.addEventListener("mouseover", mouseOver);
element.addEventListener("mouseout", mouseOut);

element.addEventListener("click", function () {
    /* le clic change le contenu du texte,
	met le texte en rouge non souligné
	et supprime les gestionnaires précédents
	(le survol de la souris n'a plus défait
	une fois l'élément cliqué) */
    element.textContent = "Vous avez cliqué !";
    element.style.textDecoration = "none";
    element.style.color = "red";
    element.removeEventListener("mouseover", mouseOver);
    element.removeEventListener("mouseout", mouseOut);
});
```

### **Propagation des évènements**

Quand un évènement est créé, ce dernier se propage dans l'arbre DOM en deux phases :

1. phase de capture (capture) : l'évènement se propage du nœud `Document` jusqu'au nœud cible (élément à l'origine de l'évènement)
2. phase de bouillonnement (bubbling) : l'évènement se propage du nœud cible jusqu'au nœud `Document`

Par défaut, `addEventListener()` capte l'évènement lors de la phase de bouillonnement.

```html
<div id="div">
	<p id="p">Cliquez ici</p>
</div>
```

```jsx
// phase de bouillonnement

var div = document.getElementById("div");
var p = document.getElementById("p");

div.addEventListener("click", function () {
    console.log("évènement du div");
});

p.addEventListener("click", function () {
	console.log("évènement du p");
});

/* 
Lors du clic, affiche :
évènement du p
évènement du div
*/

```

Le paramètre optionnel `true` permet de capter l'évènement lors de la phase de capture

```jsx
// phase de capture 

var div = document.getElementById("div");
var p = document.getElementById("p");

div.addEventListener("click", function () {
    console.log("évènement du div");
}, true);

p.addEventListener("click", function () {
    console.log("évènement du p");
}, true);

/* 
Lors du clic, affiche :
évènement du div
évènement du p
*/

```

### **Objet event**

Le déclenchement d'un évènement s'accompagne de la création d'un objet `Event`  
. Ce dernier permet d'obtenir des informations sur cet évènement. ( touches enfoncées, coordonnées du curseur, élément ayant déclenché l’évènement, etc…)

Pour accéder à cet objet il faut utiliser un paramètre (avec un nom au choix, en général on utile "e") à passer dans la fonction qui sera exécutée. Ce paramètre permet de récupérer la référence vers l'objet `Event`

Remarque : l'objet `Event` peut aussi être utilisé avec l'ancienne méthode du DOM-0

```html
<button id="bouton">Cliquez-moi !</button>
```

```jsx
var bouton = document.getElementById("bouton");
bouton.addEventListener("click", function (e) {
    alert("Vous avez cliqué !");
	console.log(e.type); // affiche le type de l'évenement (click)
});
```

### **Propriétés**

**Tous les évènements**

`type` : renvoie le type de l'évènement

`target` : renvoie la cible de l'évènement (l'élément qui a déclenché l'évènement)

`currentTarget` : renvoie l'élément qui est à l'origine de l'évènement (celui auquel est attaché le gestionnaire d'évènement)

`relatedTarget` : renvoie la cible secondaire de l'évènement. Par exemple pour un évènement focus, l'élément `target` est celui qui reçoit le focus et l'élément `relatedTarget` celui qui perd le focus.  
Pour les évènements qui n'ont pas de cible secondaire, renvoie la valeur `null`

Exemple 1

```html
<div id="div">
    <p id="p">Cliquez ici</p>
</div>
```

```jsx
var div = document.getElementById("div");

div.addEventListener("click", function (e) {
    console.log(e.type); // click
    console.log(e.target); // <p id="p">
    console.log(e.currentTarget); // <div id="div">
});
```

Exemple 2

```html
<div id="p" style="width: 100px; background-color: red">Survolez moi !</div>
```

```jsx
var p = document.getElementById("p");

p.addEventListener("mouseover", function (e) {
    console.log("évènement : " + e.type);
    console.log("élément d'entré : " + e.target);
    console.log("élément de sorti : " + e.relatedTarget);
    console.log();
});

p.addEventListener("mouseout", function (e) {
    console.log("évènement : " + e.type);
    console.log("élément de sorti : " + e.target);
    console.log("élément d'entré : " + e.relatedTarget);
    console.log();
});

/*
évènement : mouseover
élément d'entré : [object HTMLParagraphElement]
élément de sorti : [object HTMLHtmlElement]

évènement : mouseout
élément de sorti : [object HTMLParagraphElement]
élément d'entré : [object HTMLHtmlElement]
*/

```

**Évènements clavier**

`key` : renvoie la valeur de la touche sous la forme d'une chaine de caractère

`altKey` : teste si la touche `alt` a été pressé

`ctrlKey` : teste si la touche `ctrl` a été pressé

`shiftKey` : test si la touche `maj` a été pressé

`repeat` : test si la touche est maintenue enfoncée de sorte qu'elle se répète automatiquement.

**Évènement souris**

`Event.clientX` : permet de récupérer la position horizontale du curseur (par rapport au coté gauche du navigateur)

`Event.clientY` : permet de récupérer la position verticale du curseur (par rapport au haut du navigateur)

`Event.pageX` : permet de récupérer la position horizontale du curseur (par rapport au coté gauche de la page Web)

`Event.pageY` : permet de récupérer la position verticale du curseur (par rapport au haut de la page Web)

Remarque : Les propriétés `Event.pageX` et `Event.pageY` prennent en compte le défilement horizontal ou vertical de la page. Par exemple si on scroll de 200px vers le bas de la page et que l'on clique à 100px vers le bas, la valeur envoyée par `pageY` sera de 300.

`Event.button` : renvoie un code numérique correspondant au bouton utilisé

- 0 : gauche
- 1 : milieu
- 2 : droit

### Stopper la propagation des évènements

La propagation des évènements peut être interrompue en appelant la méthode `stopPropagation()` sur l'objet `Event`

```html
<div id="div">
    <p id="p">Cliquez ici</p>
</div>
```

```jsx
var div = document.getElementById("div");
var p = document.getElementById("p");

div.addEventListener("click", function () {
    console.log("évènement du div");
});

p.addEventListener("click", function (e) {
    console.log("évènement du p");
    // on stoppe la propagation
    e.stopPropagation();
});

/* 
Lors du clic sur le texte, affiche :
évènement du p
*/
```

### **Comportement par défaut des évènements**

La plupart des évènement ont un comportement par défaut. Par exemple :

- click sur un lien => déclenche la navigation vers la cible du lien
- click sur le bouton droit => affichage du menu contextuel

Il est possible d'annuler ce comportement par défaut en appelant la méthode `preventDefault()` sur l'objet `Event`

```html
<p><a href="http://siteinterdit.tld" id="interdit">Lien interdit</a></p>
```

```jsx
document.getElementById("interdit").addEventListener("click", function (e) {
    e.preventDefault();
    alert("Lien interdit !");
});
```

Remarque : Sauf cas particulier, il est fortement déconseillé de modifier le comportement standard des évènements.

### **Fin du chargement des ressources de la page web**

Dans certains cas il est important que le code JS ne puisse être exécuté que si toutes les ressources de la page Web (image, CSS etc…) ont fini d'être chargées.  
Pour cela on utilise évènement `load` sur l'objet `window`

```jsx
window.addEventListener("load", function () {
    console.log("La page est complètement chargée");
    /* code JS à exécuter */
});
```
