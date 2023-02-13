# Mode strict JS

En mode normal, le langage est plus permissif et laisse passer des erreurs de syntaxe sans lever des exceptions (on parle d’erreurs silencieuses). Le mode strict permet de désactiver cette permissivité et de signaler les erreurs de manière explicite. Par exemple le mode strict ne tolère pas l'ommission du mot clé `const`, `let` ou `var` dans une déclaration de variable. De plus le mode strict interdit l'utilisation de noms qui sont réservés pour les futures versions de JavaScript.

Deux interêts :

- Oblige à utiliser une syntaxe plus rigoureuse
- L'exécution du script en mode strict est plus rapide

Pour activer le mode strict on indique en début de fichier la ligne :

```jsx
use strict;
```

On peut également activer le mode strict uniquement pour une fonction

```jsx
function demo(){
	use strict;
	// code
};

```

Attention : Pour que cela fonctionne l'instruction `user strict` doit être la première dans le script ou la fonction



