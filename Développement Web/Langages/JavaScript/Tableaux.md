
# Tableaux

Caractéristiques des tableaux (Array) en JavaScript :

- Les tableaux sont des objets
- Les éléments d'un tableau peuvent être de type différents
- Les tableaux n'ont pas de taille prédéfinie
- Il n'existe pas de tableaux associatifs. (On peut utiliser à la place des objets littéraux, mais qui ne sont pas spécifiquement des tableaux)

## **Déclaration et initialisation**

- Déclarer un tableau : `let variable = [valeur1, valeur2, valeur3,…];`
- Déclarer un tableau vide : `let variable = [];
- Retourner un élément du tableau : `variab[indice]`
- Affecter valeur : `variable[indice] = valeur;` . Si l'indice n'existe pas, renvoie => `undefined`
- Afficher la taille du tableau : `variable.length`
- Tableau multidimensionnel :`let variable = [[valeur1,…],[valeur1,…]…];`

## Parcourir et afficher un tableau

Pour parcourir le tableau on peut utiliser :

- une boucle for classique
- une boucle for…of (spécification ES6)

```jsx
let tab = ["pim", "pam", "poum"];

/* for classique */
for (let i = 0; i < tab.length; i++){
  console.log(tab[i]);
}

/* for...of */
for (let item of tab) {
  console.log(item);
}
```

Pour tester si une variable est in tableau : `Array.isArray(variable)`. Retourne un booléen

```jsx
let tab = ["pim", "pam", "poum"];
console.log(typeof tab); // object
console.log(Array.isArray(tab)); //true
```


## Méthodes itérateurs

### **Méthode foreach()**

Pour exécuter une fonction sur chaque élément d'un tableau  

On utile une fonction callback qui prend en paramètre (dans l'ordre ) :
- une variable donc la valeur correspond à l'élément du tableau en cours de traitement
- une variable correspondant à l'indice de l'élément en cours de traitement (facultatif)
- une variable qui représente le tableau sur lequel la méthode est appliquée. (facultatif)

```jsx
let tab = ["pim", "pam", "poum"]; 
console.log(tab); // ["pim", "pam", "poum"]

tab.forEach((item, index, tab)=> {
  tab[index] = item.toUpperCase();
});
console.log(tab); // ["PIM", "PAM", "POUM"]
```

### Méthode map()

Pour exécuter une fonction sur chaque élément d'un tableau et retourner le résultat dans un nouveau tableau.

On utile une fonction callback avec les même paramètres que celle pour la méthode `forEach()`. Cette fonction doit retourner comme valeur l'élément modifié

```js
let tab = ["pim", "pam", "poum"]; 
let tabCopy = tab.map(item => item.toUpperCase());

console.log(tabCopy); // ["PIM", "PAM", "POUM"]
```

```js
let users = [
  {
    name: "John",
    age: 45,
  },
  {
    name: "Peter",
    age: 38,
  },
  {
    name: "Patrick",
    age: 44,
  },
];

