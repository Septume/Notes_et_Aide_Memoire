
### Installation

Permet  de créer facilement des routes dans react
(dom@6 => installation de la version 6)
```bash
npm install react-router-dom@6
```

puis aller dans `index.jsx` et ajouter
```tsx
import { BrowserRouter } from 'react-router-dom';
```

![[Capture d’écran du 2023-02-17 14-31-16.png]]

Puis aller sur `App.jsx` et import 
```tsx
import { Routes, Route } from 'react-router-dom';
```

![[Capture d’écran du 2023-02-17 14-47-56.png]]

### Menus Navigation

Importer `NavLink` dans le `react-router-dom`.

Puis créer une section `<nav> </nav>` qui va accueillir les *NavLink* 

![[Capture d’écran du 2023-02-17 15-02-48.png]]