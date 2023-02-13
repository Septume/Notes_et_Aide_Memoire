# Pipes

Permet de faire des transformations sur les données à afficher dans le template

Pour utiliser un pipe  
`{{ value | pipe}}`

Il est possible de combiner des pipes avec la syntaxe  
`{{ value | pipe1 | pipe2 | …}}`

Certains pipes peuvent prendre des paramètres  
`{{ value | pipe:'param1':'param2'}}`

## Pipes prédéfinis

[Guide Angular sur les Pipes](https://angular.io/guide/pipes)

### Casse

Convertir en minuscule : `{{ value | uppercase }}`  
Convertir en majuscule : `{{ value | lowercase }}`  
Première lettre de chaque mot en majuscule : `{{ value | titlecase }}`

### Date

Formater de la date : `{{value | date:"dd/MM/yy"} ` [En savoir plus pour les paramètres](https://www.angularjswiki.com/angular/angular-date-pipe-formatting-date-times-in-angular-with-examples/)
Le formatage se fait en fonction de la locale de l'application

### Nombres

Formater des nombres décimaux :  `{{42.42 |number}}`
Le formatage se fait selon la locale. Il est possible d'ajouter des paramètres pour préciser le nombre de chiffre après la virgule

Formater un nombre en % : `{{0.4 | percent }}` 

Formater des valeurs monétaires : `{{29.99 | currency: 'EUR' }}`

### Autres pipes

Afficher la valeur dans un format JSON (utile pour le debogage) : `{{value | json }}`

Souscrire à un observable directement dans le template HTML :  `{{obserbable$ | async}}`

```ts
import { Observable, interval } from 'rxjs';
//**

export class AppComponent implements OnInit {
  // émet un nombre toute les secondes
  interval$!: Observable<number>;
  ngOnInit() {
    this.interval$ = interval(1000);
  }
}
```

```html
<p>{{interval$ | async}}</p>
```


### Changer la locale

Pour changer la locale par défaut de l'application il faut ajouter ces lignes dans le fichier `app.module.ts`

```ts
import { NgModule, LOCALE_ID } from '@angular/core';
import { registerLocaleData } from '@angular/common';
import * as fr from '@angular/common/locales/fr';

 //...

@NgModule({
  //...
  providers: [
    { provide: LOCALE_ID, useValue: 'fr-FR'}
  ]
})

export class AppModule {
  constructor() {
    registerLocaleData(fr.default);
  }
}
```


## Créer un pipe

`ng g p nom-pipe`

On définie le pipe avec la méthode `transform()`  
Prend en paramètre :

- la valeur à transformer
- les paramètres du pipe

Retourne la valeur transformée

```ts
export class NamePipe implements PipeTransform {
transform(value: unknown, ...args: unknown[]): unknown {
    return null;
  }
}
```

Exemple  1

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'age',
})
export class AgePipe implements PipeTransform {
  transform(date: string): number {
    let today = new Date();
    let dateOfBirth = new Date(date);
    let age = today.getFullYear() - dateOfBirth.getFullYear();
    let month = today.getMonth() - dateOfBirth.getMonth();
    if (month < 0 || (month === 0 && today.getDate() < dateOfBirth.getDate())) {
      age--;
    }
    return age;
  }
}
```

Exemple 2 (utilisation de paramètres) 

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'shorten',
})
// permet de raccourcir un texte
export class ShortenPipe implements PipeTransform {
  // on fixe une valeur par défaut de 50 caractères 
  // (paramètre facultatif)
  transform(value: string, maxLegnth = 50): string {
    if (value.length <= 50) {
      return value;
    }
    return value.substring(0, maxLegnth) + '…';
  }
}
```

```html
<span class="post-content">{{ post.content | shorten: 100 }}</span>
```

