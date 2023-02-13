# Routes

Permet d'avoir un système de navigation pour l'application

Les routes sont configurées  :
- au niveau racine dans le fichier `app-routing.module.ts`
- au niveau d'un module

## Configurer les routes

### Au niveau racine

Créer un fichier `app-routing.module.ts`

```ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';


// routes racines
const routes: Routes = [];

@NgModule({
  // permet d'enregister les routes racines
  imports: [RouterModule.forRoot(routes)],
  // export du routing une fois configuré
  exports: [RouterModule],

})

export class AppRoutingModule {}
```

Ajouter le module dans `app.module.ts`

```ts
//...
import { AppRoutingModule } from './app-routing.module';

@NgModule({
 //...
  imports: [BrowserModule, AppRoutingModule],
})
```

Dans `app-routing.module.ts` on utilise la constante `routes` pour définir les routes

```ts
const routes: Routes = [
  { path: 'users', component: ListUsersComponent },
  // URL avec un paramètre
  { path: 'user/:id', component: DetailUserComponent },
  // route par défaut (path avec un string vide) 
  // on redirige vers un autre path
  // le pathMatch permet d'éviter les erreurs lors de la redirection depuis un chemin vide
  { path: '', redirectTo: 'users', pathMatch: 'full' },
   // ** => signifie "toutes routes". A UTILISER EN DERNIER
   // permet d'avoir une page ereur 404 personnalisée
  {path: '**', component: PageNotFoundComponent}
];
```

Attention : les routes sont lues de haut en bas => l'ordre de déclaration des routes est importante. Il faut toujours aller du plus spécifique au plus général, en terminant par la route par défaut

### Au niveau d'un module

Voir [[Modules]]

## Configurer les templates

`<router-outlet>` : permet de relier les routes  
à chaque changement d'URL, Angular récupère le component associé et injecte le template à la place de la balise. A mettre dans le template racine

`routelink` : Cette directive permet de créer des liens. On indique comme valeur une route existante.  
On peut en plus appliquer la directive `routerLinkActive` qui permet d'appliquer une classe à la route active et ses enfants. `[routerLinkActiveOptions]` permet de configurer des options. par exemple :

- `exact:true` : la classe n'est pas appliquer aux enfants

```html
<nav>
  <a routerLink="" routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">Home</a>
  <a routerLink="/facesnaps" routerLinkActive="active">facesnaps</a>
  </nav>
```

Remarque pour `routerLink` 
- si on ne pas le `/` => on accède à une sous-route (relative)
- si on met le `/` => on accède à une route de manière absolue (à partir de la racine)


## Configuration navigation

### URL avec paramètre

```ts
const routes: Routes = [
  // URL avec un paramètre
  { path: 'user/:id', component: DetailUserComponent }
  //...
];
```

```ts
export class DetailUserComponent implements OnInit {
 
  // ActivatedRoute => service qui pemet d'avoir accès à la route courante
  constructor(private route: ActivatedRoute) {}

  ngOnInit(): void {
    // snapshot => accès à l'instant T
    // paramMap => paramètres transmis à l'URL
    // get() => récupération de l'identifiant
    const userId  = this.route.snapshot.paramMap.get('id');
    // on utilise ensuite l'id pour afficher l'élement correspondant 
    if (userId) {
      this.user = this.userService.getUserById(+UserpId);
    }
  }
}
```

### Bouton de navigation

```ts
export class ListUserComponent implements OnInit {
 //...
 
  constructor(private router: Router){} // indispensavble pour utiliser navigate()
  ngOnInit(): void { }
  goTo(user: User) {
  /*
  navigate => Methode de Router. Prend en paramètre un tableau qui contient
    - L'URL vers laquelle naviguer
    - éventuellement des paramètres
   */
    this.router.navigate(['user', user.id])
   /* sans paramètres on peut aussi utiliser : 
   this.router.navigateByUrl('user');
   */
   
  }
}
```
