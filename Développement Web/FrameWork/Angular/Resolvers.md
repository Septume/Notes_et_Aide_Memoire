# Resolvers

Permet d'effectuer des requêtes lors du routing. 
La navigation aboutit uniquement si les données ont bien été reçus. 
Cela permet d'éviter l'affichage d'un page où il manque des éléments 

Pour créer un fichier resolver : `ng g resolver resolver-name`

```ts
// Post[] => type de données qui sera récupéré
export class ExampleResolver implements Resolve<Post[]> {
  constructor(private _postService: PostService) {}
  resolve(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<Post[]> {
    // on retourne les données récupérés (ici on utilise un service qui retourne un observable)
    return this._postService.getPosts();
  }
}
```

On ajoute ensuite le resolver au providers des modules qui en ont besoin (facultatif) 

```ts
@NgModule({
  // ...
  providers: [ExampleResolver]
})
```

Puis  indiquer le resolver créé dans le routing 

```ts
const routes: Routes = [
  // la clé "example" sera utilisée dans le component pour avoir accès au données renvoyées par le resolver
  { path: '', component: ExampleComponent, resolve: { example: ExampleResolver } }
];
```

Pour accéder aux données dans le component

```ts
export class ExampleComponent implements OnInit {
  posts$!: Observable<Post[]>;

  // on injecte ActivateRoute 
  constructor(private _route: ActivatedRoute) {}
  ngOnInit(): void {
  // la propriété data de ActivateRoute permet d'avoir accès aux données du resolver et retourne un observable
  // On utilise la clé indiquer dans l'objet de configuration pour récupérer les données
    this.posts$ = this._route.data.pipe(map((data) => data['posts']));
  }
}
```