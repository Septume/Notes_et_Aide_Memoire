# Objet littéral

## Créer un objet

Les propriétés doivent être séparées par des virgules
Remarque : En JavaScript, les méthodes sont considérées comme des propriétés.

```
var objet = {
	propr1: valeur,
	propr2: valeur,
	propr3: valeur,
	methode1: function(){},
	methode2: function(){}
};

// création d'un objet vide
var objet = {};

```

Depuis ES6, il existe une syntaxe plus courte pour les méthodes

```
var objet = {
	methode1(){},
	methode2(){}
};
```

Pour accéder à une propriété: `objet.propriété;`

Pour appeler une méthode : `objet.methode()`

Mot clé `this` : représente l'objet en cours, sur lequel on peut appliquer une propriété ou une méthode

Exemple :

```jsx
var personne = {
    nom: "Dupont",
    prenom: "Jean",
    age: 45,
    adresse: {//objet
        rue: "10 rue de la paix",
        codePostal: "75000",
        ville: "Paris"
    },
    decrire() { // remarque : on peut utiliser des paramètres
	    return `${this.prenom} ${this.nom} - ${this.age} ans`;
    },
    afficherAdresse() {
        return `adresse : ${this.adresse.rue}, ${this.adresse.codePostal} ${this.adresse.ville}`;
    }
};
console.log(personne.decrire()); // "Jean Dupont - 45 ans"
console.log(personne.afficherAdresse()); // "adresse : 10 rue de la paix, 75000 Paris"
console.log(personne.toString()); // La méthode toString() est héritée
```

On peut parcourir un objet avec une boucle `for…in`. On utile pour cela une variable qui sert d' identifiant pour chaque propriétés (méthodes comprises) de l'objet

```jsx
for (var i in personne){
    console.log(personne[i]);

```

Le mot clé `instanceof` permet de tester si une variable est une instance d'un objet

### Créer un objet à partir d'un autre objet

Utilisation de la méthode `Object.create()`

```jsx
// definition d'un objet
var personne = {
    nom: "Dupont",
    prenom: "Jean",
    age : 45,
    decrire() {
        return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans";
        }
};

// Définition d'un nouvelle objet à partir de l'objet personne
var personne2 = Object.create(personne);

console.log(personne2.nom); // affiche : Dupont (propriété trouvée dans le prototype "personne")
```

On peut ainsi définir un prototype qui sert de modèle pour créer des objets. Par convention son nom commence par une majuscule

```jsx
// définition d'un prototype 
var Personne = {
    nom: "",
    prenom: "",
    age : 0,
    decrire {
	    return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans";
	}
};

// création d'une première personne 
var personne1 = Object.create(Personne);
personne1.nom = "Dupont";
personne1.prenom = "Jean";
personne1.age = 45;
console.log(personne1.decrire());

// création d'une deuxième personne 
var personne2 = Object.create(Personne);
personne2.nom = "Gauthier";
personne2.prenom = "Marie";
personne2.age = 38;
console.log(personne2.decrire());

```

Il peut être utile de créer une méthode permettant l’initialisation des propriétés d'un objet. Celle-ci prend en paramètre les valeurs initiales des propriétés.

```jsx
// définition d'un prototype 
var Personne = {
    // méthode d'initialisation
    init: function(nom,prenom,age) {
        this.nom = nom;
        this.prenom = prenom;
        this.age = age;
    },
    decrire: function() {
        return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans";
    }
};

// création et initialisation d'une première personne
var personne1 = Object.create(Personne);
personne1.init("Dupont","Jean", 45);
console.log(personne1.decrire());

// création et initialisation d'une première personne
var personne2 = Object.create(Personne);
personne2.init("Gauthier","Marie", 38);
console.log(personne2.decrire());

```

Pour créer des sous prototypes à partir d'un prototype

```jsx
//prototype Personne 
var Personne = {
    initPersonne: function (nom, prenom, age) {
        this.nom = nom;
        this.prenom = prenom;
        this.age = age;
    }
};

//sous Prototype Adulte
var Adulte = Object.create(Personne);
Adulte.initAdulte = function (nom, prenom, age, profession) {
    this.initPersonne(nom, prenom, age);
    this.profession = profession;
};
Adulte.decrire = function () {
    return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans - Profession : " + this.profession;
};

// sous Prototype enfant
var Enfant = Object.create(Personne);
Enfant.initEnfant = function (nom, prenom, age, classe) {
    this.initPersonne(nom, prenom, age);
    this.classe = classe;
};
Enfant.decrire = function () {
    return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans - classe : " + this.classe;
};

// création et inialisation de deux objets Adulte
var adulte1 = Object.create(Adulte);
adulte1.initAdulte("Dupont", "Jean", 45, "informaticien");
var adulte2 = Object.create(Adulte);
adulte2.initAdulte("Gauthier", "Marie", 38, "medecin");
console.log(adulte1.decrire());
console.log(adulte2.decrire()); 

// création et inialisation d'un objet Enfant
var enfant1 = Object.create(Enfant);
enfant1.initEnfant("Dupuis", "Louise", 10, "CM2");
console.log(enfant1.decrire
```
