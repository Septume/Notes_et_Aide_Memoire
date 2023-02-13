# Components

## Créer un component

`ng generate component nom-component`  
Options : 
`--module=ModuleName` : Ajouter le component pour un module spécifique
`--export` : Ajouter le component aux exports du module


Ou en raccourci : `ng g nom-component`  
Cela créé dans `scr/app` un dossier du nom du component avec tous les fichiers 

Remarque : il est conseillé de ranger les dossiers des components dans un dossier parent nommé `components` . Pour cela utiliser la commande `ng g c components/nom-component

## Configuration

Le décorateur `@Component` permet de configurer le component  

- `selector` :  sélecteur à utiliser pour ajouter  le  component comme balise HTML.
  Pour ajouter le composant dans le code HTML :  `<nom-selector></nom-selector>`
- `template` : permet d'indiquer du code HTML à afficher 
  (Ex : `template: '<h1>Hello World</h1>'`)
- `styles` : permet d'indiquer dans un tableau des styles CSS 
  ( Ex : `styles: ['h1 {font-family: Verdana}', 'p {font-size: 20px}']` 
- `templateUrl` : permet d'indiquer le fichier qui va servir de template pour le code HTML
  (Ex : `templateUrl: './app.component.html'`)
- `styleUrls` : Permet d'indiquer dans un tableau une liste de fichier de style


Remarque : on peut utiliser plusieurs fois le sélecteur. Cela créé autant d'instance du component. Chaque instance est totalement indépendante ce qui permet à chaque component d'avoir des données et comportements différents


## Propriétés et méthodes

La class du component implémente l'interface `ngOnInit` qui oblige à utiliser la méthode `ngOninit()` même si celle ci est vide. cette méthode est appelée automatiquement par Angular au moment de la création de l'instance du component

### Déclarer des propriétés

- `nomPropriete!:type` : Déclaration. (le `!` (bang) ou opérateur d'assertion non nul permet de préciser que la valeur ne peut pas être `null` ou `undefined` )
- `nomPropriete:type = valeur` : Déclaration et initialisation
- `nomPropriete = valeur` : Déclaration et initialisation avec inférence (le type est automatiquement déterminé en fonction de la valeur)

Exemple

```ts
export class nameComponent {
  createdDate!: Date; // déclaration 
  title: string = "Hello world";  // déclaration et initialisationn
  description = 'Lorem ipsum'; // déclaration et initialisation avec inférence
}
```

 La méthode `ngOnInit()` permet d'initialiser les propriétés

```js
ngOnInit() {
  this.createdDate = new Date();
  this.title = 'Hello Word';
  this.description = 'Lorem ipsum';
}
```

### Définir des méthodes

Syntaxe TypeScript

```
nomMethode(param: type) : type {]
```

Une méthode sans valeur de retour est de type `void`

Exemple

```ts
message(name: string): void {
  console.log("Hello" + name);
}
```


## Cycle de vie d'un component 

1. `ngOnChanges()` : Méthode appelée en premier (avant même  `ngOnInit()`) lors de l'instanciation du component et à chaque fois que la valeur d'une propriété est modifiée pour permettre la mise à jour du template HTML.  Prend en paramètre un objet qui contient les anciennes et les nouvelles valeurs 
2. `ngOnInit()` : Méthode qui initialise le component 
3. `ngDoCheck()`  : Permet détendre le comportement par défaut de la méthode `ngOnChange()` (Peu utilisée) 
4. `ngAfterViewInit()` : Méthode appelée après que le template HTML soit généré, ainsi que les templates enfants
5. `ngOnDestroy()` :  Méthode appelée en dernier juste avant la suppression du component dans le DOM. (un component est supprimé si par exemple il n'est plus affiché lors d'un changement de route)  Permet notamment de se désabonner des services qui ne sont plus utiles pour éviter de saturer la mémoire. 

Ces méthodes sont appelées en interne par Angular et peuvent être surchargées dans la class du component. En général on utilisera `ngOnInit()` et `ngOnDestroy()` 

## Échange des données parent/enfants

### Parent vers l'enfant

1. On créé une propriété dans le composant parent : `parentPropertyName!: type`
2. On injecte la propriété dans le component enfant  :`@Input() childPropertyName!: type
3. On fait le lien entre les propriétés en utilisant le property binding dans le code HTML du parent : `<app-example [childPropertyName] = "parentPropertyName" ></app-example>` 

Attention : Le décorateur `@Input()` doit au préalable être importé.  
`import { Input } from '@angular/core'`

Exemple
```ts
export class ParentComponent implements OnInit {
  tab!: number[]; // on declare un tableau de nombre
  constructor() { }
  ngOnInit(): void {
     this.tab = [3, 6, 9, 15, 27, 2]; // on initialise le tableau de nombre
  }
}
```

```ts
import { Component, OnInit, Input } from '@angular/core'; // on oublie pas d'importer Input

//....

export class ChildComponent implements OnInit {
  @Input() tabNumber!: number; // on injecte une propriété depuis le parent
  constructor() { }
  ngOnInit(): void {
  }

}
```

```html
<!--Code HTML du component parent-->

<!-- On on fait une boucle qui va parmettre d'afficher autant d'enfant qu'il y a d'élements dans le tableau initialisé dans le parent. Chaque enfant affiche une des valeurs du tableau  -->
<div *ngFor="let item of tab">
  <app-child [tabNumber]="item"></app-child>
</div>
```

```html
<!-- Code HTMl du component enfant -->
{{tabNumber}}
```

### Enfant vers le parent

Permet à un component parent de réagir à des événements venant de son enfant
On utilise le décorateur `output()` et l'objet `EventEmitter`

```ts
import { Component, EventEmitter, Input, OnInit, Output } from '@angular/core';
//**


export class childComponent implements OnInit {

  // EventEmitter : objet qui émet des évènements
  // dans l'exemple le type est string
  @Output() newEvent = new EventEmitter<string>();

  //**


  onSubmit() {
    // la methode emit() prend comme argument la valeur à emettre
    this.newEvent.emit(this.message);
    //***
  }
}
```


`EventEmitter` créé un nouveau type d'évènement qui peut être utilisé comme Event Binding dans le template du parent 

```ts

export class ParentComponent implements OnInit {
  // on indique le type de valeur à emettre (dans l'exemple string) 
  onNewEvent($event: string) {}
}

```


```html
<!-- "$event" est obligatoire => variable globale qui est utilisé pour passer une valeur du type déclaré -->
<app-child (newEvent)="onNewEvent($event)">
</app-child>

```

On peut utiliser comme type pour `EventEmitter` un objet littéral 

```ts
export class ExampleComponent {
  @Output() postCommented = new EventEmitter<{ comment: string;  postId: number}>
  onNewComment($event: string) {  
    this.postCommented.emit({ comment: $event, postId: this.post.id})
  }
}
```



