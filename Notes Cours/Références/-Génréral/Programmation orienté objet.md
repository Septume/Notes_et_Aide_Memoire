# Programmation orienté objet

Définition et interaction de briques logicielles appelés objets. Permet de regrouper des données et des traitements en une seule entité

### **Avantages de la POO**

- Robustesse
- Modularité
- Lisibilité

=> Maintenabilité

### **Concepts de base**

- Abstraction
- Encapsulation
- Héritage
- Polymorphisme
=> permet de mieux organiser les programmes complexes

### **Vocabulaire**

- **Objet** : représente un concept, une idée ou toute entité du monde physique. Possède une structure interne et un comportement et interagi avec ses pairs.
	
- **Classe** : résultat des processus d'encapsulation et d'abstraction. Désigne une catégorie d'objets . Définit un nouveau type de variable
	
- **Instance** : réalisation concrète d'une classe, c'est à dire déclaration d'une variable du type défini par la classe qui permet de manipuler un objet. (la variable contient une référence vers l'objet)
	
### **Encapsulation et abstraction**

Regrouper en une seule entité (objet) les données et traitements qui lui sont spécifiques. Les objet sont définis par leur attributs et leurs méthodes :
- attributs : données incluses dans un objet
- méthodes : les fonctions (= traitements ) définies dans un objet

Les méthodes et attributs sont accessibles uniquement depuis l’intérieur de l'objet. Pour le programmeur utilisateur c'est comme une boite noire. Ce dernier n'a accès qu'à l'interface qui permet d'utiliser l'objet.

### **Héritage**

- Superclasse : classe générale dans laquelle sont regroupés des attributs et méthodes communs aux autres classes.
	
- Sous-classes : classe plus spécialisés qui hérite des caractéristiques de la superclasse. Les sous-classes sont des extensions des superclasses par enrichissement (ajout) ou spécialisation (modification ) des méthodes
	
Transitivité de l'héritage : les instances d'une sous-classe possèdent les attributs et méthodes de l'ensemble des classes parentes. Un objet de sous-classe hérite le type de sa super-classe et par transivité les types de toutes les classes ascendant => un objet peut donc avoir plusieurs types.

### **Polymorphisme**

Le fait que les instances d'une sous-classes, lesquelles sont substituables aux instances des classes de leur ascendance (en argument d'une méthode, lors d'affectation) garde leur propriétés propres.

=> le choix des méthodes à évoquer lors de l' exécution du programme se fait en fonction de la nature réelle des instances concernés => résolution dynamique des liens.
