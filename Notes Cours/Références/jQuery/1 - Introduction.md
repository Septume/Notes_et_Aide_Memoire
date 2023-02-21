# Introduction

Framework JavaScript libre créé en 2006

Fonctionnalités :

- Gestion de la compatibilité sur tout les navigateurs
- Parcours et modifications du DOM
- Gestion des événements
- Effets visuels et animations
- Manipulation du CSS
- Gestion des formulaires
- Ajax
- Plugins (avec possibilité de créer ses propres plugins)
- Utilitaires

## **Fonctionnement**

jQuery repose sur une seule et unique fonction : `jQuery()` ou son alias `$()` qui retourne un objet jQuery contenant des éléments du DOM et sur lequel on peut appliquer des méthodes

`$(param).methode(param)`

Les méthodes peuvent être chainées. Pour une meilleur lisibilité on peut les placer les unes sous les autres avec une indentation

```
  $(param)
     .methode1(param)
     .methode2(param)
     .methode3(param)
     .methode4(param);
```

Pour des meilleures performances Il est fortement recommandé de chainer les méthodes plutôt que de créer à chaque fois un nouvel objet jQuery

Il est possible d'affecter l'objet retourné à une variable (par convention son nom commencera par un `$` afin de spécifier qu'il s'agit d'un objet jQuery)

`var $variable = $(param);`

## **Code de base**

pour que jQuery puisse fonctionner correctement il faut s'assurer que le document HTML est prêt, c'est à dire que l'arbre DOM ai été entièrement construit

On utilise pour cela la méthode `ready()` sur l'objet document. Cette méthode prend comme paramètre une fonction anonyme qui contiendra l'ensemble du code jQuery

```
 $(document).ready(function() {
     // code JQuery
 });
```

On peut utiliser une version raccourci

```jsx
 $(function() {
     // code jQuery 
 });
```

## **Gestion des conflits**

D'autre bibliothèques JavaScript peuvent également utilisé la fonction `$()` ce qui créé un conflit avec jQuery

Pour résoudre le problème, deux solutions :

- utiliser `jQuery()` plutôt que l'alias `$()`
- Passer l'alias en paramètre de `ready()` pour le rendre local à la fonction

```jsx
 jQuery(document).ready(function($){
     // code jQuery 
 });
 
 // Version raccourci 
 jQuery(function($){
     // code jQuery 
 });
 
```
