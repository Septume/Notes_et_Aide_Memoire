# Modules

Chaque application Angular possède au minimum un module => `AppModule` (Module racine)  
Pour une meilleure organisation ont peut créer un module pour chaque fonctionnalité de l'application.

## Créer un module

Pour créer un module : `ng g m nom-module`  
Options : 
`--routing` : Ajouter un fichier de routing spécifique au module

Cela créé un dossier du nom du module avec un fichier `nom-module.module.ts`

Un module utilise le décorateur `@NgModule` qui prend en paramètre un objet qui décrit les propriétés du module.

- `declarations` :  Components, Directives et Pipes appartenant au module
- `imports` : Permet d'importer les modules nécessaires pour le fonctionnement du module courant
	- `CommonMdule` : Module qui permet d'avoir accès aux fonctionnalités de base d'Angular
- `Exports` : Éléments du module à exporter pour une accessibilité dans toute l'application
- `Providers` : Pour définir des classes ou autre qui sont des dépendances 
- `bootstrap` : Ne concerne que le module racine et permet de définir le composant racine.

## Lazy Loading

Par défaut l'application génère un seul fichier JavaScript. Cela signifie que l'application doit être chargée dans sa totalité pour être utilisée.  
Le lazy loding consiste à ce que les modules gèrent leurs propres routing ce qui permet de générer des fichiers JS séparés pour chaque fonctionnalités de l'application
Tout le code lié à un module sera chargé que si sa route est chargée

Pour créer un routing propre au module il faut créer un fichier `<nom-module>-routing.module.ts` (à côté du fichier `<nom-module>.module.ts

```ts
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from '@angular/router';

/* on créé une constante de type Routes pour définir les routes spécifiques au module */
const routes: Routes = [
  // routes dont le préfixe sera "users"
  { path: 'create', component: ListUserComponent }
  { path: ':id', component: DetailUsersComponent },
  { path: '', component: ListUserComponent },
];

@NgModule({
  imports: [
    // On enregistre les routes dans le Router
    // forChild() => routes enfants
    RouterModule.forChild(routes)
  ],
  // on export le Router configuré
  exports: [RouterModule]
})
export class ExampleRoutingModule { }
```

Puis on importe le RouterModule configuré dans `<nom-module>.module.ts

```ts
//**

@NgModule({
  //** 
  imports: [ExampleRoutingModule],
})
export class ExampleModule {}

```

Enfin on met en place le lazy loading au niveau du routing racine

```ts
const routes: Routes = [
// Le module sera chargé que pour les routes qui commence par 'users'
    { path: 'users', loadChildren: () => import('./path/example.module').then(m => m.ExampleModule) },

];
```

Attention : il faut aussi enlever l'importation du module dans le module racine AppModule car ce dernier ne doit pas l'inclure lors de la compilation (c'est le routing qui s'en charge)

```ts
@NgModule({
  //**
  imports: [
    CommonModule,
    // enlever l'importation du module pour lequel le lazy loading a été configuré
    // ExampleModule
   ]
})
export class AppModule {
}
```

Remarque : si on souhaite qu'un module gère son propre routing mais sans implémenter le lazy loading il faut juste enregistrer les routes avec  `RouterModule.forChild()` et importer le module dans le module racine AppModule





