# Sectionnement

### Titres

`<h1>` …. `<h6` : Niveau de titre. Les titres permettent de créer des sections implicites. Les éléments de section peuvent avoir leur propre hiérarchie de titre par rapport à l’ensemble de la page. Il est recommandé de ne jamais sauter des niveaux et de n’avoir qu’un seul titre de niveau 1 par section.

`<hgroup>` : Section regroupant plusieurs titres de différents niveaux. Dans ce cas seul le titre du plus haut niveau sera pris en compte dans le plan (outline) du document. Cela permet d’indiquer des titres de niveau plus bas comme un sous-titre ou un titre alternatif sans que cela infecte le plan du document. Attention : cet élément doit contenir exclusivement des éléments titres. cet élément est en général contenu dans un `header`

Remarque : Si on a besoin de créer une hiérachie visuelle différente de la hiérachie sémantique on peut utiliser des classes `.h1`, `.h2`, etc, reprenant les styles CSS définis pour les différents niveaux titres.

### Sections

Remarque : chaque sections peut avoir sa propre hiérarchie de titre

`<body>` : section principale représentant la page

`<header>` : Entête de page ou de section. (Exemple de contenu : titre, éléments de navigation, métadonnées, table des matières)

`<footer>` : Pied de page ou de section. (Exemple de contenu : mentions légales, informations de contact, source d’une actualité, navigation)

`<section>`: Section générique permettant de regrouper des contenus en fonction de leur thématique ou de leur fonctionnalité (ex : groupes d’articles sur la même page, article scindé en plusieurs chapitres).

`<article>`: Section de contenu indépendant, pouvant être individuellement extrait du document ou être diffusé via un flux de syndication sans pénaliser sa compréhension. ( Ex : une actualité, une fiche d’information…). Peut contenir des éléments `section`, `header`, `footer` ou `nav`. Peut également contenu un autre élément `article` (Ex : commentaire sur un billet de blog)

`<main>` : Contenu principal (ou fonctionnalité centrale). Ce contenu doit être unique au sein du site ou de l’application, ce qui exclus tout contenus qui se répètent sur l’ensemble des pages (header, navigation, ..). Il doit y avoir qu’un seul élément `main` actif dans le document. (les autres éléments `main` doivent être désactivés avec l’attribut `hidden`). Un élément main ne doit pas être un enfant d’un élément `article`, `aside`, `footer`, `header` ou `nav`. Idéalement cet élément doit être descendant d’un élément `<html>`, `<body>`, `<div>`, ou `<form>`

`<nav>` : Section contenant les liens de navigation principaux. Un document peut avoir plusieurs éléments `nav`. Pour indiquer les différents liens on utilise en général une liste `<ul>`

```html
<nav>
	<ul>
		<li><a href="#">Accueil</a></li>
		<li><a href="#">A propos</a></li>
		<li><a href="#">Contact</a></li>
	</ul>
</nav>
```

`<aside>`: Section pour regrouper des informations connexes au contenu principal. (Exemple : biographie, glossaire, note, publicité, etc.). Peut également être utilisé pour indiquer un barre de menu latéral (sidebar). Si il est contenu dans un `article` les informations doivent être connexes au contenu de l’article.

`<address>` : Section regroupant des informations de contact (mail, adresse postale, téléphone…)
