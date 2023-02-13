# Programmation objet

Rappel : Contrairement aux valeurs primitives, on accède aux objets par référence (et non pas par valeur).

Cela a une incidence lors de :

- l'affichage d'un objet
- la copie d'un objet
- la comparaison de deux objets

## Notion de prototype

JavaScript est un langage orienté prototype. Un prototype est un objet à partir duquel on créé de nouveaux objets qui héritent des propriétés et méthodes de leur prototype. Comme tout les objets héritent d'un prototype, cela créé une chaine de prototypage. Le dernier maillon de cette chaine est un objet dont le prototype vaut `null` . Plus précisément lors qu'on cherche une propriété, celle ci sera recherchée d'abord sur l'objet en lui-même, puis sur son prototype, puis sur le prototype de son prototype et ainsi de suite. De plus les propriétés sont hérités de manière dynamique. Cela signifie que la modification d'un prototype entraine donc une modification immédiate de tout les objets qui ont hérités de ce prototype

Tout les objets ont une propriété `__proto__` qui contient une référence vers son prototype. Cette propriété ne doit pas être utilisé dans le code. A la place on utilise les méthodes :

 `Object.getPrototypeOf(objet)` : qui renvoie le prototype de l'objet indiqué en argument.

`Object.setPrototypeOf(objet,prototype)` : qui modifie le prototype de l'objet indiqué en argument. Le deuxième argument permet de définir le nouveau prototype.

## Objet object

La quasi totalité des objets JS héritent de l'objet `Object` et notamment de la méthode `toString()` qui par défaut, renvoie `[object type]`, où *type* est le type de l'objet. Certains objets natifs surchargent cette méthode pour renvoyer plutôt une chaine de caractères qui représente l'objet.


## Anciennes méthodes de création d'objet

Méthodes obsolètes depuis la spécification ES6

### Utilisation d'une fonction constructeur

```
function NomConstructeur(params,...){
	// instructions; 
}
```

Pour créer une instance :`variable = new NomConstructeur(args,…) ;`

Exemple

```jsx
// constructeur
function Personne(nom, prenom, age) {
    this.nom = nom;
    this.prenom = prenom; 
    this.age = age; 
    this.decrire = function(){
        return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans";
    }
}

//Création objet 
var personne = new Personne("Jean", "Dupont", 54);
console.log(personne.decrire()); // Prénom : Dupont - Nom : Jean - Age : 54 ans
personne.prenom = "pierre"; 
console.log(personne.decrire()); // Prénom : pierre - Nom : Jean - Age : 54 ans
console.log(personne instanceof Personne); // true
```

Pour créer une fonction constructeur qui hérite des propriétés d'une autre

```jsx
function Adulte(nom, prenom, age, profession) {
/* Héritage de Personne */
this.Personne = Personne;
this.Personne(nom, prenom, age);
/* propriétés de Adulte */
    this.profession = profession;
    this.decrire = function(){
        return "Prénom : " + this.prenom + " - Nom : " + this.nom + " - Age : " + this.age + " ans - Profession : " + this.profession;
    }
}

var adulte = new Adulte("Jean", "Dupont", 54, "informaticien");
console.log(adulte.decrire()); // "Prénom : Dupont - Nom : Jean - Age : 54 ans - Profession : informaticien"

```

 `constructor` : Propriété qui retourne une référence vers la fonction constructeur

`constructor.name` : Retourne le nom de la fonction constructeur

### Méthode object.create()

Il est possible de créer un objet à partir d'un autre objet avec la méthode `Object.create()`

```jsx
// definition d'un objet
var personne = {
    nom: "Dupont",
    prenom: "Jean",
    age : 45,
    decrire: function() {
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
    decrire: function() {
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

## Redéfinir un objet

Il est possible de rédéfinir dynamiquement un objet via la propriété `prototype` de son prototype qui permet de créer ou de modifier une propriété

```jsx
class Personne {
  constructor(nom, prenom, age){
    this.nom = nom;
    this.prenom = prenom;
    this.age = age;
  }
  
  info(){
    return `${this.nom} ${this.prenom}`;
	}
}

var personne = new Personne("Dupont","Jean", 40);
console.log(personne.info()); // Dupont Jean

/* ajout d'ube propriété à Personne */

Personne.prototype.getAge = function(){
  return `${this.age} ans`;
}

console.log(personne.getAge()); // 40 ans

/* Modification d'une propriété de Personne */

Personne.prototype.info = function(){
  return `${this.nom} ${this.prenom} - ${this.age} ans`;
}

console.log(personne.info()); // Dupont Jean - 40 ans
```
