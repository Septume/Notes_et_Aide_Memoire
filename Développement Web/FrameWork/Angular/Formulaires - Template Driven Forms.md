## Template Driven Forms

Importation du module : `import { FormsModule } from '@angular/forms';`

### Directives

 `[ngForm]` : A utiliser comme attribut sur un élément HTML `form` . Permet de créer une instance de l'objet `FormGroup` au niveau global du formulaire

`[(ngModel)]` A utiliser comme attribut sur un contrôle de formulaire (élément `input`, `select`) . Permet pour chaque contrôle de créer une instance de l'objet `FormControl`  
Utilise le **two-way binding** ( liaison dans les deux sens) pour le lien avec la propriété associée du component (Permet à la fois de gérer les interactions de l'utilisateur et de traiter les données saisies côté component)

### Création du formulaire

#### Two-way binding

```ts

export class TemplateFormsComponent implements OnInit {
  firstName!: string;
  lastName!: string;
  email!: string;
  dateOfBirth!: Date;
  message = "Hello World !"
  
  ngOnInit(): void {}
}
```

```html
<div>
  <label for="firstname">Prénom : </label>
  <!--ngModel fait le lien avec la propriété associée -->
  <input type="text" id="firstname" [(ngModel)]="firstName">
</div>

<div>
  <label for="lastname">Nom : </label>
  <input type="text" id="lastname" [(ngModel)]="lastName">
</div>

<div>
  <label for="email">Email : </label>
  <input type="email" id="email" [(ngModel)]="email">
</div>

<div>
  <label for="date-of-birth">Date de naissance : </label>
  <input type="date" id="date-of-birth" [(ngModel)]="dateOfBirth">
</div>

<!-- comme la propriété "message" a déjà une valeur celle ci est affichée dans le champ=> (2-way binding) -->
<div>
  <label for="message">Message : </label>
  <textarea id="message" [(ngModel)]="message"></textarea>
</div>

<!--les infos entrées dans le formulaire sont directement affichées -->
<h3>Affichage données formulaire</h3>
<ul>
  <li>Prénom Nom : {{firstName}} {{lastName}}</li>
  <li>Mail : {{email}} </li>
  <li>Date de naissance : {{dateOfBirth | date : 'dd/MM/yyyy'}} </li>
</ul>
```

#### Soumission de formulaire

Méthode 1

```ts
export class TemplateFormsComponent implements OnInit {
  user = {
    firstname: "",
    lastname: "",
    email: ""
  };
  ngOnInit(): void {}
  onSubmit(): void {
    console.log(this.user);
  }
}
```

```html
<!-- ngSubmit : Evènement Angular qui surcharge l'évènement natif submit.
  La méthode onSubmit() sera déclencher lors de l'évènement
  l'attribut name est obligatoire si ngModel est défini dans un form
-->
<form (ngSubmit)="onSubmit()">
  <div>
    <label for="firstname">Prénom : </label>
    <input id="firstname" type="text" name="firstname" [(ngModel)]="user.firstname">
  </div>

  <div>
    <label for="lastname">Nom : </label>
    <input id="lastname" type="text" name="lastname" [(ngModel)]="user.lastname">
  </div>

  <div>
    <label for="email">Email : </label>
    <input id="email" type="email" name="email" [(ngModel)]="user.email">
  </div>

  <button type="submit">Envoyer</button>
</form>
```

Méthode 2

```ts
import { NgForm } from '@angular/forms';
//** 


export class ExampleComponent {
  firstname!: string;
  lastname!: string;
  email!: string;


  // prend comme argument un objet de type NgForm
  onSubmit(form: NgForm) {
    // affiche objet avec les propriétés firstname, lastname et email
    console.log(form.value);
  }
}

```

```html
<!--
#myForm = variable de template
En indiquant comme valeur `ngForm` la variable ne référence plus l'élément associé mais l'objet ngForm
Lors de la soumission on appelle une méthode qui prend en argument la référence vers l'objet ngForm" 
-->

<form #myForm="ngForm" (ngSubmit)="onSubmit(myForm)">
  <div>
    <label for="firstname">Prénom : </label>
    <input id="firstname" type="text" name="firstname" [(ngModel)]="firstname">
  </div>

  <div>
    <label for="lastname">Nom : </label>
    <input id="lastname" type="text" name="lastname" [(ngModel)]="lastname">
  </div>

  <div>
    <label for="email">Email : </label>
    <input id="email" type="email" name="email" [(ngModel)]="email">
  </div>

  <button type="submit">Envoyer</button>
</form>

```

### Validation

```ts
export class TemplateFormsComponent implements OnInit {
  user = {
    firstname: "",
    lastname: "",
    email: ""
  }
  /...
  
  onSubmit() {
    console.log(`${this.user.firstname} ${this.user.lastname} - ${this.user.email}`)
    }
}
```

```html
<!--
#userForm = variable de template
En indiquant comme valeur `ngForm` la variable ne référence plus l'élément associé mais l'objet ngForm (qui permet d'avoir accès à des fonctionnalités comme la validation)
-->

<form (ngSubmit)="onSubmit()" #userForm="ngForm">
  <!--les champs utilisent des règles de validation HTML qui pourront être traité par Angular-->
  <!--Les variables de template sont également surchargées avec ngModel (permet d'avoir accès à l'état de validité du champ)-->
  <div class="input-group">
    <label for="firstname">Prénom : </label>
    <input type="text" id="firstname" required [(ngModel)]="user.firstname" name="firstname" #firstnameInput="ngModel"
      minlength="2">
    <!--Est caché si le champ est valide ou si il n'a pas encore été modifié-->
    <div [hidden]="firstnameInput.valid || firstnameInput.pristine">
      Le prénom est requis et doit faire au moins 2 caractères
    </div>
  </div>

  <div class="input-group">
    <label for="lastname">Nom : </label>
    <input type="text" id="lastname" required [(ngModel)]="user.lastname" name="lastname" #lastnameInput="ngModel"
      minlength="2">
    <div [hidden]="lastnameInput.valid || lastnameInput.pristine">
      Le nom est requis et doit faire au moins 2 caractères
    </div>
  </div>

  <div class="input-group">
    <label for="email">Email : </label>
    <input type="email" id="email" required [(ngModel)]="user.email" name="email" #emailInput="ngModel"
      pattern="[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{1,63}$">
    <div [hidden]="emailInput.valid || emailInput.pristine">
      Email invalide
    </div>
  </div>
  <!-- le boutton de soummission reste désactivé tant que le formulaire n'est pas valide-->
  <button type="submit" [disabled]="userForm.form.invalid">Valider</button>
</form>
```

Les directives `ngModel` et `ngForm` fournis aussi des classes CSS

```css
/* class fourni par ngModel */

/* éléments avec l'attribut required qui sont valides */
.ng-valid[required] {
  border-left: 5px solid #42a948;
}

/* éléments invalides (sauf form) */
.ng-invalid:not(form) {
  border-left: 5px solid #a94442;
}
```