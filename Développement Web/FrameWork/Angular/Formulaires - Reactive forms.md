# Reactive forms

Caractéristiques

- permet de générer des formulaires dynamiques (dont la structure n'est pas connu d'avance)
- mise à disposition des Observables qui permet de traiter en temps réel les saisies
- validations plus poussées

Importation du module : `import { ReactiveFormsModule } from '@angular/forms'`

## Créer le formulaire

### FormControl

Instanciation d'un objet `FormControl` avec `new FormControl()` qui peut prendre en paramètre une chaine de caractères correspondant à la valeur par défaut du contrôle.

Propriétés de l'objet `FormControl`

- `value` : valeur du contrôle.

```ts
import { FormControl } from '@angular/forms';

//...

export class ReactiveFormsComponent {
  username = new FormControl();
  message = new FormControl('Hello World'); 
}
```

Dans le template on utilise l'attribut `[FormControl]` qui prend comme valeur le nom de l'objet créé  
Pour afficher les valeurs saisies on utilise `{{controlName.value}}`

```html
<input type="text" placeholder="pseudo" [formControl]="username">
<!-- affiche la chaine de caractères passée en paramètre du constructeur-->
<input type="text" placeholder="message" [formControl]="message">

<ul>
<!-- On précise "value" car sinon ça affiche l'objet et non pas la valeur -->
  <li>Votre pseudo : {{ username.value }} </li>
  <li>Votre message: {{ message.value }} </li>
</ul>
```

### FormGroup

Instanciation d'un objet `FormGroup` avec `new FormGroup()` qui peut prendre en paramètre un objet qui contient l'instanciation de plusieurs `FormControl`

```ts
import { FormControl, FormGroup} from '@angular/forms';

//...

export class ReactiveFormsComponent {
  form = new FormGroup({
    username: new FormControl(),
    message: new FormControl('Hello World')
  });
}
```

Dans le template on utilise l'attribut `[FormGoup]` qui prend comme valeur le nom de l'objet créé  
Pour afficher les valeurs saisies on utilise `{{groupName.value.controlName}}`

```html
<form [formGroup]="form">
  <input type="text" placeholder="pseudo" formControlName="username">
  <input type="text" placeholder="message" formControlName="message">
</form>

<ul>
  <li>Votre pseudo : {{ form.value.username }} </li>
  <li>Votre message: {{ form.value.message }} </li>
</ul>

```

### FormBuilder

Permet de générer un formulaire réactif

On utilise la méthode  `group`  du FormBuilder qui prend en paramètre un objet

- Les clés de l'objet correspondent aux noms des champs
- les valeurs permet de préciser la chaine à afficher dans les champs.

```ts

import { FormBuilder, FormGroup } from '@angular/forms';
//***

export class exampleComponent implements OnInit {
  // contient le formulaire
  form!: FormGroup;

  // FormBuilder : outil pour générer des forms réactifs
  constructor(private _formBuilder: FormBuilder) {}

  ngOnInit(): void {
    // la méthode group() permet de générer un formGroup
    // prend comme argument un objet
    // dans lequel on associe le nom des champ avec leur valeur par défaut
    this.form = this._formBuilder.group({
      username: [null],
      email: [null],
      message: 'Hello World !'
    });

  onSubmit(): void {
    //affiche un objet avec le noms des champs et la valeur
    console.log(this.snapForm.value);
  }
}

```

```html
 <!--pour lier le formulaire à l'objet-->
  <form [formGroup]="form">
    <div>
      <label for="username">Username</label>
      <!--formControlName correspond à une propriété de l'objet-->
      <input type="text" id="username" formControlName="username">
    </div>
     <div>
      <label for="email">Email</label>
      <input type="email" id="email" formControlName="email">
    </div>
    <div>
      <label for="message">Message</label>
      <textarea row="4" id="message" formControlName="message"></textarea>
  </div>
</form>
```

La propriété `valueChanges` retourne un observable qui émet à chaque changement de valeur d'un champ

```ts
export class exampleComponent implements OnInit {
  form!: FormGroup;
  // preview du formulaire
  formPreview$!: Obervable<any>;
  
  constructor(private _formBuilder: FormBuilder) {}
  
  ngOnInit(): void {
    this.form = this._formBuilder.group({
      username: [null],
      email: [null],
      message: 'Hello World !'
    },
    // objet pour une configuration supplémentaire
    {
      //mettre à jour que lorsque le champ perd le focus
      updateOn: 'blur',
    }
  );
  
  this.formPreview$ = this.snapForm.valueChanges;
}
```

