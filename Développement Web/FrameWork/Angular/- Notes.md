# Notes

```html
<!-- si 'toto' existe et qu'il a la propriété 'id' (deux syntaxe possible) -->
{{toto ?? toto.id }}
{{toto?.id}} 
```
--------------

`--dry-run` : permet de tester une commande. Celle ci affiche le résultat mais ne fait rien en réalité.

-------------------

Un provider est un objet que l'on déclare à Angular pour qu'il puisse l'injecter à différentes endroits de l'application.

D'ailleurs, même si vos services ne figurent pas ici, ce sont des providers également ! Ils sont déclarés avec  @Injectable()  et Angular peut ensuite les injecter là où vous en avez besoin, comme via le constructor de vos components, par exemple.

--------------------------------

La commande  `ng add`  permet d'ajouter certaines bibliothèques à un projet Angular. En plus d'installer les packages  `npm`  nécessaires,  `ng add`  va **configurer** le projet pour le préparer à l'utilisation de la bibliothèque.

-----------------

Astuce Shared Module 

Si on a besoin d''utiliser un module à plusieurs endroits il faut l'importer dans un Shared Module puis indiquer le module dans `export`. Par contre si le shared Module  n'utile pas lui même le module on a pas besoin de l'indiquer dans `imports` 

Exemple : 

```ts
import { MatToolbarModule } from '@angular/material/toolbar';
@NgModule({
  declarations: [],
  // on importe pas le module car on en a pas besoin dans le SharedModule
  imports: [CommonModule],
  // on export le module pour qu'il disponible dans tout l'app
  exports: [MatToolbarModule],
})
export class SharedModule {}

```

Il faut faire attention à ce que le SharedModule soit bien importé dans tout les autres modules 

-----------------

Très souvent, on appellera une méthode de **service** dans le `ngOnInit` d'un component. Cette méthode retournera un Observable qui correspond à une **requête HTTP**. On souscrit à cet Observable, la requête est envoyée, et quand le serveur répond, on **affiche** les données dans le template. La souscription se fait souvent avec **le pipe `async`**  .
L'autre approche est d'utiliser un resolver

----------------------------

Astuce
Quand un module imports de nombreux autre modules, il peut être intéressant de créer un autre fichier module pour pouvoir les regrouper. (Ne pas oublier d'ajouter ce fichier module au imports/exports du module principal


--------------
Un Pipe est une fonction **pure** : c'est-à-dire que ce qu'elle retourne ne dépend que des arguments qu'on lui passe. Elle n'a pas d'autres dépendances, et ne modifie aucune valeur extérieure. Ce sont donc des éléments très faciles à tester !

---------------------------
Une méthode  `private`  ne peut pas être appelée depuis le template.
Ça évite d'avoir de **l'autocomplétion** dans le template, par exemple, pour une méthode qui ne doit pas y être appelée. Ça explique aussi à vos coéquipiers (ou à vous-même six mois plus tard !) que cette méthode est **prévue** pour être appelée à l'intérieur du component.


-------------------

fonctions utilitaires
-   fonctions statiques helper (à ranger dans un dossier helpers)
-   faire une export

------------------------

Programmation réactive / RxJS
-   switchMap => le flux précédent est stoppé avant de passer aux flux suivant
-   contactMap => Le flux précédent doit être terminé avec de passer au flux suivant
-   mergeMap => on traite les flux en parallèle.






