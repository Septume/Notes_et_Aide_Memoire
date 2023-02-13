# Animations

Pour utiliser les animations il faut importer  `BrowserAnimationsModule`

```ts
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
```

On ajoute les animations dans le décorateur `@component` 
- On utiliser la propriété `animations` qui prend comme valeur un tableau d' animations 
- On utilise la fonction `trigger()` pour créer une animation. Elle prend en paramètres
  - le nom de l'animation
  - Un tableau qui contient les éléments de l'animation

```ts

import { trigger } from '@angular/animations';

@Component({
  selector: 'app-comment',
  templateUrl: './comment.component.html',
  styleUrls: ['./comment.component.scss'],
  animations: [
  trigger('AnimName1', []),
  trigger('AnimName2', [])
  ],
})
```

```html
<div @animName1></div>
<div @animName2></div>
```

## Définir des états 

