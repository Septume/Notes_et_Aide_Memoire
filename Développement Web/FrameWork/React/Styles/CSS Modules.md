Un module CSS est un fichier CSS dans lequel tous les noms de classe et d'animation ont une portée locale par défaut. 
Toutes les URL (`url(...)`) et les `@imports` sont au format de requête de module (`./xxx` et `../xxx` signifient relatif, `xxx` et `xxx/yyy` signifient dans le dossier des modules, c'est-à-dire dans `node_modules`).

Les modules CSS sont compilés dans un format d'échange de bas niveau appelé ICSS ou Interoperable CSS, mais sont écrits comme des fichiers CSS normaux :

```css
/* style.css */
.className {
  color: green;
}
```

Lorsque le module CSS est importé d'un module JS, il exporte un objet contenant toutes les correspondances entre les noms locaux et les noms globaux.

```js
import styles from "./style.css";
// import { className } from "./style.css";

element.innerHTML = '<div class="' + styles.className + '">';
```

#### Nom
Pour les noms de classes locales, l'utilisation de camelCase est recommandée, mais non imposée.

```
Cette recommandation est motivée par le fait que l'alternative courante, la casse kebab, peut provoquer un comportement inattendu lorsque l'on tente d'accéder à style.class-name en notation par points. Vous pouvez toujours contourner la casse kebab avec la notation entre crochets (par exemple, style['class-name']) mais style.className est plus propre.
```

#### Exceptions
`:global` passe en portée globale pour l'identifiant respectif du sélecteur actuel. `:global(.xxx)` respective `@keyframes :global(xxx)` déclare les éléments entre parenthèses dans la portée globale.

De même, `:local` et `:local(...)` pour la portée locale.

Si le sélecteur passe en mode global, le mode global est également activé pour les règles. (Cela nous permet de rendre l'`animation : abc` ; locale).

Exemple : `.localA :global .global-b .global-c :local(.localD.localE) .global-d`

#### Composition
Il est possible de composer des sélecteurs.

```css
.className {
  color : green ;
  background : red ;
}

.otherClassName {
  composes : className ;
  color : yellow ;
}
```

Il peut y avoir plusieurs règles de `composition`, mais les règles de `composition` doivent être placées avant les autres règles. L'extension ne fonctionne que pour les sélecteurs à portée locale et uniquement si le sélecteur est un nom de classe unique. Lorsqu'un nom de classe compose un autre nom de classe, le **CSS Modules** exporte les deux noms de classe pour la classe locale. Cela peut donner lieu à plusieurs noms de classe.

Il est possible de composer plusieurs classes avec `composes : classNameA classNameB ;`.

#### Dépendances
###### Composition à partir d'autres fichiers
Il est possible de composer des noms de classes à partir d'autres **CSS Modules**.

```css
.otherClassName {
  composes : className from "./style.css";
}
```

Notez que lorsque vous composez plusieurs classes à partir de différents fichiers, l'ordre d'application n'est pas défini. Veillez à ne pas définir des valeurs différentes pour la même propriété dans plusieurs noms de classe provenant de fichiers différents lorsqu'ils sont composés dans une seule classe.

Notez que la composition ne doit pas former une dépendance circulaire. Par ailleurs, il n'est pas défini si les propriétés d'une règle remplacent les propriétés d'une règle composée. Le système de modules peut émettre une erreur.

C'est mieux si les classes font une seule chose et que les dépendances sont hiérarchiques.

###### Composition à partir de noms de classes globales
Il est possible de composer à partir de noms de classes globales.

```css
.otherClassName {
  composes : globalClassName from global;
}
```

#### Utilisation avec les préprocesseurs
Les préprocesseurs peuvent faciliter la définition d'un bloc global ou local.

Par exemple, avec less.js

```css
:global {
  .global-class-name {
    color : vert ;
  }
}
```
