# CSS - Typographie fluide

Consiste à définir une taille de police qui est automatiquement proportionnelle à la taille du viewport.  
L'idée n'est plus d'adapter la taille de la police en fonction de plusieurs breakpoints  via les media queries mais de faire en sorte que la taille change de manière progressive en fonction de la taille de l'écran.  
Pour définir une taille de police fluide on se base sur l'unité vw. On doit également définir une taille de police minimale et maximale quelque soit le viewport.

### Méthode 1

Utilisation d'une formule  

```
taille police min + ( taille police max - taille police min) * (100vw - taille viewport min ) / (taille viewport min - taille viewport max)
```

Par exemple : Si on veut que la taille de la police soit entre

- 16px sur un écran de 320px ou moins
- 22px sur écran de 1000px ou plus  

```css
/* taille minimale */  
html {  
	font-size: 16px;  
}  
/* formule */  
@media (min-width: 320px) {  
	html {  
		font-size: calc(16px + (22px - 16px) * (100vw - 320px) / (1000 - 320));  
	}  
}  
/* taille maximale */  
@media (min-width: 1000px) {  
	html {  
		font-size: 22px;  
	}  
}
```

### Méthode 2

Utilisation de la nouvelle fonction CSS  `clamp()` (Attention : Pas encore supporté par tout les navigateurs)  

Prend 3 valeurs

- Valeur minimale
- Valeur préférée (Valeur médiane et dynamique)
- Valeur maximale  

Par exemple si on veut une taille de police entre 16px et 22px et qu'entre les deux la taille correspond à 4vw  

```css
html {  
	font-size: clamp(16px, 4vw, 22px)  
}  
```

On peut aussi utiliser des rem

```css
html {  
	font-size: clamp(1rem, 4vw + 1rem , 1.375rem)  
}
```

Inconvénient de la méthode : Le calcul de la valeur préférée est compliquée mais on peut utiliser des outils en ligne qui le fait pour nous comme [The Clamp Calculator](https://royalfig.github.io/fluid-typography-calculator/)