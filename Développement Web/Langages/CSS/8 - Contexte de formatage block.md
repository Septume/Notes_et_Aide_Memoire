# Contexte de formatage block

# Définition

Ce contexte est créé dans les situations suivantes :

- Éléments flottants
- Éléments en position absolue ou fixe
- Blocs en ligne (`inline-block`)
- Cellules de tableau ( `table-cell`)
- Titres de tableau ( `table-caption`)
- Les éléments où `overflow` a une valeur autre que `visible`
- Les boîtes flexibles (`flex` ou `inline-flex`)

Attention : Un élément en `display:block` ne crée pas de contexte de formatage block

Un élément générant un contexte de formatage block a les caractéristiques suivantes :

- Ses éléments enfants s'affichent les uns en dessous des autres
- Peut contenir des éléments enfants flottants
- Ne s'écoule pas autour des flottants externes
- Ne subit pas la fusion des marges avec ses enfants

## Cas d'utilisation

### Contenir des flottants

Comme les éléments flottants sont hors du flux, ces derniers peuvent “déborder” de leur parent. Avec un parent possédant un contexte de formatage block, les éléments flottant peuvent être contenus.

```html
<div class="container">
    <div class="float"></div>
	<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. 
    Libero alias voluptate ducimus amet quasi 
    Beatae quaerat, nisi consectetur commodi
  </p>
</div>
```

```css
.container {
	border: 1px solid black;  
	/* permet de créer un contexte de formatage block
	empechant le dépassement du flottant */
	overflow: hidden; 
}

.float {
	width: 200px;
	height: 200px;
	background: red;
	float: left;
	margin-right: 10px;
}
```

### Écoulement autour d’un flottant

Le contenu qui suit un élément flottant s’écoule autour de celui-ci.

Mais si ce contenu bénéficie d’un contexte de formatage block, il ne s’écoule plus et reste calé à droite du flottant

```html
<div class="container">
	<div class="float"></div>
	<p class="content">
		Lorem ipsum dolor sit amet, consectetur adipisicing elit
		Numquam dolorum non eveniet doloribus ! 
		In rerum aspernatur, dolorum molestiae molestias. 
		Lorem ipsum dolor sit amet, consectetur adipisicing elit. 
		Maxime tempore explicabo aliquam laboriosam.
	</p>
</div>
```

```css
.container {
	width: 400px;
}

.float {
	width: 100px;
	height: 100px;
	background-color: red;
	float: left;
	margin-right: 10px;

}

.content {
	/* contexte formatage block */
	overflow: hidden;
}
```

### Fusion des marges

Utiliser un contexte de formatage sur le block parent empêche la fusion des marges
