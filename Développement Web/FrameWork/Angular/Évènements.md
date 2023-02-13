# Évènements

On créé une méthode qui sera appelée au moment de l'évènement  
(Par convention les méthodes qui répondent à un évènement ont un nom qui commence par `on`)

```ts
export class FaceSnapComponent implements OnInit {
  title!: string;
  description!: string;
  createdDate!: string;
  snaps!: number;
  imageUrl!: string;

  ngOnInit() {
    this.title = 'Archibald';
    this.description = 'Mon meilleur ami depuis tout petit !';
    this.createdDate = new Date().toLocaleDateString();
    this.snaps = 6;
    this.imageUrl =
      'https://cdn.pixabay.com/photo/2015/05/31/16/03/teddy-bear-792273_1280.jpg';
  }
  onAddSnap() {
    this.snaps++;
  }
```

 **Event binding** : Liaison par évènement. On utilise la syntaxe `(event)="methode()`

```html
<button (click)="onAddSnap()">Oh Snap!</button>
```

## Paramètre $event

Permet de récupérer des informations sur l'évènement

```html
<input type="number" (click)="selectOption($event)">
```

```ts

export class AppComponent implements OnInit {
//...

 //  pour un évènement "click" le type est MouseEvent
  selectOption(event: MouseEvent): void {
   /*  
   - target : cette propriété permet de récupérer l'élément qui a déclenché l'évènement
   - as HTMLInputElement : consiste à caster la propriété en un objet HTMLInputElement (obligatoire pour être compris côté composant)
   - "value" => valeur du champ
   - le "+" permet de transformer le string en nombre
    */
    const index: number = +(event.target as HTMLInputElement).value;
  }
}
```

## Variable de template

Déclarer des variables dans le template => permet d'avoir un accès direct à un élément du DOM
On utilise la syntaxe `#variable` 

Exemple 1
```html
<!-- 
- On utilise une variable #input pour faire référence au champ 
- (keyup)="null" => permet de mettre automatiquement à jour la valeur sans avoir besoin de lancer une méthode
-->
<input type="text" #input (keyup)="null">

<!--On affiche directement la valeur du champ-->
<p>{{input.value}}</p>
```

Exemple 2
```html
<input type="number" #input (change)="selectOption(input.value)">
```

```ts
export class AppComponent implements OnInit {
 //...
  selectOption(inputValue: string): void {
    // le + permet de convertir le string en nombre
    let optionId = +inputValue;
    console.log(optionId);
  }
}
```

## Pseudo évènements 

Évènements spécifiques à Angular 

Par exemple : 
`keyup.enter` => quand on appuie sur la touche entrée 
`blur` => perte du focus d'un élément du DOM

```html
<input type="number" #input (keyup.enter)="selectOption(input.value)">
```

----

```
# Angular Events Cheat-sheet
(drag)="myFunction()"
(drop)="myFunction()"
(dragover)="myFunction()"
(blur)="someFunction()"
(focus)="someFunction()" 
(scroll)="someFunction()"
(submit)="someFunction()"
(click)="someFunction()"
(dblclick)="someFunction()"
(cut)="someFunction()"
(copy)="someFunction()"
(paste)="someFunction()"
(keyup)="someFunction()"
(keypress)="someFunction()"
(keydown)="someFunction()"
(mouseup)="someFunction()"
(mousedown)="someFunction()"
(mouseenter)="someFunction()"
```