# CSS - Astuce des 62,5 %

Pour la taille de la police

## Problème de départ

L'utilisation l'unité rem est recommandé pour indiquer la taille de la police.  
Mais la conversion entre une valeur en pixel et une valeur en rem peut être compliquée si on part d'une valeur qui est impaire on d'un grand nombre (cela demande d'utiliser la fonction `calc()` ou un préprocesseur comme SASS)

Exemple : Si 16px = 1rem

- 8px = 0.5rem => facile à trouver
- 5px = 0.3125rem => plus difficile à trouver

## La solution

Comme il est plus facile de faire des calcul en utilisant une base 10 on pourrait  utiliser : 10px = 1rem  
Or la taille de la police de base utilisé par les navigateurs n'est pas 10px mais 16px.  
Pour pouvoir ramener cette base à 10px il faut utiliser un pourcentage, en l'occurrence :  62,5%

```css
:root {
	font-size: 62.5%; /* 62,5 % de 16px = 10px */
}
```

Il ne faut pas oublier ensuite de ramener la taille de police du corps de texte à 16px

```css
body {
	font-size: 1.6rem: /* 16px */
}
```

Remarque : L'utilisation d'un pourcentage permet de conserver les préférences de l'utilisateur concernant la taille de base de la police
