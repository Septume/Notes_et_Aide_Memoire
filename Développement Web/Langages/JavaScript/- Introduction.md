# Introduction

Langage de programmation de script orienté objet par prototype créé par Netscape en 1995

Standardisé en 1997 sous le nom ECMAScript par ECMA International (spécification : ECMA-262)

Dernières versions d' ECMAScript :

- **ES5 (2009) :** Compatible avec les navigateurs à partir d' IE9
- **ES6 (2015) :** Comptatible avec les navigateurs modernes
	- Mots clé `let` et `const`
	- type `symbol`
	- Template literals
	- Boucle `for…of` (Permet d'itérer sur un tableau)
	- Fonctions fléchées (*arrows functions*)
	- Paramètres par défaut pour les fonctions
	- Paramètre de reste (*Rest parameter*) pour les fonctions (Permet d'utiliser un nombre d'arguments indéfinis)
	- Affectation par décomposition (*Destructuring*)
	- Classes
	- Modules
- ECMAScript 2016, 2017, 2018

[JavaScript Versions](https://www.w3schools.com/js/js_versions.asp)

Pour assurer la comptabilité avec les dernières versions on peut utiliser :

- Un **polyfill** : Script JS permettant de simuler les fonctionnalités des nouvelles versions qui ne sont pas encore pris en charge par tout les navigateurs
- un **transpiler** : Outil permettant de traduire le code vers une ancienne syntaxe. Ex : Babel

## **Syntaxe**

Les instructions se terminent par un point-virgule

Les blocs d'instructions sont délimités par des accolades

Permissivité :

- Le point-virgule peut être omis, si l'instruction est suivi d'un retour à la ligne
- les accolades peuvent être omis si le bloc contient qu'une seule instruction

## **Commentaires**

```jsx
 //ceci est un commentaire de fin de ligne 
 
 /* ceci est 
 un commentaire 
 sur plusieurs lignes */
```

## **Hello world**

```jsx
 alert("Hello World"); 
 
 //ou dans une console (outil de développement des navigateurs) 
 console.log("Hello World"); 
```

## **Placement du code**

De préférence à la fin de l'élément `body` (le JavaScript sera chargé après le corps de la page)

On peut également le placer dans l'élément `head` (le JavaScript sera chargé avant le corps de la page)

Dans le code HTML :

```html
 <script> /* CODE JAVASCRIPT */</script>
```

Dans un fichier externe :

```html
 <script src="fichier.js"></script>
```

Remarque : le fichier externe est mis en cache par le navigateur, et n'est donc pas rechargé à chaque chargement de page, ce qui accélère l’affichage

On peut en plus utiliser deux attributs (de type booléen) :

- `defer` Le script JS est chargé après le corps de la page, quelque soit son emplacement. Cet attribut n’a pas d’effet pour les scripts inline ou si l’attribut `async` est utilisé
- `async` : Le script est exécuté de manière asynchrone dès qu'il sera prêt et sans bloquer le chargement de la page. A utiliser si le fonctionnement de la page n’est pas dépendante du script. Cet attribut n’a pas d’effet pour les scripts inline

