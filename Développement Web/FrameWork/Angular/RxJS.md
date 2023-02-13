# RxJS

**Reactive eXtension for JavaScript** = Librairie la plus populaire pour la programmation réactive en JS et utilisée par défaut par Angular

**Programmation réactive** = programmation avec des flux de données asynchrones

**Observable** = Objet qui émet des valeurs au cours du temps (flux de données). Les valeurs sont toujours du même type.  
En plus des valeurs un observable peut émettre :

- une erreur
- un signal de fin qui termine le flux  
Dans ces deux cas l'émission des valeurs se termine et l'observable est détruit  
Les observables peuvent être synchrones ou asynchrones. (Mais sont surtout utiles pour les traitements asynchrones)

**Subscriber** = s'abonne à un observable pour écouter en permanence le flux de données  
A noter que dans la majorité des cas un observable n'émet rien tant qu'on a pas souscrit à ce dernier.

Avantages de la programmation réactive

- Gestion des erreurs plus facile
- Séquence d'évènements annulable
- Possibilité de faire des opérations (fonctions) sur les flux (regroupement, filtrage, combinaison, etc…)

## Créer et souscrire à un observable

Par convention le nom d'un observable doit se terminer par un `$`

```ts
 // création d'un observable
    const observable$ = new Observable(subscriber => {
      // la méthode next() permet d'émettre une nouvelle valeur
      subscriber.next(1);
      subscriber.next(2);

      // cette méthode créé une erreur et termine le flux
      // subscriber.error(new Error('Error test'));

      subscriber.next(3);
      // la méthode complete() termine le flux
      subscriber.complete();
    });

    // souscription à l'observable
    const subscription = observable$.subscribe({
      // cette méthode est appelée à chaque emmission de valeur
      next(value) {
        console.log(value);
      },
      // cette méthode est appelée en cas d'erreur
      error(error) {
        console.log('une erreur est survenu');
        console.log(error);
      },
      // cette méthode est appelée que le fux est terminé.
      complete() {
        console.log('Terminé');
      },
    });

    // désabonnement
    subscription.unsubscribe();
  }
```

Il est possible de souscrire à un observable directement dans le template avec le pipe `async`

```html
<p>{{observable$ | async}}</p
```

## Opérateurs

Les opérateurs sont des fonctions. Il existe deux types

- opérateur de création : Permet de créer un nouveau observable.
- opérateur pipable :
  - Renvoie un nouveau observable (sans modifier le précédent).
  - Utilisé avec la syntaxe `obsevable$.pipe(operator))`

### Opérateurs de création

Pour utiliser un opérateur de création il faut d'abord l'importer depuis `rxjs`

```ts
// exemple d'inmportation
import { interval, of, from} from 'rxjs';
```

#### Interval()

La méthode `interval()` permet de générer un Observable qui émet des nombres croissants en fonction d'une intervalle

```ts
import { interval } from 'rxjs';
//***

export class ExampleComponent implements OnInit {
  const interval$ = interval(1000); // émet toutes les 1s
    // souscription à l'observable
    // prend en argument un callback qui sera appelé à chaque émission de valeur
    const subscription = interval$.subscribe(value => console.log(value));
    // on se désabonne au bout de 10s
    setTimeout(() => {
      subscription.unsubscribe();
    }, 10000);
}
```

#### of()

