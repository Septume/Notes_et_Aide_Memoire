# Components standalone


Nouvelle fonctionnalité d'Angular 14 
Concerne également les directives et les pipes 

Standalone = Ne fait parti d'aucun module 

On peut avec le CLI utiliser l'option `--standalone` pour créer l'élément

```ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  stylesUrl: './app.component.css',
  // option pour rendre le component standalone
  standalone: true,
  // Modules nécessaires au component (utiliser seulement si standalone = true) 
  imports: [CommonModule]
})
```

  Attention : pour rendre un component existant standalone il ne faut pas oublier de le supprimer du tableau déclaration de son module 
  


