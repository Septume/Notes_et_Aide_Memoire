# Les formulaires

### **Propriétés et méthodes de l'élément form**

### **Propriétés**

`elements` : renvoie la liste des champs du formulaire. (dans l'ordre sur la page). On peut ensuite accéder à un champ via son indice ou en utilisant une propriété dont le nom correspond à la valeur de l'attribut `name` du champ.

```html
<form id="formulaire">
    <label for="pseudo">Pseudo</label> : 
	<input type="text" name="pseudo" id="pseudo">
</form>
```

```jsx
// affiche "pseudo" (valeur attribut name)
console.log(document.getElementById("formulaire").elements[0].name); 

// affiche l'objet ayant "pseudo" comme valeur de l'attribut name
console.log(document.getElementById("formulaire").elements.pseudo);
```

### **Méthodes**

`submit()` : envoie le formulaire sans l'intervention de l'utilisateur. Attention cette méthode ne déclenche pas l'événement `submit`

`reset()` : réinitialise le formulaire. Même fonctionnement que `submit()`

### **Propriétés et méthodes des éléments de formulaire**

### **Propriétés**

`value` : accès et modification de la valeur de l'attribut `value` ainsi que du contenu d'un élément `textarea`

`disabled` : accès et modification de la valeur de l'attribut booléen `disabled` ( `true` ou `false`)

`checked` : accès et modification de la valeur de l'attribut booléen `checked`

`readonly` : accès et modification de la valeur de l'attribut booléen `readonly`

`options` : liste dans un tableau les éléments d'une liste déroulante

`selectedIndex` : renvoie l'index de la valeur sélectionnée dans une liste déroulante

### **Méthodes**

`focus()` : donne le focus sur l'élément

`blur()` : enlève le focus de l'élément

`select()` : sélectionne le texte d'un champ `input` ou `textarea`

### **Évènement change**

Rappel : l 'évènement `change` se déclenche que lorsque l'élément qui a été modifié perd le focus

Propriété

- `checked` : teste si la case est coché
- `target.value` : contient la valeur de l'attribut `value` de l’ élément sélectionné (bouton radio, choix liste déroulante…)

### **Validation des données saisies**

Le contrôle peut se faire :

- pendant la saisie d'une donnée via l'événement `input` (modification de la valeur d'un champ textuel pendant la saisie)
- à la fin de la saisie d'une donnée via l'événement `blur` (perte du focus)
- au moment de la soumission du formulaire via l'événement `submit`. On peut également annuler l'envoi en appelant la méthode `preventDefault()` sur l'objet `Event` associé à l'événement