Émet une suite de valeurs puis termine le flux de données en appelant automatiquement `complete()` Il n'est dont pas nécessaire de faire un `unsubscribe()`  
Prend en paramètres une suite de valeurs (qui peut être de n'importe quel type)

```ts
 // Exemple 1
    of('pommes', 'poires', 'bananes').subscribe((fruit: string) =>
      console.log(fruit)
    );

    // Exemple 2
    const listValue: number[] = [1, 2, 3, 4, 5];
    // on utilise le spread operator pour décomposer les élements du tableau
    // console.log permet d'afficher directement la valeur
    of(...listValue).subscribe(console.log);
```

#### from()

Permet de transformer un tableau, un itérable ou une promesse en un observable  
Tout comme `of()` appel automatiquement `complete()`

```ts
   // Exemple 1
    const listValue: number[] = [1, 2, 3, 4, 5];
    from(listValue).subscribe(console.log);

    // Exemple 2
    // émet chaque caractères de la chaine
    from('Hello World').subscribe(console.log);

    // Exemple 3
    from(new Promise((resolve) => resolve('Hello World')))
    .subscribe(console.log);
```

### Opérateurs avec pipe

Pour utiliser un opérateur de création il faut d'abord l'importer depuis `rxjs/operators`

```ts
// exemple d'inmportation
import { tap, take, map, filter } from 'rxjs/operators';
```

#### map()

Permet de transformer les valeurs d'un observable

```ts
const interval$ = interval(1000).pipe(
  map(value => value % 2 === 0 ? `${value} est pair` : `${value} est impair`)
  );
  
const subscription = interval$.subscribe(console.log);

setTimeout(() => {
  subscription.unsubscribe();
}, 10000);
```

#### filter()

Permet de filtrer les valeurs d'un observable

```ts
const interval$ = interval(1000).pipe(
  // affiche que les nombres pairs
  filter(value => value % 2 === 0)
);
```

#### tap()

Permet de récupérer les valeurs pour effectuer un traitement mais sans modifier celles ci

```ts
let tab: number[] = [];
const interval$ = interval(1000).pipe(
  // on ajoute les valeurs au tableau
  tap((value) => tab.push(value))
);

const subscription = interval$.subscribe(console.log);
setTimeout(() => {
  subscription.unsubscribe();
  console.log(tab);
}, 10000);
```

#### take()

Récupère les N premières valeurs et termine le flux

```ts
// on garde les 10 premières valeurs
const interval$ = interval(1000).pipe(take(10));
interval$.subscribe(console.log);
  ```

## Observables haut niveau

Observables (dit extérieur) qui souscrivent à d'autres Observables (dit intérieurs)

`mergeMap`  assure la mise en parallèle : l'Observable extérieur peut souscrire aux Observables intérieurs suivants sans attendre que les précédents soient complétés

`concatMap`  assure la mise en série : il attend que les Observables intérieurs complètent avant de souscrire aux suivants– même si l'Observable extérieur émet plusieurs fois. Les Observables intérieurs seront traités en séquence à la suite.

`exhaustMap`  assure le traitement complet d'une souscription avant d'observer une nouvelle émission de l'Observable extérieur. Si d’autres demandes sont faites entre temps, elles ne seront pas prises en compte.

`switchMap`  traite la dernière demande de souscription de l’Observable extérieur et annule toute souscription précédente non complétée

## Subject

Observable qui émet une valeur à la demande (Le plus souvent un booléen)

```ts
import { Subject } from 'rxjs';

//**

export class ExampleComponent implements OnInit {
subject!: Subject<boolean>;


  ngOnInit(): void {
    this.subject$ = new Subject<boolean>();
    this.subject$.next(true);
}
```

## Détruire un observable

Important pour éviter les fuites de mémoires

Un observable peut être détruit dans les situations suivantes :

- une erreur est survenue
- Appel de la méthode `complete()`
- Certains opérateurs comme `take()` termine le flux
- Désabonnement du flux avec `unsubscribe()`

Le plus souvent on se désabonne d'un observable lors de la destruction d'un component.  

```ts
import { Component, OnInit, OnDestroy } from '@angular/core';
import { interval, Subscription } from 'rxjs';


export class FaceSnapListComponent implements OnInit, OnDestroy {
  subscription!: Subscription
  
  ngOnInit(): void {
    this.subscription = interval(1000).subscribe((value) => console.log(value));

  }

  ngOnDestroy(): void {
    this.subscription.unsubscribe();
  }
}

```

Remarque : Si on a souscris à un observable dans le template avec le pipe `async` ce dernier sera automatiquement `unsubscribe` lors de la destruction du component qui l'utilise
