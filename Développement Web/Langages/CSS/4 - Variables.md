# Variables

## Variables css (ou propriétés personnalisées)

Définition : `-nomVariable : valeur;` Attention, les variables ne peuvent être définies qu'à l'intérieur du bloc de déclaration d'un sélecteur CSS

Appel : `var(--nomVariable)`

Les règles d'héritage s'appliquent de la même manière que pour les propriétés classiques.

La variable doit être définie au niveau de l’élément `html` pour être accessible dans tout le document. Il est conseillé d’utiliser la pseudo classe `:root` qui permet de cibler l’élément `html`mais avec une plus grande spécificité.

```css
:root { 
	--primary-color : blue;
}
.box {
	background: var(--primary-color);
}
```

Il est possible d’appeler une variable en indiquant une valeur par défaut si celle-ci n’a pas été définie

```css
background: var(--primary-color, red);
```

On peut redéfinir la variable au niveau d’un autre élément

```css
:root {
	--primary-color : blue;
}

.item1 {
	/* cette élément sera bleu */
	background: var(--primary-color);  
}

.item2 {
	/* cette élément sera rouge */
	--primary-color : red;
	background: var(--primary-color);
}

.item3 {
	/* cette élément sera bleu */
	background: var(--primary-color);
}
```

Remarque : Il est possible d'utiliser les valeurs des propriétés personnalisés en JavaScript de la même façon que les propriétés classiques

## Variables d'environnement

Il s'agit de variables qui sont globales au document. Elles peuvent être utilisées à n'importe quel endroit où les valeurs CSS sont autorisées (propriétés, règles `@`,…). Ces variables sont définies au niveau du navigateur. Pour l'instant il n'est pas possible de créer ses propres variables d'environnement. (Voir évolution de la spécification)

les variables d'environnement disponible :

- `safe-area-inset-top`
- `safe-area-inset-right`
- `safe-area-inset-bottom`
- `safe-area-inset-left`

⇒ Permet de définir une *safe area.* Il s'agit d'une zone de l'écran dans lequel le contenu peut être affiché de manière sur sans être rogné. (Remarque : Ces variables d'environnement ont été proposées par Apple pour permettre de gérer l'affichage sur l' iphone X qui a une zone d'encoche (*notch*) sur l'écran pouvant masqué du contenu si une *safe area* n'a pas été défini)

Pour utiliser une variable d'environnement on utilise la fonction `env()` qui prend en argument la variable. On peut également indiquer comme deuxième argument une valeur de substitution au cas où si la variable d'environnement n'est pas pris en charge. Par exemple : `env(safe-area-inset-top, 20px)`
