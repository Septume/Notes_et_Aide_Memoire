# Angular

Caractéristiques :

- Permet de développer des Single Page Applications (ou SPA)
- Framework complet (pas de librairies tierces nécessaire)
- Impose des  *best practices* dans la structure du code
- Utilise TypeScript et SCSS

## Installation du CLI

`npm i -g @angular/cli`  
vérifier l'installation : `ng v`
Obtenir l'aide : `ng help`

## Démarrer un nouveau projet

`ng new nom-projet <options>` => génère un dossier avec tout les fichiers d'une application Angular, installe les dépendances du projet et initialise un dépôt Git  

Options : 
- `--skip-tests=true` : Ne pas générer des fichiers de tests unitaires
- `--style=scss` : Utiliser SCSS
- `--routing=true` : générer un fichier qui va permettre de créer des routes
- `--minimal` : installation minimal
Pour afficher la liste des options : `ng new --help` 

Pour lancer le serveur de développement : `ng serve`  (Il faut que la commande soit lancer dans le dossier du projet) 
Options :
- `-o` : ouvrir l'application dans le navigateur

## Arborescence du projet

Le dossier `src` contient les fichiers de l'application

- `index.html` : fichier principal. La balise `<app-root>` permet d'inclure le `AppComponent` qui est le composant racine de l'application
- `app/
	- `app.component.html` : template HTML de  `AppComponent`
	- `app.component.scss` : code SCSS de  `AppComponent`
	- `app.component.ts` : configuration de  `AppComponent`
	- `app-routing.module.ts`: Configuration des routes de l'application
	- `app.module.ts` : fichier de déclaration des modules
- `assets/` : contient images, icones, fonts etc..
- `environments/`: variables d'environnement du projet
- `angular.json` : configuration d'Angular
- `tsconfig.json` : configuration de TypeScript
- `tsconfig.app.json` : Configuration de TypeScript pour la compilation du TS de l'application


## Injection de dépendances 

Système d'injection de dépendances (dependency injection ou DI) 
=> consiste à résoudre les dépendances d'un component en les injectant via le constructeur

`constructor(private _property: ClassName){} 

## Variables d'environnements 

Deux fichiers pour les variables d'environnement  
- *environments.ts* : contient les variables qui seront utilisées lors du développement de l'application
- *environments.prod.ts* : contient les variables qui seront utilisées lors de la mise en production de l'application 
Lors du build, Angular remplace le fichier de dev par le fichier de prod 

les variables d'environnements sont utilisées pour tout ce qui concerne l'accès à des API, base de données, etc... 
Il est fortement recommandé d'utiliser des données fictives (ou des données mises à disposition spécifiquement pour le dev)  lors de la phase de développement pour ne pas compromettre les données réelles en prod. 

Pour utiliser une variable d'environnement 
```ts
import { environment } from 'src/environments/environment';

//***
let variable = environnement.variable

```











