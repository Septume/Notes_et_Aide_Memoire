# Classes 

Attention : Malgré l'arriver des classes dans la spécification ES6, JavaScript reste un langage orienté prototype. Par conséquent les classes seront converties par le langage en prototypes.

### Créer une classe

On utile le mot clé `class` suivi d'un nom de classe qui par convention commence par une majuscule

```
class NomClasse {}
```

Pour créer un instance de la classe

```
variable = new NomClasse(arg1, arg2,...)
```

### Constructeur

Méthode qui sera appelée lors de l'instanciation de la classe et qui permet d'initialiser les propriétés de l'objet.

```
class NomClasse {
	constructor(param1, param2,...) {
	}
}
```

Exemple

```jsx
class User {
  constructor(username, name, mail){
    this.username = username;
    this.name = name;
    this.mail = mail;
  }
  
  info(){
    return `Nom : ${this.name} - Mail : ${this.mail}`
	}
}

const mickey = new User("mickey", "Mickey Mouse", "mickey-mouse@mail.tld");
const donald = new User("donald", "Donald Duck", "donald-duck@mail.tld");
```

 `constructor` : Propriété qui retourne une référence vers la classe

`constructor.name` : Retourne le nom de la classe

### Héritage

Pour créer une sous-classe à partir d'une classe parente

```
class NomSousClasse extends NomClasseParente {}
```

La classe enfant hérite des propriétés et méthodes de la classe parent.

Si on a besoin de modifier le constructeur pour la classe enfant, on utile d'abord le mot clé `super()` pour appeler le constructeur du parent dans celui de l'enfant.

Si on a besoin de modifier une méthode, il suffit de la réécrire.

Exemple

```jsx
class Admin extends User {
  constructor(username, name, mail){
    super(username, name, mail); // appel constructeur parent
    this.status = "ADMIN";
  }
  
  info(){
    return `${this.status} - Nom : ${this.name} - Mail : ${this.mail}`;
	};
}

const walt = new Admin("walt", "Walt Disney", "walt-disney@mail.tld")
```
