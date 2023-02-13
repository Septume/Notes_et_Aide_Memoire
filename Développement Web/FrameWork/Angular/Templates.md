# Templates

## Afficher des valeurs

**Text interpolation** : affichage de la valeur d'une propriété dans le template avec la syntaxe `{{ nomPropriete }}`  
**Property binding** (liaison de données) Permet d'utiliser des valeurs dynamiques pour les attributs HTML

```html
<h2>{{ title }}</h2>
<p>Mis en ligne le {{ createdDate }}</p>
<img [src]="imageUrl" [alt]="title">
<p>{{ description }}</p>

```

## Éléments ng-container et ng-template

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

## Variables de template  

On peut déclarer une variable dans le template avec la syntaxe `#variableName` pour faire référence à un élément du DOM, une directive ou un component

```html
<!-- on declare la variable #phone -->
<input #phone placeholder="Numéro de téléphone" />
<!-- phone.value permet d'avoir accès la valeur du champ -->
<button type="button" (click)="callPhone(phone.value)">Call</button>
```

Si la variable est déclarée au niveau du sélecteur d'un component, elle fait référence à ce component.  
Si elle est déclarée au niveau d'un `ng-template` elle fait référence à un instance de `TemplateRef` qui représente le modèle.

Pour faire référence à une directive on l'indique en valeur de la variable

```html
<!--
En indiquant comme valeur `ngForm` la variable ne référence plus l'élément associé mais l'objet ngForm
-->
<form (ngSubmit)="onSubmit()" #userForm="ngForm">
 
  <!---********** -->
  
  <button type="submit" [disabled]="userForm.form.invalid">Valider</button>
</form>
```
