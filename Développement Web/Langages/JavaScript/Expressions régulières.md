# Expressions régulières

### **Syntaxe**

Une regex est délimitée par des caractères d'encadrement. On utilise en général le slash.

`/regex/`

Pour décrire une regex on utilise des caractères spéciaux appelés métacaractères

`! ^ $ ( ) { } ? + * . / \ |`

Si un de ces caractères se trouvent dans l'expression à chercher, il faut penser à l'echapper avec un anti-slash (ce dernier compris)

### **Opérateurs**

- `^expr` : Expression en début de chaine
- `expr$` : Expression en fin de chaine
- `(expr1 | expr2)` : *expr1* ou *exp2* (on peut utiliser plus de 2 possibilités)
- `[abc]` : Expression qui inclus un des caractères
- `[^abc]` : Expression qui exclus un des caractères
- `[a-z]` : Expression qui inclus un lettre minuscule compris dans l'intervalle.
- `[A-Z]` : Expression qui inclus une lettre majuscule compris dans l'intervalle
- `[0-9]` : Expression qui inclus un chiffre compris dans l'intervalle
- `[^a-z]` : Expression qui exclus une lettre minuscule compris dans l'intervalle
- `.` : Un caractère quelconque (excepté un caractère de saut de ligne)
- `a?` : Caractère qui est répété 0 ou 1 fois
- `a+` : Caractère qui est répété 1 ou plusieurs fois
- `a*` : Caractère qui est répété 0, 1 ou plusieurs fois"
- `a{n}` : Caractère qui est répété n fois
- `a{n,m}` : Caractère qui est répété de n à m fois
- `a{n,}` : Caractère qui est répété au moins n fois

Remarque :

- les opérateurs peuvent être combinées
- on peut chainer les intervalles de caractères. Par exemple : `[a-zA-Z] [a-z0-9]`
- Une intervalle comme `[a-z]` ne prend pas en compte les caractères accentuées. Il faut donc les indiquées avec l'intervalle `[a-zâäàéèùêëîïôöçñ]`

Exemple pour une adresse mail :  
`/^[a-z0-9._-]+@[a-z0-9._-]+\.[a-z]{2,6}$/`

### **Les options**

On peut également ajouter à la suite de la regex une ou plusieurs options :

- `i` : ignorer la casse
- `g` : faire une recherche globale (plutôt que de s’arrêter au premier résultat trouvé, on va chercher tous les résultats disponibles)
- `m` : faire une recherche sur plusieurs lignes. Permet de prendre en compte les retours à la ligne comme la fin d'une première chaine et le début d'une autre.

`/regex/igm`

### **Objet regexp**

Instanciation : `var variable = /regex/options;`

méthodes

- `test()` : teste si le motif est présent dans une chaine de caractères indiquée en paramètre.
- `exec()` : cherche le motif dans une chaine de caractères indiquée en paramètre. Retourne la chaine trouvée ou le cas échéant la valeur null

```jsx
var chaine = "Mangez des POMMES !";
console.log(/pommes/.test(chaine)); // false
console.log(/pommes/i.test(chaine)); // true
console.log(/pommes/.exec(chaine)); // null 
console.log(/pommes/i.exec(chaine)); // POMMES
```

### **Utilisation avec des méthodes de l'objet string**

`match()` : retourne un tableau contenant toutes les occurrences correspondant au motif. Si l'option g n'est pas indiqué, retourne que la première occurrence. Si aucune occurrence est trouvé, retourne null

`search()` : retourne la position de la première occurrence ou -1 si aucune occurrence est trouvée.

`split()` : découpe la chaine selon un motif

`replace()` : remplace une sous-chaine correspondant à une motif par une autre chaine.

```jsx
var chaine = "Mangez des pommes ! Mangez des POMMES ! ";
var regex = /pommes/ig;
console.log(chaine.match(regex)); // Array [ "pommes", "POMMES" ]
console.log(chaine.search(regex)); // 11
var chaine2 = chaine.replace(regex, "bananes");
console.log(chaine2); // // Mangez des bananes ! Mangez des bananes !
console.log(chaine2.search(regex)); // - 1
```
