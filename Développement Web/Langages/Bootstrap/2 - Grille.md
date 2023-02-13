# Grille

## Fonctionnement

### Caractéristiques de la grille

- Largeur de 100% (grille fluide) ou max en fonction du device (grille fixe centrée)
- Un padding à gauche et à droite de la grille de 15px
- Basée sur 12 colonnes de largeur égale. La largeur est calculée en % et dépend donc de la taille de l'écran. Si la somme des colonnes est plus grande que 12, cela provoque un renvoie à la ligne des blocs suivants
- Gouttières de largeur fixe de 30px (Quel que soit la largeur de l'écran)

### Caractéristiques en fonction des device

**Extra small (Smartphone en mode portrait )**

- breakpoint : `< 576px`
- Largeur max du conteneur fixe : `auto`
- Classe de colonne : `col-*`

**Small (Smartphone en mode paysage )**

- breakpoint : `>= 576px`
- Largeur max du conteneur fixe : `540px`
- Classe de colonne : `col-sm-*`

**Medium (Tablette)**

- breakpoint : `>= 768px`
- Largeur max du conteneur fixe : `720px`
- Classe de colonne : `col-md-*`

**Large (Desktop)**

- breakpoint : `>= 992px`
- Largeur max du conteneur fixe : `960px`
- Classe de colonne : `col-lg-*`

**Extra-large (Desktop avec écran large)**

- breakpoint : `>= 1200px`
- Largeur max du conteneur fixe : `1140px`
- Classe de colonne : `col-xl-*`

## **Container**

Obligatoire pour placer la grille.

Deux classes de container :

- `container` : Container fixe. Largeur max à chaque breakpoint
- `container-fluid` : Container fluide. 100% de la largeur

Propriétés :

- `padding-left` et `padding-right` de 15px
- `margin-left` et `margin-right` en auto (permet de centrer la grille)

Remarque :

- Le container peut être placé au niveau de body (dans ce cas le comportement de la grille s'appliquera sur toute la largeur de la fenêtre)
- On peut imbriquer des containers (Bien que la plupart des mises en page n'en ont pas besoin)

## **Lignes**

Contient les colonnes

Classe : `row`

Propriétés :

- `display: flex`
- `wrap` : les éléments retournent à la ligne s’il n'y a plus de place
- `margin-left` et `margin-right` de -15px (margin négatif chaque côté permettant d' harmoniser le padding des colonnes)

Les lignes doivent avoir comme enfants immédiats uniquement des colonnes

Autres classes :

`no-gutters` : supprime les gouttières (à appliquer sur l'élément `row`)

## **Colonnes**

Permet de placer le contenu

Classes :  
`col-x,` `col-sm-x`, etc. (ou x est le nombre de colonnes)

Propriétés :

- `padding-left` et `padding-right` de 15px (gouttières)

Remarque :

- Si on ne définit pas une classe `col-*` pour un device, c'est les propriétés définies pour le device d'affichage inférieure qui s'appliquent ⇒ Approche mobile-first
- il est possible d'imbriquer des colonnes dans des colonnes (nested) On indique pour cela une `row` dans un `col` qui va reprendre un nouveau contexte à 12 colonnes

Exemple 1

```html
<div class="container">
	<div class="row">
	<!-- 3 blocs de 4 colonnes  -->
		<div class="col">
		Lorem ipsum dolor sit amet, consectetur adipisicing elit
		</div>
		<div class="col">
		Lorem ipsum dolor sit amet, consectetur adipisicing elit
		</div>
		<div class="col">
		Lorem ipsum dolor sit amet, consectetur adipisicing elit
		</div>
	</div>
</div>
```

Exemple 2

```html
 <div class="container">
    <div class="row">
      <!--
      12 colonnes sur les smartphones portrait (1 bloc par ligne)
      6 colonnes sur les smartphones paysage (2 blocs par ligne)
      4 colonnes ur les tablettes (3 blocs par ligne)
      2 colonnes sur les écran taille standard et large (6 blocs par ligne)
	    -->
      <div class="col-12 col-sm-6 col-md-4 col-lg-2">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit
      </div>
      <div class="col-12 col-sm-6 col-md-4 col-lg-2">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit
      </div>
      <div class="col-12 col-sm-6 col-md-4 col-lg-2">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit
      </div>
      <div class="col-12 col-sm-6 col-md-4 col-lg-2">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit
      </div>
      <div class="col-12 col-sm-6 col-md-4 col-lg-2">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit
      </div>
      <div class="col-12 col-sm-6 col-md-4 col-lg-2">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit
      </div>
    </div>
  </div>
 
```

`offset-x`, `offset-sm-x`, etc : décale un élément vers la droite (via un `margin-left`) de x colonnes (Les éléments à la suite sont également décalés)
