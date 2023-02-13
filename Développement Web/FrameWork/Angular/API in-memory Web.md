# API in-memory Web

Outils qui permet de simuler l'appel à une API sur un serveur distant et les opérations CRUD

Installation :  
`npm install angular-in-memory-web-api

Créer un service qui va simuler la base de données

```ts
import { Injectable } from "@angular/core";
import { InMemoryDbService } from "angular-in-memory-web-api";
import { data } from "./path/data"; // objet qui contient les données

@Injectable({
  providedIn: "root",
})

export class ExampleService implements InMemoryDbService {
  // méthode qui va permettre de simuler une base de données
  createDb(): any {
    return { data };
  }
}
```

On peut indiquer directement l'objet qui contient les données

```ts


import { Injectable } from '@angular/core';
import { InMemoryDbService } from 'angular-in-memory-web-api';
@Injectable({
  providedIn: 'root'
})
export class ExampleService implements InMemoryDbService {
  createDb() any {
      const data = [
        {
          id: 1,
          name: ' Voluptatem excepturi magnam nostrum dolore recusandae'
        },
        {
          id: 2,
          name: 'amet consectetur adipisicing elit.Lorem ipsum dolor sit',
        }
      ];
      return { data };
    
  }
}
```

Attention : l'objet doit obligatoirement avoir un une clé **id**

Puis dans le module importer `HttpClientInMemoryWebApiModule` et utiliser sa méthode `forRoot()` pour passer le service créé (permet d'avoir qu'une seule instance du service) 

```ts
import { HttpClientInMemoryWebApiModule } from "angular-in-memory-web-api";
import { ExampleService } from "./services/example.service";
//...

@NgModule({
  //...
  imports: [
  //...
  HttpClientInMemoryWebApiModule.forRoot(ExampleService, { dataEncapsulation: false,}),
],
//...
})
```

Attention :  `HttpClientInMemoryWebApiModule` doit être importé après le `HttpClientModule`

Pour effectuer les requêtes HTTP utiliser une URL sous la forme `api/<objectName>` où on indique le nom de l'objet créé dans le `InMemoryDbService`
Dans notre exemple : `api/data` 
