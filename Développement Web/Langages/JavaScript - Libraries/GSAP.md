# Gsap

GreenSock Animation Platform  
Librairie JavaScript pour créer des animations

**Avantages** :

- Peut animer n'importe quoi qui peut être manipuler en JS (propriétés CSS, SVG, objet Canevas, WebGL etc…)
- Animations optimisés
- Permet de facilement gérer les enchainements entre les animations et la chronologie

**Deux principes** :

- Les tweens : permet de créer une séquence (animation de base)
- Les timelines : permet d'enchainer les animations et gérer la chronologie

## Tweens

Méthodes de l'objet gsap

**Attention** : les tweens ne sont pas directement exécutées. Ils sont à la place enregistrés dans une timeline qui sera exécutée à la fin de l'exécution du script JS

Les méthodes :

- `gsap.to(targets, vars)` : On débute l'animation avec les valeurs de base (définies dans le CSS ou valeurs par défaut) pour aller vers les valeurs définies dans la méthode
- `gsap.to(targets, vars)` : Inverse. On débute l'animation avec les valeurs définies dans la méthode pour aller vers les valeurs de bases
- `gsap.fromTo(targets, vars, vars)` : On débute et on termine l'animation avec les valeurs définies dans la méthode. Utile pour les animations susceptibles d'être relancées plusieurs fois de suite (Suite à une action de l'utilisateur)

Paramètres :

- *targets* : le ou les éléments à animer. On peut utiliser des sélecteurs (indiqués entre guillemets) ou des variables/tableaux/objets qui référencent les éléments
- *vars* : objet contenant toutes les propriétés à animer ainsi que des propriétés spéciales (fromTo utilise deux objets)

Propriétés spéciales (utilitaires) :

- `duration` : durée de l'animation en secondes (par défaut dure .5 ). Indiquer un nombre.
- `delay` : Ajoute un délais en secondes avant de commencer une animation
- `repeat` : répéter l'animation. (exemple : `repeat : 2` => l'animation sera jouée 3 fois). La valeur `-1` permet de faire une répétition à l'infinie
- `repeatDelay` : Durée en seconde entre chaque répétitions
- `yoyo` : si true l'animation est jouée en sens inverse lors d'un repeat
- `ease` : Timing de l'animation. [Voir les valeurs possibles](https://greensock.com/docs/v3/Eases)
- `stagger` : Peut être utiliser lorsque plusieurs éléments sont animés dans un tween. Permet de créer un décalage entre le début de chaque animation. On peut indiquer comme valeur :
  - un nombre pour indiquer le décalage en seconde
  - Un objet pour spécifier des options supplémentaires. Exemple de propriétés :
	- `each` : décalage en seconde
	- `from` : indiquer "end" pour débuter par le denier élément ou "center"
  - Une fonction
- `autoAlpha` : Identique à opacity sauf que lorsque la valeur atteint 0 la propriété visibility sera définie sur hidden pour empêcher toutes interactivités sur l'élément. Pour les valeurs autre que 0, la valeur sera inherit

<u>Exemples</u>

```js
gsap.to( '.img', { 
  x: 100, // translateX()  
  y: 100, 
  scale: 2, 
  duration: 2, 
  ease: "power4" 
})
```

```js
gsap.to( 'h1', { 
  color: 'red',
  backgroundColor: 'white', // Utilisation du camelCase
  duration : 2
})
```

```js
var imgs = document.querySelectorAll('img'); // on utilie plusieurs images 
  gsap.to( imgs, {  
  y: 200, 
  duration: 2, 
  ease: 'power1', 
  stagger: .2 // décalage de 0.2 secondes 
})
```

```js
gsap.to( imgs, {  
  y: 200, 
  duration: 2, 
  ease: 'power1', 
  stagger: { 
    each: .2, 
    from: 'end' // On commence par la dernière image 
  } 
})
```

```js
gsap.fromTo( img, 
  {opacity: 0}, 
  {opacity:1, duration: 3}
);
```

### Utiliser des valeurs aléatoires

`random(valMin, valMax, [arrondi])` : La valeur aléatoire doit se trouver entre une valeur min et une valeur max. EN facultatif on peut indiquer un arrondi

`random(array)` : La valeur aléatoire est choisi dans un tableau de valeur

**Attention : la fonction doit être indiquer sou forme de chaine de caractères**

<u>Exemples</u>

```js
gsap.to( imgs, {  
  y: "random(-100, 100, 10)", 
  duration: 2, 
  ease: 'power1', 
})
```

```js
gsap.to( imgs, {  
  y: "random([100,150,200])", 
  duration: 2, 
  ease: 'power1'
})
```

### Exécuter des fonctions à des étapes de l'animation

Propriétés

- `onStart` : au commencement de l'animation
- `onComplete` : quand l'animation est terminée
- `onRepeat` : à chaque répétition
- `onUpdate` : à chaque mise à jour de frames

```js
gsap.to(img, { 
  y: 100, 
  duration: 5, 
  onStart: () => console.log("Démarrage"), 
  onComplete: () => console.log("Terminé") 
});
```

### Keyframes

Permet de créer des étapes

On utile la propriété keyframes qui prend comme valeur un tableaux d'objets spécifiant les différentes étapes

```js
gsap.to(img, {keyframes: [ 
  {y: 100, duration: 1}, 
  {x: 100, duration: 1}, 
  {scale: 2, duration: 0.5} 
]});
```

