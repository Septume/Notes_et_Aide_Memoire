# Bonnes pratiques

## Le principe de responsabilité unique

 - Définit un seul élément par fichier (composant, module, service, …) afin de facilité la lecture et la maintenance de l'application. En général les fichiers ne doivent pas dépasser les 400 lignes. 
 - Définir des petites fonctions plutôt que des fonctions trop importantes, car plus facile à tester, lire et maintenir. Cela encourage aussi la réutilisation du code. En général les fonctions ne doivent pas dépasser les 75 lignes

## Convention de nommage 

Fichiers : 
- Utiliser la syntaxe `kebab-case` pour le nom des fichiers
- Utiliser des nom de fichier consistant sous la forme `feature-name.type.extension` 
Exemple : `list-user.component.ts` , `list-user.component.html` , `user.service.ts` 

Éléments : 
- Utiliser la syntaxe `PascalCase` pour le nom des classes (Ex: `ListUserComponent` ) 
- Utiliser la syntaxe `camelCase` pour le nom des propriétés et méthodes. Préfixer les propriétés et méthodes privées par un underscore `_` 
- Utiliser la syntaxe `kebab-case` pour le nom des sélecteurs de components ou directives. Utiliser également un préfixe personnalisé. (ex: `app`, `admin` etc...) 

## Convention de code 

Privilégier `const` plutôt que `let` , sauf si  la valeur doit changer au cours du traitement. Pour le nom des constantes, préférer la syntaxe `camelCase` plutôt que le `UPPER_SNAKE_CASE` (qui est traditionnellement utilisé pour les constantes mais moins facile à lire) 

Toujours typer les propriétés, paramètres, retour de méthode (même vide) , etc...

Déclarez les propriétés avant les méthodes et les éléments privés après ceux qui sont publics, par ordre alphabétique.

Trier les règles d'import par ordre alphabétique


## Organisation des dossiers/fichiers 

Les modules sont organisés en dossier et qui contient des sous-dossiers pour chaque type de fichiers (components, services, models, etc...).
Créer également un dossier par component 
Les nom de dossiers sont toujours au pluriel  
Les nom de fichier sont au singulier

## Structure de l'application 

Règle **LIFT** 
  - Locate => Pouvoir localiser le code rapidement
  - Identify => Pouvoir identifier le code  rapidement
  - Flat => Avoir une structure la plus plate possible (moins de 7 fichiers par dossier) 
  - Try => Essayer d'être DRY = Don't Repeat Yourself 



### Organisation des modules

**App Module**   
Module racine. Prend en charge le chargement des autres modules. 

**Core Module**   
Module qui contient des éléments partagés dans toute l'application mais qui ont besoin d'être importées qu'une seule fois
- Services singleton (instanciés qu'une seule fois)
- Composants : Login, header, home, page erreur 404
- Modèles, utils, helpers, guards etc...
Le Core Module doit être importé qu'une seule fois dans le AppModule

Pour éviter que le core module soit importer ailleurs ont peut ajouter ce code dans le constructor de ce dernier
```javascript
export class CoreModule {
  constructor(@Optional() @SkipSelf() parentModule: CoreModule) {
    if (parentModule) {
      throw new Error(
        'CoreModule is already loaded. Import it in the AppModule only.'
      );
    }
  }
}
```


**Shared Module**   
Contient des components, pipes, directives réutilisables et accessibles dans toutes l'application ainsi que des modules à partager (Par ex : RouterModule, FormsModule, ReactiveFormsModule, modules Material et autres modules de bibliothèque) 
Ces éléments devront être exportés  pour être accessible à tout les autres modules.   
Le Shared Module peut être importé plusieurs fois dans l'application (AppModule et Feature Module) 

**Feature Module**   
Module correspondant à une fonctionnalité et qui contient des components, services et modèles qui seront utilisés que pour ce module. 
Pour une meilleure organisation on peut utiliser un préfixe commun à tout les fichiers du module (qui correspond au nom de la fonctionnalité) 
Pour chaque Feature Module on peut également créé un module de routage 


### Components

**Architecture Container / Presente**r (appelé aussi Smart/Dumb) 
- **Container** : component parent qui s'occupe de la logique, de l'interaction avec les services. 
- **Presenter** : components enfants qui s'occupent de la présentation. Pas d'interactions avec les services. ils se contentent d'afficher les données envoyées par le  parent via des `Input()` 
**Bubble Up** : consiste  à retransmettre un évènement au component parent Container pour que ce dernier le transmettre à un service. On utilise pour cela les `@output()` 








 