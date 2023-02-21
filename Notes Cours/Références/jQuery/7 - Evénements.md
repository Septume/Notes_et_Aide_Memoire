# Evénements

### **Gestionnaire d'événements**

Pour gérer les événement on utilise la méthode `on()` qui prend en paramètre :

- le nom de l'événement (type string)
- une fonction anonyme à exécuter (où on peut utiliser l'objet `Event`)

`on('click', function(){ }`

### **Gérer plusieurs événements avec la même méthode**

Pour cela on indique en 1er argument la liste des événements séparer par un espace

```jsx
$('button').on('mouseover mouseout click', function () {
    console.log('événement déclenché');
});
```

Pour indiquer une fonction différence pour chaque événement il faut indiquer en argument de `on()` un objet ayant pour propriétés les événements à utiliser et pour valeur les fonctions anonyme à exécuter

```jsx
$('button').on({
    mouseover: function () {
        console.log('la souris est entré sur l\'élément')
    },
    mouseout: function () {
        console.log('la souris est sorti de l\'élément')
    },
    click: function () {
        console.log('vous avez cliqué')
    }

});
```

### **Filtrer les éléments descendants qui déclenchent l'évènement**

On indique en paramètre le ou les éléments descendant sur lesquels l'événement sera déclenché

```html
<div id="exterieur" style="height: 200px; width: 200px; background-color: red">
    <div id="interieur" style="height: 100px; width: 100px; background-color: green">
    </div>
</div>
```

```jsx
/* Bien que l'événement est écouté sur la div extérieure
ce dernier sera déclenché que lors d'un click sur
la div intérieure */

$('#exterieur').on('click', '#interieur', function () {
	/* this fait référence à l'élément descendant filter
	le carré intérieur devient bleu au click */
	$(this).css('background-color', 'blue');
});

```

### **Forcer le déclenchement d’un évènement**

On utilise une des méthodes qui prend en argument le nom d'un événement

`trigger()` : s'exécute pour tous les éléments possédant les caractéristiques ciblées et déclenche également le comportement par défaut de l'événement

`triggerHandler()` : s'exécute que pour le premier élément ciblé et ne déclenche pas le comportement par défaut de l'événement

```jsx
/* le clic sur le bouton 
déclenche l'événement focus sur le input 
Le champ reçoit immédiatement le focus 
(comportement par défaut)
*/

$('button').on('click', function () {
	$('#input').trigger('focus');
});
```

### **Supprimer un gestionnaire d'évènement**

On utilise la méthode `off()` qui prend comme argument le nom de l'événement à supprimer.

On peut omettre l'argument. Dans ce cas c'est tous les événements attachés à l'élément qui sont supprimé

Utiliser sans argument => supprime tous les gestionnaires d'évènement attachés à un élément

```jsx
var $p = $('p');

$p.on({
    click: function () {
        $p.text('Vous avez cliquez ! ');
        /* desactive   evenement click */
        $p.off('click');
    },
    mouseover: function () {
        $p.css('color', 'red');
    },
    mouseout: function () {
        $p.css('color', 'black');
    }

});
```
