# Xml

## Introduction

= Extensible Markup Language

Dérivé du SGML (Standard Generalized Markup Language)

Langage de balisage générique utilisé pour les échanges de données. Permet de créer son propre vocabulaire grâce à un ensemble de règles et de balises personnalisables

### Syntaxe

`<balise attribut="valeur">contenu</balise>`

`<balise attribut="valeur"/>`

`<!-- Ceci est un commentaire ! -->`

### **Règles de nommage**

- Les noms sont sensibles à la casse
- Les noms peuvent contenir des lettres, des chiffres ou des caractères spéciaux.
- Les noms ne peuvent pas commencer par les lettres XML (quelle que soit la casse).
- Les noms ne peuvent pas débuter par un nombre ou un caractère de ponctuation.
- Les noms ne peuvent pas contenir d'espaces.
- Éviter les caractères - , ; . < et > ainsi que les caractères accentués
- Les règles de nommage des attributs sont les mêmes que pour les balises.
- La valeur d'un attribut doit impérativement être délimitée par des guillemets, simples ou doubles.
- Dans une balise, un attribut ne peut être présent qu'une seule fois.

### **Structure d'un document xml**

### **Prologue**

Première ligne du document XML. Donne des informations de traitement.

Obligatoire depuis la version 1.1 d'XML. (Il est conseillé de l'utiliser également pour la version 1.0)

Syntaxe

`<?xml ?>`

Exemple :

```
 <?xml version = "1.0" encoding="UTF-8" standalone="yes" ?>
```

standalone = permet d'indiquer si le document est autonome ou non

### **Le corps**

Ensemble des balises qui décrivent les données. Le corps est contenu dans une paire de balise appelée élément racine (dont le nom doit être explicite et refléter le contenu)

Exemple

```
 <?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
 <repertoire>
     <personne sexe="masculin">
         <nom>DOE</nom>
         <prenom>John</prenom>
         <adresse>
             <numero>7</numero>
             <voie type="impasse">impasse du chemin</voie>
             <codePostal>75015</codePostal>
             <ville>PARIS</ville>
             <pays>FRANCE</pays>
         </adresse>
         <telephones>
             <telephone type="fixe">01 02 03 04 05</telephone>
             <telephone type="portable">06 07 08 09 10</telephone>
         </telephones>
         <emails>
             <email type="personnel">john.doe@gmail.com</email>
             <email type="professionnel">john.doe@societe.com</email>
         </emails>
     </personne>
 </repertoire>
```

### **Document xml bien formé**

- prologue renseigné dans un document utilisant la version 1.1 du XML
- le document ne possède qu'une seule balise racine.
- le nom des balises et des attributs est conforme aux règles de nommage.
- les balises ensont correctement imbriquées et fermées.

### **Définition d'un document xml**

= ensemble de règles décrivant la façon donc le document doit être construit. => impose une écriture uniforme que tout le monde doit respecter.

Pour être valide, le document doit être conforme à la définition.

## **Document type definition (dtd)**

Document permettant d'écrire la définition d'un document XML

### **Définition d'une balise**

`<!ELEMENT nomBalise (contenu)>`

Le contenu d'une balise peut être :

- une autre balise. Dans ce cas celle-ci doit avoir été également définie
- une valeur simple (nombre, chaine de caractères…). Dans ce cas ou utilise le mot clé `#PCDATA`
- vide Dans ce cas on utilise le mot clé `EMPTY` (Remarque : ici on peut omettre les parenthèses)
- tout. Dans ce cas on utilise le mot clé `ANY` (on peut omettre ls parenthèses). Il est tout de fois déconseillé de l'utiliser afin de restreindre le plus possible la liberté de rédaction du document XML.

Exemple

```
     <!ELEMENT personne (nom)>
     <!ELEMENT nom (#PCDATA)>
```

### **Séquence**

permet de décrire l’enchaînement imposé des balises.

