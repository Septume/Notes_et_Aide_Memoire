# TypeScript

Superset de JavaScript  
Permet de typer les variables, paramètres et classes => réduction des erreurs au niveau du développement

## Installation et configuration

### Installation

Pour installer TypeScript : `npm install -g typescript`  
Vérifier l'installation : `tsc -v`

### Compilation

Pour compiler un script TS en JS : `tsc script-name.ts`

### Configuration

Pour créer un fichier de configuration JSON (*tsconfig.json*) : `tsc --init`

### Suivre les changement

`tsc -w`

## Typage

3 catégories

- `any` => tout types (donc les objets)
- Types natifs à JavaScript
- Types créer par classe ou interface

Syntaxe 
-  `variable:type`  : Déclaration
- `variable:type = valeur` : Déclaration et initialisation 
- `variable = valeur`  : Déclaration et initialisation avec inférence (le type est automatiquement déterminé en fonction de la valeur) 

On peut également utiliser la syntaxe `variable!:type` => le `!` (bang) ou opérateur d'assertion non nul permet de préciser que la valeur ne peut pas être `null` ou `undefined` 

### Types natifs

- `string`
- `number`
- `boolean`
- `null`
- `undefined`

```js
let text = "Hello World"; // inférence
let nombre: number; // déclaation 
let isDone: boolean = false; // déclaration et initialisation

nombre = 1;
// provoque une erreur
// text = 5; // Type 'number' is not assignable to type 'string'.
// nombre = "texte"; // Type 'string' is not assignable to type 'number'
```

#### Tableaux

On utilise la syntaxe `type []`

```ts
let textTab: string[]; // tableau de string
let numericTab: number[]; // tableau de nombre
let anyTab: any[]; // tableau contenant des valeurs de n'importe quel type

textTab = ["pim", "pam,", "poum"];
numericTab = [1, 2, 3];
anyTab = ["pim", 1, ["pam", 2]];

// provoque une erreur
// numericTab = ["pim", "pam,", "poum"];
```

```ts
// declaration d'un tableau
let tab: any[];

// ne fonctionne pas car le tableau n'a pas été initialisé
//tab.push('data');

//initialisation du tableau
tab = [];
tab.push("data");

// pour déclarer et initialiser 
// let tab: any[] = [];
```

Autre syntaxe : ` Array<type>`

```ts
let textTab: Array<string>; // tableau de string
let numericTab: Array<number>; // tableau de nombre
let anyTab: Array<any>; // tableau contenant des valeurs de n'importe quel type
```

#### Fonctions

Si une fonction ne retourne rien on utilise le type `void`

```js
// fonction sans retour
function message(name: string): void {
  console.log("Hello" + name);
}
message("Stephanie");

// fonction avec retour
// prend en argument un nombre et retourne un nombre
function square(data: number): number {
  return data * data;
}
```

#### Objets

```ts
let Person: { name: string, age: number }
let person: Person
```

### Créer ses propres types

Interface => Fonctionnalité purement TypeScript. Contrairement à une classe ne peut pas instancier un objet

```ts
interface User {
  id: number;
  name: string;
}


let user: User = {
  id: 1,
  name: "toto"
  // provoque une erreur car la propriété email n'a pas été définie dans l'inteface
  // email: "toto@mail.tld"
}
```

Si on créé une classe celle ci sera aussi un type. 

Remarque : lorsqu'on implémente une interface on est obligé d'utiliser ses propriétés et méthodes dans la classe qui l'implémente


## Propriétés optionnelles 

```ts
class FaceSnap {
  public title!: string;
  public description!: string;
  public imageUrl!: string;
  public createdDate!: Date;
  public snaps!: number;
  // propriété optionnelle (syntaxe avec un "?") 
  public location?: string
}
```


## Literal Types


## Décorateurs 








  