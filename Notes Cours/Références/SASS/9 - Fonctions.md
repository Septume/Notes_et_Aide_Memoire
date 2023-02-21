# Fonctions

Pour définir une fonction on utilise la syntaxe :

```
@function nom-fonction(parm1, parm2,...) { 
	@return valeur;
}
```

```scss
@function lightness-shift($colour){
  @if ( lightness($colour) < 25% ) {
      @return lighten($colour, 10%);
  }@else{
      @return darken($colour, 10%);
  }
}
```
