# GSAP - ScrollTrigger

Plugin pour gérer les animations au scroll

## utilisation

```js
gsap.to("elt", {
  duration: 1,
  y: 0,
  scale: 2,
  autoAlpha: 1,
   // l'animation est lancé lorsqu'on arrive au niveau de l'élément indiqué
  scrollTrigger: "elt",
});

```

On peut utiliser un objet pour préciser des paramètres

```js
gsap.to(".b2 h2", {
  duration: 1,
  y: 0,
  scale: 2,
  autoAlpha: 1,
  scrollTrigger: {
    trigger: ".b2 h2",
    markers: true // permet d'afficher des marqueurs pour faciliter les réglages
  },
});
```

## Triggers et scrollers

`start` / `end` : Triggers (Déclencheurs). Par défaut situé en haut et en bas de l'élément

`scroller-end` / `scroller-start` : Scroll. Par défaut situé en haut et en bas de la fenêtre

L'animation est déclenché quand `scroller-start` se situe au niveau de `start`

on peut régler le positionnement des `triggers` et `scrollers`

```js
gsap.to(".b2 h2", {
  duration: 1,
  y: 0,
  scale: 2,
  autoAlpha: 1,
  scrollTrigger: {
    trigger: ".b2 h2",
    markers: true
    // Trigger Scroller 
    start: "top center" // le trigger est positionné en haut de l'élement et le scroller au millieu du viewport
  },
});
```

En plus des mots clés on peut utiliser des valeurs en % ou en pixels

```
"50% bottom" 
"10 bottom" // +10px
"-10 bottom" // -10px
"center+=10 bottom" // au centre + 10px
"center-=10 bottom" // au centre - 10px
"center+=10% bottom"
 ```

Le `scroller-end` permet de jouer une animation tout le long du scroll jusqu'à qu'on arrive à `end`

## Évènements

`onEnter` : lorsque qu'on entre dans la zone de vue de l'animation (on scroll vers le bas après le `start`) start - start  
`onLeave` : Lorsqu'on sort de la zone de vue (on scroll vers le bas après le `end`) end -enf  
`onEnterBack` : lorsqu'on revient en arrière dans la zone de vue (on scroll vers le haut avant le `end`)  
`onLeaveBack`: lorsqu'on sort de la zone de vue après être revenu en arrière. (on scroll vers le haut avant le `start`)

Un fonction callback peut être exécutée lorsqu'un évènement se produit

```js
scrollTrigger: {
    markers: true,
    trigger: ".elt",
    onEnter: () => console.log("ENTER"),
    onLeave: () => console.log("LEAVE"),
    onEnterBack: () => console.log("ENTERBACK"),
    onLeaveBack: () => console.log("LEAVEBACK"),
  },
```

## Actions

- `play`
- `pause`
- `resume` (rejouer l'animation après une pause)
- `restart` (rejouer l'animation)
- `reverse` (rejouer en inversé)
- `complete`(aller à la fin de l'animation)
- `reset` (remettre à zéro)
- `none` (aucune action)

La propriété `toggleActions` permet d'exécuter des actions  
lors des évènements `onEnter` , `onLeave` , `onEnterBack` et  
`onLeaveBack` (dans cet ordre)

```js
 // onEnter onLeave onEnterback onLeaveBack
toggleActions: "play reverse play reverse"
```

### Scrub et pin

 `scrub` : Pour que l'animation soit jouée en même temps que le scroll

 

```js
scrollTrigger: {
	trigger: ".elt",
	scrub: true
}
```

```js
scrollTrigger: {
	trigger: ".elt",
	scrub: 1 // avec un décalage de 1s
}
```

`pin` : l'élément reste fixe 

```js
scrollTrigger: {
	trigger: ".elt",
	pin: true
}
```
