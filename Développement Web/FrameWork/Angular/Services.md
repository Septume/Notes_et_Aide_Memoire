# Services

Service = échange de données entre components même si il n'y a pas de relation parent/enfant. Utilise des observables  

En général on utilise les services pour faire le lien entre le backend et le frontend

## Créer un service

pour créer un service  
`ng generate service nom-serice` ou `ng g s nom-service`

```js
// decorateur qui permet d'indiquer les dépendances du service (utilise le mecanisme d'injection de dépendance) 
@Injectable({
  providedIn: 'root' // service enregistré à la racine de l'app (le service peut être utilisé par tous les components)
})
export class NameService {
  constructor() { }

  // propriétés et méthodes du service
  exampleMethod() {}
}
```

## Utiliser un service

```ts
// on importe le service
import { exampleService } from '../services/example.service';

//...

export class exampleComponent implements OnInit {
// on injecte le service (système d'injection de dépendances)
  constructor(private exampleService: ExampleService) {}
  ngOnInit(): void {
  // on a accès aux propriétés et méthodes du service
  this.property = this.exampleService.exampleMethod()
  
  }
}
```

Remarque : l' injection de dépendance permet d'utiliser la même instance de service pour tout les composants qui en ont besoin

## Gestion de l'injection du service

3 types d'injection :

- au niveau racine (application entière)
- au niveau d'un module
- au niveau d'un component

### Injection racine

Comportement par défaut.

```ts
@Injectable({
  providedIn: 'root'
})
```

### Injection au niveau d'un module

Dans le fichier du service on supprime `providedIn: 'root'`  

Puis dans le fichier du module on ajoute à `@ngModule` l'option `providers` qui contient un tableau avec la liste des services

```ts

import { ExampleService } from './services/example.service';

//...

@NgModule({
  declarations: [
    //...
  ],
  imports: [
    //...
  ],
  providers: [ExampleService]
})
```

### Injection au niveau d'un component

Remarque : peu utilisé car dans ce cas, chaque component va disposé d'une instance du service différente.

On ajoute l'injection dans le `@Component`

```ts
@Component({
  //...
  providers: [ExampleService]
})
```
