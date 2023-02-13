# Formulaires 


`<mat-form-field>` : permet d'envelopper des composants de formulaire pour appliquer des styles de champ de texte

```html
<mat-form-field appearance="fill">
  <mat-label>Input</mat-label>
  <input matInput>
</mat-form-field>

<mat-form-field appearance="fill">
  <mat-label>Select</mat-label>
  <mat-select>
    <mat-option value="one">First option</mat-option>
    <mat-option value="two">Second option</mat-option>
  </mat-select>
</mat-form-field>

<mat-form-field appearance="fill">
  <mat-label>Textarea</mat-label>
  <textarea matInput></textarea>
</mat-form-field>
```

Variante d'apparence : 
- `fill` (zone d'arrière-plan remplie + soulignement)
- `outline` (bordure) 
- `legacy` (défaut. déconseillé car ne correspond plus à la spécification actuelle de Material Design) 

On peut configurer l'apparence par défaut pour l'ensemble de l'application avec un provider global

```ts
@NgModule({
  providers: [
    {provide: MAT_FORM_FIELD_DEFAULT_OPTIONS, useValue: {appearance: 'fill'}}
  ]
})
```

`<mat-label>` : permet d'indiquer un label flottant. Le texte du label est affiché dans le champ. Lorsque ce dernier prend le focus le texte du label flotte au dessus du champ (si le champ a un placeholder, ce dernier est affiché à la plae du label lors du focus) 
Si le champ est `required` le label affiche également une astérisque rouge 

Hint labels : permet d'indiquer un texte indicatif sous le champ

```html
 <mat-form-field hintLabel="10 caractères max" appearance="fill">
    <mat-label>Entrer quelque chose</mat-label>
    <input matInput #input maxlength="10">
  </mat-form-field>
```

`<mat-error>` : permet d'afficher un message en cas d'erreur

```html

<mat-form-field appearance="fill">
  <mat-label>Email</mat-label>
  <input matInput [formControl]="email" required>
  <mat-error *ngIf="email.invalid">{{getErrorMessage()}}</mat-error>
</mat-form-field>

```