### Enregistrer un tween

permet de réutiliser un tween sur un autre élément

`gsap.registerEffect()`

- `name` : nom de l'effet (chaine de caractère)
- `effect` : une fonction pour définir les effets
- `defaults` : un objet avec les valeurs par défaut

pour utiliser le tween enregistré

`gsap.effects.tweenName()`

```js
// enregister un tween

gsap.registerEffect({ 
  name: "myAnim", 
  effect: (targets, config) => { 
    return gsap.to(targets, {duration: config.duration, y: 200, scale: 1.4, rotation: 360}); 
  }, 
  defaults: {duration: 1} 
})

// utiliser le tween enregistré
gsap.effects.myAnim(elt1); // avec la durée par défaut 
gsap.effects.myAnim(elt2, {duration: 3}); // en changeant la durée pour 3 secondes
```

### Méthodes pour les tweens

Un tween retourne un objet sur lequel on peut appliquer des méthodes

Exemple

```js
const anim = gsap.to(elt,{y: 200}); 
anim.duration(5);
```

Quelques méthodes :

- `delay(number)`
- `pause()` : mettre en pause l'animation
- `remuse()` : reprendre une animation mise en pause
- `restart()` : relancer une animation
- `kill()` : tuer une animation

## Timelines

Permet de créer des séquences de tween  
Il faut dans un premier créer un objet timeline

`let TL = gsap.timeline()`

On applique ensuite des tweens à cet objet

```
TL 
.to(elt1, {y: 50}) 
.to(ielt2, {y: 50}) 
.to(ielt3, {y: 50})
```

Les animations seront jouées les unes après les autres

### Paramètres de positions

Utilisation d'un 3ème arguments dans la méthode pour régler le moment T où doit démarrer l'animation

#### Position absolu

```js
// l'img3 démarrage au moment T0 (et donc en meême moment que l'img1) 
TL
  .to(img1, { opacity: 1, y: 0, duration: 1 })
  .to(img2, { opacity: 1, y: 0, duration: 1 })
  .to(img3, { opacity: 1, y: 0, duration: 1 }, 0)
```

```js
// l'img3 démarrage au moment T1 (et donc en meême moment que l'img2)  
TL 
  .to(img1, { opacity: 1, y: 0, duration: 1 }) 
  .to(img2, { opacity: 1, y: 0, duration: 1 }) 
  .to(img3, { opacity: 1, y: 0, duration: 1 }, 1)
```

Attention : si on indique un positionnement temporel qui est supérieur par rapport à la position dans la timeline, cela vas ajoutera un temps d'attente avant l'animation suivante.

#### Position relatif

Le positionnement se fait par rapport au tween précédent

```js
let TL = gsap.timeline();
TL.to(img1, { opacity: 1, y: 0, duration: 1 })
  .to(img2, { opacity: 1, y: 0, duration: 1 }, "-=0.75") // démarre à 1s (durée tween précédent) - 0.75 [remarque : on peut également utiliser le +]
  .to(img3, { opacity: 1, y: 0, duration: 1 }, "-=0.75")
```

Autres méthode pour le positionnement relatif

```
let TL = gsap.timeline();

TL.to(img1, { opacity: 1, y: 0, duration: 1 })
  .to(img2, { opacity: 1, y: 0, duration: 1 }, '<') // demarrage au même moment que tween précédent
  .to(img3, { opacity: 1, y: 0, duration: 1 })
```

Les valeurs possibles

- `<` : Démarrage en même temps que le tween précédent
- `>` : Démarrage à la fin du tween précédent

On peut préciser le nombre de secondes. Ex : `<0.5` => Démarrage à 0,5 s après le début du tween précédent.

On peut mixer les positionnements

```js
TL.to(img1, { opacity: 1, y: 0, duration: 1 }, 1)
  .to(img2, { opacity: 1, y: 0, duration: 1 }, 0) 
  .to(img3, { opacity: 1, y: 0, duration: 1 }, ">"); 
```

### Utilisation d'un label

Permet der référencer un point de la timeline pour l'utiliser dans des méthodes

```js
TL.to(img1, { opacity: 1, y: 0, duration: 1 }, 1)
  .to(img2, { opacity: 1, y: 0, duration: 1 }, 0) 
  .addLabel('nomLabel')
  .to(img3, { opacity: 1, y: 0, duration: 1 }, ">"); 

setTimeout(() => {
	TL.play()
}, 1000)
```

### Créer une timeline avec des paramètres par défaut

```js
let TL = gsap.timeline({
  defaults: {
    duration: 1,
    ease: "power",
  },
});

TL.to(img1, { opacity: 1, y: 0 })
  .to(img2, { opacity: 1, y: 0, duration: 2 }, "-=0.75") // on peut surcharger les paramètres par défaut. 
  .to(img3, { opacity: 1, y: 0 }, "-=0.75");
```

### Autres paramètres de l'objet timeline

En plus de `defaults` on peut utiliser d'autres paramètres

```js
let TL = gsap.timeline({
  defaults: {
    duration: 1,
    ease: "power",
  },
  repeat: 1,
  repeatDeplay: 1,
  onComplete : () => console.log('ok');
});
```

## Méthodes utilitaires de GSAP

`gsap.set(target, vars)` : permet de fixer des propriétés pour des éléments

```js
gsap.set(elt, { 
	opacity: 0 
})
```
