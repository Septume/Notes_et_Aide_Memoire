# Requêtes HTTP

Importation du module 
`import {HttpClientModule} from '@angular/common/http'`

Utilise un observable : 
- si la requête a réussi => l'observable retourne la réponse et complète 
- si la requête échoue => l'observable retourne une erreur


On créé un [[Services|service]] pour gérer les requêtes

```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';


@Injectable({
 providedIn: 'root',
})

export class DataService {
  constructor(private _http: HttpClient) {}
  // traitements
}
```

## Requête GET

```ts

export class DataService {
  url: string = 'https://reqres.in/api/users?page=2';
  constructor(private _http: HttpClient) {}
  getData(): Observable<any> {
    // requête get
    return this._http.get(this.url, {
      // valeurs par défaut
      observe: 'body',
      responseType: 'json',
    }); // retourne observable
  }
}
```

Il est possible de préciser le type  qui est retourné par `get()` 

```ts
getData(): Observable<items[]> {
    // requête get
    return this._http.get<items[]>(this.url); // retourne observable
  }
```

Pour gérer les erreur

```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { catchError, Observable, of } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class DataService {
  url: string = 'https://reqres.in/api/users?page=2';
  constructor(private http: HttpClient) {}
  getData(): Observable<any> {
    return this.http.get(this.url).pipe(
      // en cas d'erreur
      catchError((error) => {
        // on affiche l'erreur
        console.log(error);
        // on retourne undefined
        return of(undefined);
      })
    );
  }
}
```

Ensuite on s'abonne à l'observable dans le component qui a besoin du service

```ts
import { DataService } from 'src/app/services/example.service';
//...

export class MainContentComponent implements OnInit {

  //...
  
  constructor(private _dataService: DataService) {}
  
  ngOnInit(): void {
    // abonnement au service
    this.dataService.getData().subscribe((res: any) => {
      console.log(res);
    });
  }
}
```


## Requête POST

```ts
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Observable} from 'rxjs';

//...

export class DataService {
  url: string = '';
  constructor(private _http: HttpClient) {}

  postData(data : any): Observable<any> {
    return this._http.post('api/pokemons', data,  
    // options de la requête
     {
      headers: new HttpHeaders({ 'Content-Type': 'application/json' }),
      observe: 'response', // obtenir une réponse complète et pas uniquement les données
    })
  }
}
```

Remarque : les requêtes PUT fonctionne de la même manière (méthode `put()` avec 3 paramètres) 


## Requête Delete 

```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable} from 'rxjs';

//...

export class DataService {
  url: string = '';
  constructor(private _http: HttpClient) {}

  DeleteData(data): Observable<ay> {
    return this._http.delete(this.url);
  }
}
```


## Intercepteurs HTTP

permet d'intercepter les requêtes envoyées, ainsi que les réponses reçues, dans le but d'effectuer certaines tâches comme l'authentification, la gestion des erreurs 

Créer un ficher interceptor : ` ng g interceptor nom-interceptor 
La méthode `intercept()` est appelé à chaque requête de l'application.

```ts

export class ExampleInterceptor implements HttpInterceptor {
  constructor(private auth: AuthService) {}

  // méthode appelée à chaque requête de l'app
  // request : représente la requête
  // next: permet d'envoyer la requête
  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    //renvoie la requête
    return next.handle(request);
  }
```

On peut via cette méthode modifier le header de chaque requête  pour ajouter un token d'autorisation

```ts
@Injectable()

export class ExampleInterceptor implements HttpInterceptor {
  constructor(private auth: AuthService) {}

  intercept(
    request: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    // ajout d'un header
    const headers = new HttpHeaders().append(
      'Authorization',
      `Bearer ${this.auth.getToken()}` // token d'autorisation
    );

    // L'objet représentant la requête ne peut pas être modifié
    // on fait donc un clone de celui 
    // en argument on indique un objet de configuration pour passer la const "headers"
    const modifiedReq = request.clone({ headers });

    // on envoie la requête clonée
    return next.handle(modifiedReq);
  }
}
```

Ensuite il faut créer dans le dossier des interceptors un fichier *index.ts* qui va permettre de centraliser tout les intercepteurs créés

```ts
import { HTTP_INTERCEPTORS } from '@angular/common/http';
import { ExampleInterceptor } from './example.interceptor';

export const httpInterceptorProviders = [
  {
    provide: HTTP_INTERCEPTORS,
    useClass: ExampleInterceptor, // on indique le nom de classe de l'interceptor créé
    multi: true, // option qui autorise l'enregistrement de plusieurs interceptors
  },
];
```

On ajoute ensuite la constante créé à la liste des providers de AppModule 

```ts
//***
import { httpInterceptorProviders } from './interceptors';
// ...
    providers: [ httpInterceptorProviders],
//***
```

Les interceptors permettent également de gérer les erreurs de toutes les requêtes via `catchError()` 


## Bonnes pratiques 

- Utiliser un component parent qui interagit avec le service pour récupérer les données. 
- Utiliser des components enfants pour afficher les données
=> Permet de séparer la logique dynamique (interactions service, etc...) de la logique d'affichage 
