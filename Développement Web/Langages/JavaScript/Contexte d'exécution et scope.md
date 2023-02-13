# Contexte d'exécution et scope

## Fonctionnement

Un contexte d'exécution est créé à chaque fois qu'on exécute une fonction. Le code n'appartenant pas à une fonction fait parti d'un contexte d'exécution globale

3 étapes :

- Création du contexte d'exécution
- Exécution ligne par ligne du code associé au contexte.
- Destruction du contexte d'exécution.

Un contexte d'exécution est composé de :

- de l'objet des variables (variables object) => Cet objet est créé et initialisé pendant la phase de création du contexte d'exécution. Il contient les variables (paramètres compris) et fonctions déclarés dans ce contexte.
- Chaine des scopes => les variables qui sont accessibles au contexte d' exécution.
- La valeur du mot clé `this` => référence vers l'objet qui a exécuté la fonction responsable du contexte d'exécution.

## Portée des variables (scopes)

**Variable locale**

- Si déclarée dans une fonction (paramètres compris) avec un mot clé ( `var`, `let` ou `const`)
- Si déclarée dans une structure de contrôle (condition ou boucle) avec le mot clé `let` ou `const`.  
⇒ Accessible uniquement localement (sinon erreur : `ReferenceError`)

Une bloc interne à une autre bloc, dit externe, a accès aux variables déclarées dans celui ci, ainsi que dans tout bloc "ancêtre". à l'inverse un bloc externe n'a pas accès aux variables déclarées dans ses blocs internes.

**Variable globale**

- Si déclarée en dehors d'une fonction avec le mot clé `var`
- Si déclarée en dehors d'une structure de contrôle avec les mot clé `let` ou `const`
- si déclarée sans mot clé (totalement déconseillé)

⇒ Accessible partout dans le code. Implémentée comme propriété d'un objet `Global` spécial.

|                                | let / const | var (déconseillé) | sans mot clé (totalement déconseillé) |
| ------------------------------ | ----------- | ----------------- | ------------------------------------- |
| Dans une fonction              | locale      | locale            | globale                               |
| Dans une structure de contrôle | locale      | globale           | globale                               |
| Dans le reste du code          | globale     | globale           | globale                               |

Remarque : Les fonctions ont accès aux variables globales. De m̂ême une fonction qui est déclarée à l'intérieur d'une autre fonction a accès aux variables de celle-ci

 Il faut donc faire attention aux éventuels effets de bord lors qu'une fonction utilise une variable globale car celle-ci peut être modifiée ailleurs dans le programme.

## Objet Windows

Au niveau du navigateur, l'objet `window` correspond au scope global.  
Les variables globales sont des propriétés de `window`

Écrire `variable = valeur` revient à écrire `window.variable = valeur`

En dehors du contexte d'un objet défini , `this` fait référence à l'objet global `window`

## Mot clé this

Si la fonction est exécuté par un objet, le `this` pointe vers cet objet. Sinon le `this` pointe vers l'objet global.

```js
function fonction() {
  console.log(this); // l'objet associé à ce contexte d'exécution est l'objet global (window si le code est exécuté dans le navigateur) 
}
fonction(); // affiche : window

let objet = {
  methode() {
    console.log(this); // l'objet associé à ce contexte d'exécution est l'objet user
  },
};
objet.methode(); // affiche le contenu de l'objet "objet"
```

Attention : Dans le cas d'une fonction qui a été exécutée à l'intérieur d'une méthode d'un objet, le mot clé `this` pointe vers l'objet global (car ce n'est pas l'objet qui l'a exécuté mais une méthode)

```js
let objet = {
  methode: function () {
    console.log(this); // affiche l'objet "objet"
    function inside() {
      console.log(this); // affiche l'objet global car ce n'est pas l'objet qui a exécuté cette fonction mais la méthode
    }
    inside();
  },
};

objet.methode();
```

### Méthode bind()

La méthode `bind()` permet de lier une fonction à un objet pour y faire référence avec `this` (La méthode retourne une nouvelle fonction)

```js
let user = {
  name: "Stef",
  sayHello() {
    console.log("Hello " + this.name);
  },
};

user.sayHello(); // Affiche "Hello Stef"

let message1 = user.sayHello;
message1(); // Affiche Hello (car c'est message1() qui a exécuté la méthode sayHello() et non pas l'objet 

let message2 = user.sayHello.bind(user);
message2(); // Affiche Hello Stef

```

La méthode `bind()` permet également de fixer la valeur des arguments de la fonction retournée.

```js
function multiply(num1, num2) {
  console.log(num1 * num2);
}

const multiplyByTwo = multiply.bind(this, 2); // on fixe le premier argument à 2
multiplyByTwo(4); // affiche 8

/* on peut également ecrire " multiply.bind(this, 2)(4)" pour exécuter la fonction sans passer par une variable */
```

### Méthodes call() et apply()

Contrairement à `bind()` la méthode `call()` ne créé par une nouvelle fonction mais exécute directement la fonction

```js
let user = {
  name: "Stef",
  message() {
    function sayHello(before, after) {
      console.log(before + " " + this.name + ", " + after);
    }
    sayHello.bind(user, "Salut", "comment vas-tu ?")(); // la méthode bind retourne une fonction qui doit être exécutée
  },
};
user.message();
```

```js
let user = {
  name: "Stef",
  message() {
    function sayHello(before, after) {
      console.log(before + " " + this.name + ", " + after);
    }
    sayHello.call(user, "Salut", "comment vas-tu ?"); // la méthode call exécute directement la fonction
  },
};

user.message();
```

La méthode `apply()` fait la même chose que la méthode `call()` sauf qu'elle utilise un tableau pour fixer les arguments

```js
let user = {
  name: "Stef",
  message() {
    function sayHello(before, after) {
      console.log(before + " " + this.name + ", " + after);
    }
    sayHello.apply(user, ["Salut", "comment vas-tu ?"]); // la méthode call exécute directement la fonction
  },
};

user.message();
```

### Cas des fonctions fléchées

Fonctionne différemment par rapport au `this` . Lorsqu'une fonction fléchée est exécutée le `this` fait référence au scope parent

```js
let objet = {
  methode: function () {
    let classicFunction = function () {
      console.log(this); // affiche l'objet global
    };
    let arrowFunction = () => {
      console.log(this); // fait référence au scope parent dont à l'objet "objet"
    };
    classicFunction(); 
    arrowFunction();
  },
};

objet.methode();

```
