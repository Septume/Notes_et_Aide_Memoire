# Conditions et boucles

## Opérateurs

### **Opérateurs de comparaison**

- `==` : égal à (avec conversion de type implicite)
- `===` : contenu et type égal à (pas de conversion de type) [Recommandé]
- `!=` : différent de (avec conversion de type implicite)
- `!==` : contenu et type différent de (pas de conversion de type) [Recommandé]
- `>` , `>=` , `<` , `<=`

### **Opérateurs logiques**

- `&&` : ET
- `||` : OU
- `!` NON

## **Conditions**

### **If…else**

```
if (/*CONDITION */) {
	// instructions;
}else if (/*CONDITION */) {
	//instructions;
} else {
	//instructions;
}
```

### **Switch**

Attention : vérifie aussi les types de valeurs

```
switch (variable){
	case valeur1: 
		//instructions; 
break;
	case valeur2: 
        //instructions; 
        break; 
case valeur3: 
        //instructions; 
        break; 
default: // optionnel (permet de gérer les cs d'erreurs)
        //instructions; 
}
		
```

### **Les ternaires**

```
variable = (condition) ? valeur : valeur
```

Si la condition est vrai, la valeur se trouvant après le " ?" est affectée, sinon c'est la valeur se trouvant après le " : "

### **Test sur les variables**

Il est possible de tester si une variable à une valeur sans passer par `typeof()` en la convertissant en booléen avec une condition (la condition vaut `true` si la variable possède une valeur)

Exemple

```jsx
let texte = "Hello World";
if (texte){
	console.log("valeur : oui");// condition juste 
}else{
	console.log("valeur : non");
}
```

Les valeurs suivantes sont testé comme false :

- 0
- chaîne de caractères vide ("")
- `NaN`
- `undefined`
- `null`

L'opérateur OU permet également de renvoyer la première variable possédant une valeur évaluée à `true`

```jsx
let variable1 = ""
let variable2 = "Hello World"; 
console.log(variable1 || variable2); // affiche : Hello World
```

## **Boucles**

### **While**

```
while (CONDITION){
	// instructions;
}
```

### **Do…while**

```
do {
	// instructions;
} while (CONDITION);
```

### **For**

```
for ( INITIALISATION; CONDITION, INCREMENTATION) {
	// instructions; 
}
```

Exemple

```jsx
let tab = ["pim", "pam", "poum"];
for (let i = 0; i < tab.length; i++){
  console.log(tab[i]);
}
```

### For…of (spécification es6)

Permet de parcourir un tableau ou tout autre objet itérable. On utile pour cela une variable qui sert d' identifiant pour chaque éléments du tableau ou de l'objet

```
for (let variable of tableau) {
  // instructions
}
```

Exemple

```jsx
var tab = ["pim", "pam", "poum"];
for (let item of tab) {
  console.log(item);
}
```

### For…in

Permet de parcourir les propriétés d'un objet

```
for (let variable in objet) {
  // instructions
}
```

Attention : il ne faut pas utiliser `for…in` sur les tableaux

### **Break et continue**

`break` : mot clé permettant de sortir d'une boucle alors que celle-ci est encore vrai et exécute le code suivant

`continue` : mot clé permettant de mettre fin à l'itération en cours et de passer à l'itération suivante (la boucle n'est pas stoppé)
