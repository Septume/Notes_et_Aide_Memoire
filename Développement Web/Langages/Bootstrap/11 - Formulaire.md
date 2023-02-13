# Formulaire

### **Contrôles**

`form-control :` les contrôles prennent toute la largeur possible + mise en forme basique (a utiliser sur `<select>`, `<input>` et `<textarea>`)

`form-group` : pour grouper des éléments. Créer un espacement avec un `margin-bottom` de 1rem

```html
 <form>
     <div class="form-group">
         <label for="login">Pseudo</label>
         <input type="text" id="login" name="login" class="form-control">
     </div>
         <div class="form-group">
         <label for="password">Mot de passe</label>
         <input type="password" id="password" name="password" class="form-control">
     </div>
     <button type="submit">Envoyer</button>
 </form>
```

Autres classes :

- `sr-only` : permet de rendre invisible les labels plutôt que de ne pas en mettre (il est conseillé d'utiliser un label pour chaque contrôle pour une meilleur accessibilité)

### **Checkbox et bouton radio**

`form-check` : met en forme les éléments

`form-check-label` : met en forme le label

`form-check-input` : met en forme le input

`form-check-inline` : aligne les éléments

```html
 <form action="">
     <p>Désirez-vous vous inscrire à notre newsleter ?</p>
     <div class="form-check form-check-inline">
         <label class="form-check-label">
             <input type="radio" name="newsletter" value="true" class="form-check-input">Oui
         </label>
     </div>
         <div class="form-check form-check-inline">
         <label class="form-check-label">
             <input type="radio" name="newsletter" value="false" class="form-check-input">Non
         </label>
 </di
```

### **Aide et validation**

`form-text` : texte d'aide. à associer avec une classe de texte comme text-muted

`is-valid`: indique avec une bordure verte que le champ est valide

`is-invalid` : indique avec une bordure rouge que le champ n'est pas valide

`valid-feedback`: message indiquant que le champ est valide

`invalid-feedback` : message indiquant que le champ est invalide

```html
 <form action="">
     <div class="form-group">
         <label for="username">Pseudo</label>
         <input type="text" id="username" class="form-control is-valid">
         <p class="valid-feedback">OK</p>
     </div>
     <div class="form-group">
         <label for="password">Mot de passe</label>
         <input type="password" id="password" class="form-control is-invalid">
         <p class="invalid-feedback">Mot de passe incorrect</p>
         <small class="form-text"><a href="#" class="text-muted">Mot de passe oublié ?</a></small>
     </div>
     <button class="btn btn-primary">Envoyer</button>
 </form>
```

### **Mise en forme du formulaire**

On peut aligner les labels et les champs en utilisant les classes `row` et `col-*`

```html
 <form>
     <div class="form-group row">
     <label for="login" class="col-4">Pseudo</label>
     <input type="text" id="login" name="login" class="col-8 form-control">
     </div>
     <div class="form-group row">
     <label for="password" class="col-4">Mot de passe</label>
     <input type="password" id="password" name="password" class="col-8 form-control">
     </div>
     <button type="submit" class="btn btn-primary">Envoyer</button>
 </form>
 
```

`btn` : met en forme un bouton. A utiliser avec les balises `<button>`, `<a>` et `<input>` de type `button` ou `submit`

Options de couleur de fond :

- `btn-primary`
- `btn-secondary`
- `btn-success`
- `btn-danger`
- `btn-warning`
- `btn-info`
- `btn-light`
- `btn-dark`
- `btn-link`

Options de couleur de outline :

- `outline-primary`
- `outline-secondary`

	etc…

Options de taille de bouton :

- `btn-lg` : gros bouton
- `btn-sm` : petit bouton

Autres options :

`btn-block` : donne un display block (le bouton s' étend sur la largeur complète du parent)
