# Guards

Permet de contrôler la navigation et les accès

Les types de guards
- `CanActivate` : contrôle la navigation sur une route (utiliser pour créer un système d'authentification)
- `canActivateChild` : contrôle la navigation d'une route enfant
- `canDesactivate` : contrôle la navigation en dehors de la route courante
- `canLoad` : contrôle la navigation vers un sous module chargé de manière asynchrone

le guard retourne un booléen pour donner ou non l'autorisation de continuer la navigation.  
Le plus souvent un guard fonctionne de manière asynchrone et retourne un `Observable<boolean>` ou un `Promise<boolean>`

Pour créer un guard : `ng generate guard nom-guard`  
Puis sélectionner le type de guard à créer

## Créer une authentification

Créer un guard de type `CanActivate`

Pour appliquer le guard à une route il faut l'indiquer en 3ème option avec `canActivate`  (prend un tableau, même s'il n'y a qu'un seul guard)

```ts
const routes: Routes = [
  { path: 'path', component: ListUsersComponent, canActivate: [ExampleGuard]  }
];
```

Il faut ensuite créer un service qui va gérer le système d'authentification

```ts
export class AuthService {
  isLoggedIn: boolean = false;

  login(name: string, password: string): Observable<boolean> {
    const isLoggedIn = name == "demo" && password == "demo";
    return of(isLoggedIn).pipe(
      delay(1000), // simulation d'un délais
      tap((isLoggedIn) => (this.isLoggedIn = isLoggedIn))
    );
  }

  logout() {
    this.isLoggedIn = false;
  }
}

```

Le service est injecté dans le guard qui a été créé

```ts
import { AuthService } from "./../services/auth.service";
import { Injectable } from "@angular/core";
import {
  ActivatedRouteSnapshot,
  CanActivate,
  Router,
  RouterStateSnapshot,
  UrlTree,
} from "@angular/router";
import { Observable } from "rxjs";

@Injectable({
  providedIn: "root",
})
export class AuthGuard implements CanActivate {
  constructor(private _authService: AuthService, private _router: Router) {}

  // retour un boolean
  canActivate() {
    // si l'authentification est ok
    if (this._authService.isLoggedIn) {
      return true;
    } else {
      // sinon on redirige vers la page de login
      this._router.navigate(["/login"]);
      return false;
    }
  }
}
```

Il faut également créer un component pour le formulaire de login 

```ts
import { Router } from "@angular/router";
import { AuthService } from "./../../services/auth.service";
import { Component, OnInit } from "@angular/core";

//...

export class LoginComponent implements OnInit {
  message: string = "VOus êtes déconnecté. (demo/demo)";
  name!: string;
  password!: string;
  auth!: AuthService;

  constructor(private _auth: AuthService, private _router: Router) {}
  ngOnInit(): void {
    this.auth = this._auth;
  }

  // mis à jour du message
  setMessage() {
    if (this._auth.isLoggedIn) {
      this.message = "Vous êtes connecté";
    } else {
      this.message = "identifiant ou mot de passe incorrect";
    }
  }

  login() {
    this.message = "Connexion en cours...";
    // on envoie les codes saisies par l'utilisateur à AuthService
    this._auth
      .login(this.name, this.password)
      .subscribe((isLoggedIn: Boolean) => {
        this.setMessage();
        if (isLoggedIn) {
          this._router.navigate(["/pokemons"]);
        } else {
          this._router.navigate(["/login"]);
        }
      });
  }

  logout() {
    this._auth.logout();
    this.message = "vous ̂êtes déconnecté";
  }
}

```

