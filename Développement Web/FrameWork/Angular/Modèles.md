# Modèles

Fichier dans lequel on définit des classes permettant d'instancier des objets
les modèles permettent également de créer des types

Pour créer le modèle

`models/nameModel.model.ts`

```ts
export class NomClass {
constructor()
}
```

Exemple

```ts
export class Card {
  title: string;
  description: string;
  imageUrl: string;
  createdDate: Date;

  constructor(title: string, description: string, imageUrl: string, createdDate: Date) {
    this.title = title;
    this.description = description;
    this.imageUrl = imageUrl;
    this.createdDate = createdDate;
  }
}
```

TypeScript permet d'utiliser une syntaxe plus courte

```ts
export class Card {
  constructor(public title: string, public description: string, public imageUrl: string, public createdDate: Date) {}
}
```

Cette syntaxe permet de dire que les paramètres du constructeur sont liés à des propriétés de la classe. (Attention : pour que ça fonctionne `public` doit être obligatoire)

Pour utiliser le modèle dans un composant il faut l'importer  
`import { ModelName } from './../models/ModelName.model';`