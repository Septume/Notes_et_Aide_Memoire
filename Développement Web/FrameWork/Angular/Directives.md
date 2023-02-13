# Directives

Classe qui permet d'interagir avec le DOM et les éléments HTML

3 types de directives

- directive d'attribut : pour modifier le comportement ou le style des éléments. (ex : `[ngClass]`  ,  `[ngStyle]`)
- directive structurelle : modification du DOM. Le nom commence par une `*` (Ex : `*ngFor` et `*ngIf` )
- Les components sont aussi des directives (la class Component hérite de la class Directive )

## Directives prédéfinies

### Structurelles

#### ngIf

`*ngIf` : Ajoute ou retire un élément du DOM en fonction d'une condition  
Remarque : si on souhaite juste cacher un élément du DOM plutôt que le supprimer il faut utiliser à la place `[hidden]`

```html
<!-- 
le paragraphe s'affiche que si la conditon est true 
-->
<p *ngIf="isUserLoggedIn && age >= 18"> Lorem Ipsum </p>
```

Pour des questions de performance il est recommandé de créer une propriété et lui affecter la condition que l'on souhaite tester

```ts
export class ExampleComponent {
  //**
  isAuthorized : boolean = this.isUserLoggedIn && this.age >= 18
}
```

```html
<p *ngIf="isAuthorized"> Lorem Ipsum </p>
```

On peut également afficher des élément dans le cas où la condition est fausse

Exemple 1

```html

<!-- si la condition est fausse on n'affiche pas cet élement mais l'élement qui contient la variable de template "loggedOut" -->
<p *ngIf=" isUserLoggedIn; else loggedOut">Vous ête connecté</p>

<!-- ng-template : élement spécifique à Angular pour créer des bouts de template. Si activé par la condition c'est son contenu qui sera inséré dans le DOM -->
<ng-template #loggedOut>
  <p>Vous n'êtes pas connecté</p>
</ng-template>
```

 Exemple 2

 

```html
<!-- ng-container : cet élement ne s'affichera pas et est utilisé que pour faire le traitement (permet d'éviter d'utiliser une balise vide  -->
<ng-container *ngIf=" isUserLoggedIn; then loggedIn else loggedOut"></ng-container>

<!-- élement qui s'affiche si la condition est true -->
<ng-template #loggedIn>
  <p>Vous ête super connecté</p>
</ng-template>

<!-- élement qui s'affiche si la condition est false -->
<ng-template #loggedOut>
  <p>Vous n'êtes pas connecté</p>
</ng-template>

```

On peut utiliser `*ngIf` avec un observable et le pipe `async`

Exemple 1

```html
<!-- le mot clé "as" permet de recupérer la valeur en transit dans une variable pour l'utiliser directement dans le template 
(le template reste synchronisé avec le flux de donnée) 
-->
<div *ngIf="(user$ | async) as user">
  {{user}}
</div>
```

Exemple 2

```html
<div *ngIf="(user$ | async) as user; else loading">{{user}}</div>

<ng-template #loading>
  <p>Loading use data... </p>
</ng-template>
```

#### ngFor

`*ngFor` : créer plusieurs éléments à partir d'un tableau

```html
<ul>
<li *ngFor="let user of users">{{user}}</li>
</ul>
```

Il est possible de l'utiliser avec un observable et le pipe `async`

```html
<ul>
  <li *ngFor="let user of users | async">{{user}}</li>
</ul>
```

La directive peut être utilisé avec des variables prédéfinis qui permet de récupérer des informations sur le tableau de données

- `index` : index de l'élément (retourne un nombre)
- `count` : nombre d'élément dans le tableau (retourne un nombre)
- `first` : premier élément du tableau (retourne un booléen)
- `last` : dernier élément du tableau (retourne un booléen)
- `odd`: les éléments pairs (retourne un booléen)
- `even` : les éléments impairs (retourne un booléen)

```html
<ul>
  <!-- affiche une numérotation 1/n, 2/n etc -->
  <li *ngFor="let user of userList; index as indexUser; count as countUser"> {{indexUser + 1}}/{{countUser}}.
    {{user.firstname }} {{user.lastname}}</li>
</ul>
```

Pour le débogage on dispose du pipe `keyvalue` qui retourne l'index et la valeur de chaque élément du tableau

```html
<ul>
  <li *ngFor="let item of users | keyvalue">
    {{item.key}} : {{item.value}}
  </li>
</ul>
```

##### Optimisation

Par défaut chaque modification dans le tableau de données utilisé dans une directive `*ngFor` entraine une reconstruction complète de la liste des éléments dans le DOM.  
Pour améliorer les performances il est possible de faire en sorte que seul les éléments concernés soient modifiés dans le DOM.  
Pour cela il faut que chaque élément du tableau ai un identifiant unique et utiliser l'option `trackBy` avec une méthode qui permet de récupérer cet identifiant.

```ts
export class ExampleComponent implements OnInit {
 //**
 
/* par défaut on utilise deux paramètres
  - un id qui doit être unique
  - les élements sur lequel itérer
*/
  trackById(id: number, user: User): number {
    return user.id;
  }
```

```html
<ul>
  <li *ngFor="let user of userList; trackBy:trackById">{{user.firstname }} {{user.lastname}}</li>
</ul>
```

##### Bonne pratique