/* récupérer tout les noms d'utilisateurs */
const names = users.map( user => user.name);
```

### Méthode filter()

Pour exécuter une fonction de test sur chaque élément d'un tableau. Les éléments qui remplisse la condition sont retourner dans un nouveau tableau.

On utile une fonction callback avec les même paramètres que celle pour la méthode `forEach()`
Cette fonction doit retourner un booléen comme résultat du test.

```js
let tab = ["pim", "pam", "poum", "pimpampoum"];
console.log(tab); // ["pim", "pam", "poum", "pimpampoum"]
let tabCopy = tab.filter(item => item.length <= 6);
console.log(tabCopy); // ["pim", "pam", "poum"]
```

### Méthode find() et findIndex()

Pour exécuter une fonction de test sur chaque élément d'un tableau. Le premier élément qui remplit la condition est envoyé. 

```js
let tab = ["pim", "pam", "poum", "pimpampoum"];
console.log(tab); // ["pim", "pam", "poum", "pimpampoum"]
let tabCopy = tab.find(item => item.length <= 6);
console.log(tabCopy); // pim
```

`findIndex()` permet de retourner l'indice plutôt que la valeur

```js
let tab = ["pim", "pam", "poum", "pimpampoum"];
console.log(tab); // ["pim", "pam", "poum", "pimpampoum"]
let tabCopy = tab.findIndex((item) => item.length <= 6);
console.log(tabCopy); // 0
```

### Méthode some()

Permet d'exécuter une fonction de test sur chaque élément d'un tableau. Si au moins un  élément rempli la condition la méthode arrête de parcourir le tableau et retourne `true`. Sinon la méthode retourne `false`

```js
let tab = ["pim", "pam", "poum"];
let result = tab.some(item => item.length === 3);
console.log(result); // true;
```


### Méthode every()

Pour exécuter une fonction de test sur chaque élément d'un tableau. Si un seul élément ne rempli pas la condition la méthode arrête de parcourir le tableau et retourne `false`. Sinon la méthode retourne `true`. 

```js
let tab = ["pim", "pam", "poum"];
let result = tab.every(item => item.length === 3);
console.log(result); // false;
```



## Accesseurs

Ces méthodes ne modifient pas le tableau

`toString()` : Affiche les éléments d'un tableau forme de chaine de caractères (chaque élément est séparé par une virgule)

`includes(valeur, indice)` : Vérifie si un élement se trouve dans le tableau. Retourne un booléen. On peut indiquer comme deuxième argument facultatif un indice à partir duquel commencer la recherche. (La valeur peut-être négative)

`indexOf(valeur, indice)` : Cherche un élément dans le tableau et renvoi l'indice de la première occurrence trouvée. Si l'élément n'est pas trouvé, la méthode retourne `-1`. Le deuxième argument facultatif permet de chercher à partir d'un indice.

`lastIndexOf(valeur, indice)` : Idem mais en envoyant l'indice de la dernière occurrence trouvée.

`concat(valeur1,…)` : Pour concaténer plusieurs tableaux. On peut indiquer en paramètre un tableau ou une valeur. Retourne un nouveau tableau. Remarque : si on utilise à la place l'opérateur + pour concaténer des tableaux, cela créer une chaîne de caractères contenant tous les éléments des tableaux

`slice(indiceA, indiceB)` : Retourne une sous-tableau contenant les élément de l'indice A (inclus) à l'indice B (exclus). On peut utiliser des valeurs négatives.

## Mutateurs

Ces méthodes modifient le tableau

`push(valeur1, valeur2,…)` : Ajoute un ou plusieurs élément à la fin du tableau. Retourne la nouvelle taille du tableau

`pop()` : Supprime le dernier élément du tableau. Retourne la valeur supprimée sous forme de chaîne de caractère.

`unshift(valeur1, valeur2,…)` : Ajoute un ou plusieurs éléments au début du tableau. Retourne la nouvelle taille du tableau

`shift()` : Supprime le premier élément du tableau. Retourne la valeur supprimée sous forme de chaîne de caractère.

`sort()` : Trie le tableau par ordre croissant. Attention : les valeurs commençant par des majuscules seront classés avant celles qui commencent par des minuscules. De plus la méthode va classer les valeurs en les comparant caractère par caractère. Par exemple 25 sera considéré comme supérieur à 100 car le nombre commence par un 2 qui est supérieur à 1

`splice(indice, nombre, element1, element2…)` : Ajoute ou supprime des éléments dans un tableau. les arguments sont :

- Un indice à partir duquel commencer les modifications. ( On peut utiliser un valeur négative ce qui permet de compter à partir de la fin du tableau)
- Un entier indiquant le nombre d'élément à supprimer. `0` pour supprimer aucun élement.
- Les autres arguments sont les éléments à ajouter (Facultatif)

```jsx
let liste = ['pomme', 'poire', 'banane'];
console.log(liste); // ["pomme", "poire", "banane"]
liste.splice(2, 1, 'pêche', 'orange');
console.log(liste); //["pomme", "poire", "pêche", "orange"]
```