`<!ELEMENT balise (balise2, balise3, balise4, balise5, etc.)>`(L'ordre est important)

Exemple :

```
 <!ELEMENT personne (nom, prenom, age)>
 <!ELEMENT nom (#PCDATA)>
 <!ELEMENT prenom (#PCDATA)>
 <!ELEMENT age (#PCDATA)>
```

### **Liste de choix**

Permet d'indiquer que la balise doit contenir une des balises décrites (et pas une de plus)

`<!ELEMENT balise (balise2 | balise3 | balise4 | balise5 | etc.)>`

### **Balise optionnelle**

Le nom de la balise est suivi d'un point d'interrogation

`<!ELEMENT balise (balise2, balise3?, balise4)>`

### **Balise pouvant être répétée**

La balise est obligatoire (Présente 1 ou plusieurs fois) : Le nom de la balise est suivi d'un plus

`<!ELEMENT balise (balise2, balise3+, balise4)>`

La balise n'est pas obligatoire (présente 0, 1 ou plusieurs fois) : : Le nom de la balise est suivi d'un astérisque

`<!ELEMENT balise (balise2, balise3*, balise4)>`

### **Définition des attributs**

`<!ATTLIST balise attribut type mode>`

- type : permet de spécifier le type de valeur
- mode : information suplémentaire sur l'attribut

### **Types**

### **Liste de valeurs possibles**

`<!ATTLIST balise attribut (valeur 1 | valeur 2 | valeur 3 | etc.) mode>`

### **Texte non parsé**

Valeur de n'importe quel type. Il s'agit de données qui ne seront pas analysées par le parseur au moment de l'exploitation du document.  
On utilise le mot clé `CDATA`

`<!ATTLIST balise attribut CDATA mode>`

Exemple

```
 <!ATTLIST personne sexe CDATA mode>
```

### **Identifiant unique**

La valeur de l'attribut est unique dans le document. On utilise le mot clé `ID`

`<!ATTLIST balise attribut ID mode>`

Exemple

```
 <!ATTLIST personne position ID mode>
```

### **Référence à un identifiant unique**

On utilise le mot clé `IDREF`

`<!ATTLIST balise attribut IDREF mode>`

Exemple

```
 <!ATTLIST father id ID mode >
 <!ATTLIST child id ID mode father IDREF mode>
```

### **Mode**

### **Attribut obligatoire**

On utilise le mot clé `#REQUIRED`

`<!ATTLIST balise attribut type #REQUIRED >`

Exemple

```
 <!ATTLIST personne sexe (masculin|féminin) #REQUIRED>
```

### **Attribut optionnel**

On utilise le mot clef `#IMPLIED`

`<!ATTLIST balise attribut type #IMPLIED>`

Exemple

```
 <!ATTLIST personne sexe CDATA #IMPLIED>
```

### **Valeur par défaut**

On écrit la valeur en dur dans la règle

`<!ATTLIST balise attribut type "valeur" >`

Exemple

```
 <!ATTLIST personne sexe CDATA "non précisé">
```

### **Constante**

Permet de fixer la valeur d'un attribut non obligatoire quand celui-ci est renseigné. . On utilise le mot clé mot clef `#FIXED` suivi de la valeur

`<!ATTLIST balise attribut type #FiXED "valeur">`

Exemple

```
 <!ATTLIST objet devise CDATA #FIXED "Euro">
```

### **Les entités**

= alias permettant de réutiliser des informations au sein du document XML ou de la définition DTD.

### **Entités générales**

associe un alias à une information afin de l'utiliser dans le document XML.

`<!ENTITY nom "valeur">`

utilisation dans le document XML : `&nom;`

```
 <!ENTITY samsung "Samsung">
 <!ENTITY apple "Apple">
 
 <telephone>
         <marque>&samsung;</marque>
         <modele>Galaxy S3</modele>
 </telephone>
 <telephone>
         <marque>&apple;</marque>
         <modele>iPhone 4</modele>
 </telephone>
```

### **Entités paramètres**

à utiliser uniquement dans le DTD. Permet d'associer un alias à une partie de la déclaration de la DTD

`<!ENTITY % nom "valeur">`

utilisation : `%nom;`

```
 <!ENTITY % listeMarques "marque (Samsung|Apple) #REQUIRED">
 <!ATTLIST telephone %listeMarques; >
```

### **Entités externes analysées**

même rôle que les entités générales sauf que les informations sont stockés dans un fichier séparé

`<!ENTITY nom SYSTEM "URI">`

```
 <!ENTITY samsung SYSTEM "samsung.xml">
```

### **Lié le dtd au document xml**

### **Dtd interne**

écrit dans le même fichier que le document XML via le DOCTYPE. ce dernier est placé après le prologue et avant le contenu XML.

`<!DOCTYPE racine >`

Exemple

```
 <?xml version = "1.0" encoding="UTF-8" standalone="yes" ?>
 
 <!DOCTYPE boutique [
         <!ELEMENT boutique (telephone*)>
         <!ELEMENT telephone (marque, modele)>
         <!ELEMENT marque (#PCDATA)>
         <!ELEMENT modele (#PCDATA)>
 ]>
 <boutique>
         <telephone>
                 <marque>Samsung</marque>
                 <modele>Galaxy S3</modele>
         </telephone>
         <telephone>
                 <marque>Apple</marque>
                 <modele>iPhone 4</modele>
         </telephone>
         <telephone>
                 <marque>Nokia</marque>
                 <modele>Lumia 800</modele>
         </telephone>
 </boutique>
```

### **Dtd externe**

écrit dans un fichier à part portant l'extension `.dtd`

Dans ce cas le document XML n'est pas autonome.  
L'attribut standalone du prologue doit être à "no"

### **Dtd externes public**

Utilisées lorsque la DTD est une norme

`<!DOCTYPE racine PUBLIC "identifiant" "url">`

Exemple : Document XHTML 1.0

```
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

### **Dtd externes system**

`<!DOCTYPE racine SYSTEM "URI">`

L'URI peut être une adresse relative ou absolue

```
 <?xml version = "1.0" encoding="UTF-8" standalone="no" ?>
 <!DOCTYPE boutique SYSTEM "boutique.dtd">
```

## **Schémas xml**

## **Dom**

## **Xpath**

## **Xslt**

## **Les espaces de noms**