Il est recommandé d'utiliser :
- Un component parent : qui se chargera d'afficher la liste
- Un component enfant : qui se chargera d'afficher chaque élément de la liste

```ts
//** 
export class ParentComponent implements OnInit {
  userList: User[] = [
    // élements du tableau
  ];
  
  //**
}
```

```ts
//** 
export class ChildComponent implements OnInit {
  @Input() user!: User;

  //**
}
```

```html
<div>
  <app-child *ngFor="let user of userList" [user]="user"></app-child>
</div>
```

```html
<p>{{user.firstname}} {{user.lastname}}</p>
```

### Directives d'attribut

#### ngStyle

`ngStyle` : Pour ajouter dynamiquement du code CSS à un élément. Prend comme valeur un objet dont les clés correspondent aux propriétés CSS

```html
<p [ngStyle]="{color: 'colorProperty'}"> </p>
```

#### ngClass

`ngClass` : pour ajouter ou supprimer dynamiquement des classes CSS à un élément.  
peut prendre comme valeur :

- un chaine de caractère
- un tableau
- Un objet dont les clés correspondent aux noms de classes à appliquer et les valeurs aux conditions pour que la classe soit appliquée.  
Remarque : La directive peut être combiner avec l'attribut HTML `class`

```ts
export class ExampleComponent {
  btnClassesString: string = 'btn-success';
  btnClassesArray: string[] = ['btn-success', 'btn-lg'];
  isValid: boolean = false;
}
```

```html
<!-- utilisation d'un string -->
<button class="btn" [ngClass]="btnClassesString">Valider</button>

<!-- utilisation d'un tableau -->
<button class="btn" [ngClass]="btnClassesArray">Valider</button>

<!-- utilisation d'un objet -->
<button class="btn" [ngClass]="{'btn-success': isValid, 'btn-danger': !isValid}">Valider</button>
```

## Créer une directive

Pour créer une directive : `ng g d nom-directive`

La directive contient un sélecteur qui doit être utilisé comme attribut dans une balise HTML

```ts
@Directive({
  selector: '[appDirectiveName]',
})
```

```html
<div appDirectiveName></div>
```

Lorsque l'attribut HTML est détecté, une nouvelle instance de la directive est créé

Dans le constructor il faut injecter :
- `ElementRef` : qui est une référence vers l'élément du DOM
- `Renderer2` : (facultatif) outil qui permet d'interagir avec le DOM de manière testable (on peut écrire des tests unitaires qui peuvent être exécutés dans un contexte où le DOM n'existe pas)

Il faut également implémenter le lifecycle hook `AfterViewInit` => permet de s'assurer que le DOM est complètement construit avant de commencer à manipuler les éléments.

```ts
import { AfterViewInit, Directive, ElementRef, Renderer2 } from '@angular/core';

@Directive({
  selector: '[highlight]',
})
export class HighlightDirective implements AfterViewInit {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  ngAfterViewInit(): void {
    this.setBackgroundColor('yellow');
  }

  setBackgroundColor(color: string): void {
   // on utilise la méthode setStyle() de Renderer2 pou changer la couleur de fond 
   // on utilise la propriété nativeElement de ElementRef pour avoir accès à l'élement
    this.renderer.setStyle(this.el.nativeElement, 'background-color', color);
    // variante sans utilisé Render2
     // this.el.nativeElement.style.backgroundColor = color;
    
  }
}
```

Remarque : Les directives fonctionnant comme les components il possible de leur injecter des services ou autres.


### Propriétés personnalisées

Pour créer des propriétés personnalisés on utilise le décorateur `@Input()` 

```ts
import {
  AfterViewInit,
  Directive,
  ElementRef,
  Input,
  Renderer2,
} from '@angular/core';

@Directive({
  selector: '[highlight]',
})
export class HighlightDirective implements AfterViewInit {

  // par défaut la couleur est jaune
  @Input() color = 'yellow';

  constructor(private el: ElementRef, private renderer: Renderer2) {}

  ngAfterViewInit(): void {
    this.setBackgroundColor(this.color);
  }

  setBackgroundColor(color: string): void {
    this.renderer.setStyle(this.el.nativeElement, 'background-color', color);
  }
}
````

```html
<!-- on change la couleur par défaut -->
<p highlight color="pink">{{post.title}}</p>
```


Si on a qu'une seule propriété, celle-ci peut être du même nom que le sélecteur ce qui permet d'avoir une syntaxe raccourci dans le template 

```ts

export class HighlightDirective implements AfterViewInit {
  // ici on ne peut indiquer une valeur par défaut
  @Input() highlight!: string;
  //***
}
```

```html
<!-- on indique la couleur à utiliser -->
<p highlight="yellow">{{post.title}}</p>
```

### Réagir à des évènements 

On utilise le décorateur  `@HostListener` pour gérer les événements du DOM.
Ce dernier prend en paramètre le nom de l'évènement. 
On lui indique une méthode qui sera appelé lors de l'évènement


```ts
//**

export class HighlightDirective implements AfterViewInit {

  // lorsque la souris entre sur l'élement
  @HostListener('mouseenter') onMouseEnter() {
    //**
  }
  
   // lorsque la souris quite l'élement
  @HostListener('mouseleave') onMouseLeave() {
    //**
  }

  // lorsque d'un click sur l'élèment
  @HostListener('click') onClick() {
    //**
  }
}
```