```html
<!--
  Previex du formulaire
  le mot clé "as" permet de créer un alias 
-->
<div *ngIf="formPreview$ | async as form">
  <p>{{ form.username}}</p>
  <p>{{ form.mail}}</p>
  <p>{{ form.message}}</p>
</div>
```

Remarque : on peut également utiliser la méthode `control()` pour générer des `formControl()`

```ts

export class ExampleComponent implements OnInit {
  input!: FormControl;
  constructor(private formBuilder: FormBuilder) {}
  ngOnInit(): void {
    this.input = this.formBuilder.control('', [
      Validators.required,
      Validators.minLength(10),
    ]);
  }
}
```

```html
<input type="text" [formControl]="input">
```

Autres méthodes :

- `reset()` : permet de réinitialiser un contrôle (vide les données saisies)

## Valider le formulaire

### Validators

Disponible avec les Reactive Forms  
Permet d'ajouter une validation avancée aux champs du formulaire

```ts
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

//....

ngOnInit(): void {
  this.form = this.fb.group({
    username: [null, Validators.required], // le champ est requis
    email: [null, Validators.required],
  })
    // affiche true si le formulaire est invalide
    console.log(this.form.invalid);
  }

```

```html
  <form [formGroup]="form">
    <div>
      <label for="username">Username</label>
      <input type="text" id="username" formControlName="username">
    </div>
     <div>
      <label for="email">Email</label>
      <input type="email" id="email" formControlName="email">
    </div>
    <!-- le boutton de soummission reste désactivé tant que le formulaire n'est pas valide-->
  <button type="submit" [disabled]="form.invalid">Valider</button>
</form>
```

On peut indiquer plusieurs validators en utilisant un tableau

```ts
export class exampleComponent implements OnInit {
form!: FomGroup;
emailRegex: RegExp;

 ngOnInit(): void {
   this.emailRegex = /^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-z]+)$/
    this.form = this.fb.group({
      username: ['', [Validators.required, 
                      Validators.minLength(3),
                      Validators.maxLength(20)]],
      email: ['', [Validators.required, Validators.pattern(this.emailRegex)]],
    })
  }
}
```

### Validators prédéfinis


### Afficher un message d'erreur personnalisé 

On créé une méthode qui prend en paramètre un `AbstractControl` =>  correspond à un `FormControl` , `FormGroup` , ou un `FormArray` 

On utilise la méthode `AbstractControl.hasError()` qui prend en paramètre une clé de validation et qui retourne `true` si il y a une erreur de ce type

```ts
  getFormCtrlErrorText(ctrl: AbstractControl): string {
    if (ctrl.hasError('required')) {
      return 'ce champ est requis';
    } else if (ctrl.hasError('email')) {
      return 'mail invalide';
    } else {
      return '';
    }
  }
```

Avec Angular Material on peut afficher le message d'erreur avec un élément `mat-error` 

```html
<mat-form-field appearance="fill">
  <mat-label>Email</mat-label>
  <input type="email" matInput [formControl]="emailCtrl">
  <mat-error>{{getFormCtrlErrorText(emailCtrl)}}</mat-error>
</mat-form-field>
```

### Créer un validator personnalisé 

Créer un fichier `nom-validator.validator.ts` dans un dossier `validators` 

Pour créer un validator il faut créer une fonction (qui reprend le nom du fichier)  qui retourne une fonction de type `ValidatorFn` 

 `ValidatorFn`  prend comme argument un `AbstractControl`  et retourne :
 - soit `null` 
 - soit un objet `ValidationErrors` 

`AbstractControl.value` : permet d'obtenir la valeur du contrôle. 
Le code du validator doit faire des tests dessus : 
- si les tests sont ok => on retourne `null` 
- sinon on retourne un objet 
  - On indique un nom de propriété qui correspondra à la clé du validator
  - On indique comme valeur la valeur du contrôle 

Exemple 

```ts
import { AbstractControl, ValidationErrors, ValidatorFn } from '@angular/forms';

export function exampleValidator(): ValidatorFn {
  return (ctrl: AbstractControl): null | ValidationErrors => {
  // on test si le controle contient la chaine 'VALID'
    if (ctrl.value.includes('VALID')) {
      return null;
    } else {
      return {
      // clé du validator
         validValidator: ctrl.value,
      };
    }
  };
}
```

Pour utiliser le validator on appelle la fonction créée

```ts
import { exampleValidator } from '../validators/example.validator';
//**

this.input = this.formBuilder.control('', [exampleValidator()]);


//***

getFormCtrlErrorText(ctrl: AbstractControl): string {
    // on utilise la clé du validator
    if (ctrl.hasError('validValidator')) {
      return 'le champ doit contenir la chaine "VALID"';
    } else {
      return '';
    }
  }
```




