# Images, médias et contenus embarqués

### Images

Principaux formats pris en charge par les navigateurs

- PNG `image/png`
- JPEG `image/jpeg`
- SVG `image/svg+xml`
- GIF `image/gif`
- WebP `image/webp`
- ICO `image/x-icon`

`<img />` : Élément remplacé par ses dimensions originales. Pour rentre une image cliquable on peut la placer dans un élément `a`

- `src` : **Obligatoire**. URL de l’image.
- `alt`: **Obligatoire**. Texte alternatif décrivant l’image. Si l’image est purement décorative on peut laisser vide `<img alt= "">`
- `height` : hauteur de l’image en px
- `width` : largeur de l’image en px
- `ismap`: Attribut booléen. Indique au navigateur qu’il doit transmettre au serveur les coordonnées du point cliqué sur l’image. A utiliser uniquement sur une image cliquable.
- `usemap` : Le nom d’un élément `map` auquel est associée l’image si c’est le cas. Ce nom doit être précédé du signe dièse
- `srcset` : Permet d'indiquer plusieurs sources d'images. Le navigateur choisira celle qui convient le mieux en fonction du contexte (viewport, résolution de l'écran cible, débit…). Si aucune convient c'est l'image indiqué dans `src` qui sera utilisée. Chaque image est décrite dans une chaine de caractères (Les chaines sont séparés par une virgule). On indique l'URL de l'image suivi éventuellement d'un descripteur :
	- `x` (Pixel density descriptor ) : correspond à la résolution (densité de pixel) de l'écran à cibler. La valeur est un nombre positif, entier ou décimal. Par défaut la valeur est `1x`

		
		```html
        <img src="image.jpg" srcset="imageHD.jpg 2x" alt="">
        ```
		

	- `w` (Width descriptor ) : indique la largeur réelle de l'image en pixels. Le navigateur choisira celle qui correspond le mieux en fonction du contexte.

		
		```html
        <img src="image.jpg" 
             srcset="image-320.jpg 320w,
        						 image-640.jpg 640w"
             alt="">
        ```
		

- `sizes` : A associer avec le descripteur `w` de l'attribut `scrset` . Permet d'indiquer la largeur de l'image à l'affichage. La valeur peut être exprimée en px ou vw. La valeur par défaut est `100vw`. Il est possible d'utiliser des media queries.

	
	```html
    <!-- L'image s'affiche sur toute la largeur du viewport-->
    <img src="image.jpg" 
         srcset="image-320.jpg 320w,
    						 image-640.jpg 640w"
    		sizes="100vw"
         alt="">

    <!-- utilisation de media queries -->

    <img src="image.jpg" 
         srcset="image-320w.jpg 320w, 
                 image-480w.jpg 480w, 
                 image-800w.jpg 800w" 
         sizes="(max-width: 320px) 280px, 
                (max-width: 480px) 440px, 
                800px"
         alt="">

         
    ```
	

- `loading` : Permet d'indiquer la manière dont le navigateur doit charger l'image
	- `eager` (Défaut) : Charge l'image immédiatement
	- `lazy` : Charge l'image uniquement lorsqu'elle se trouve à une certaine distance de la fenêtre de visualisation. Utile lorsqu'il y a beaucoup d'images qui s'affichent en faisant défiler la page.
- `decoding` : Permet d'indiquer si l'image doit être décodée de manière synchrone ou asychrone
	- **`sync`**
	- **`async`** (Permet de réduire le temps nécessaire à la présentation du reste du contenu)
	- **`auto`** (Défaut). Le mode par défaut qui indique l'absence de préférence pour le mode de décodage. Dans ce cas, l'agent utilisateur décide de la meilleure stratégie.
- `crossorigin` : Indique si le CORS (Cross-Origin Ressource Sharing) doit être utilisé lors de la récupération de la ressource liée (Si l’attribut n’est pas présent le CORS n’est pas utilisé)
	- `"anonymous"`: autorise les requêtes cross-origin mai sans permettre l’authentification ou les cookies
	- `"use-credentials"`: permet également l’authentification et les cookies
- `referrerpolicy`

Indiquer explicitement les dimensions de l’image via `width` et `height` permet dès le chargement du code HTML d’allouer l’espace requis pour l’affichage de l’image sans devoir attendre la fin du chargement de celle ci. Il dont recommandé d’indiquer ces dimensions pour une meilleure performance. Idéalement il faut indiquer la taille réelle de l’image. Sinon l’image sera redimensionné par le navigateur avec un risque que les proportions ne soient pas respectée

### Images map

`<map>` : Image constituée de zones distingues contenant chacune un lien.

- `name` : **Obligatoire**. Permet de faire une association avec un élément `img` via son attribut `usemap`

`<area />` : Pour définir une zone cliquable (À utiliser uniquement dans un élément `map`)

- `href` : Cible du lien
- `hreflang` : Code langue de la cible
- `alt` : Texte alternatif
- `rel`: Relation avec la cible
	- `alternate`
	- `author`
	- `help`
	- `license`
	- `next` et `prev`
	- `search`
	- `bookmark`
	- `external`
	- `nofollow`
	- `noopener`
	- `noreferrer`
	- `tag`
- `target` : Contexte de navigation dans lequel afficher la cible
- `shape` : Forme de la zone cliquable :
	- `rect` : rectangle
	- `circle` : cercle
	- `poly` : polygone
	- `default` : rectangle couvrant la totalité de l’image
- `coords` : Cordonnées de la forme par rapport au coin supérieur gauche de l’image, en pixels. Les valeurs possibles sont :
	- pour `rect` : x1, y1, x2, y2
	- pour `circle` : x, y, rayon
	- pour `poly` : x1, y1, x2, y2, x3, y3,…
- `ping` : Contient une liste d’URL séparées par des espaces vers lesquelles sont envoyées des requêtes `POST` avec le corps `PING` lorsque l’utilisateur suit le lien. Cet attribut est généralement utilisé pour tracer un utilisateur.
- `referrerpolicy`

```html
<img src="map.jpg" alt="image cliquable" usemap="#map">
<map name="map">
	<area shape="rect" coords="264,233,404,423" href="#">
	<area shape="rect" coords="410,232,540,412" href="#">
	<area shape="rect" coords="545,229,657,398" href="#">
	<area shape="rect" coords="663,218,780,390" href="#">
</map>
```

### Images adaptatives

`<picture>`: Conteneur permettant de définir plusieurs source pour l’affichage d’une image. Cet élément doit contenir un élément `<source>` qui contient la définition des différentes sources et un élément `<img>` obligatoire pour indiquer une image à afficher par défaut.

`<source>` : Balise autofermante. (Remarque : Cet élément est également utilisé avec les éléments `audio` et `video` mais avec des attributs différents)

- `media` : Sélection de l’image en fonction d’une requête media
- `type` : Sélection de l'image en fonction
- `srcset`
- `sizes`

```html
<picture> 
	<source srcset="logo-wide.png" media="(min-width: 800px)">
	<source srcset="logo-medium.png" media="(min-width: 600px)">
	<img src="logo.png" alt="logo"> 
</picture>
```

```html
<picture>
  <source type="image/svg+xml" srcset="image.svg">
  <source type="image/webp" srcset="image.webp"> 
  <img src="image.png">
</picture>
```

### Audio et vidéo

`<audio>` : Contenu audio. On peut indiquer à l’intérieur des balises un contenu alternatif qui s’affichera si le navigateur ne prend pas en charge l’élément.

- `autoplay` : Attribut booléen. Active la lecture automatique au chargement du fichier.
- `controls` : Attribut booléen. Affiche les contrôles par défaut du navigateur. (On peut créer ses propres contrôles avec l’API JS `HTMLMediaElement`)
- `loop` : Attribut booléen. Le fichier sera lu en boucle
- `muted` : Attribut booléen. Le son est initialement coupé.
- `preload`: Indication sur le pré-chargement du fichier. A noter que les navigateurs restent libre de respecter cette indication ou pas.
	- `auto` : Défaut. Le navigateur décide s’il doit précharger le contenu, ou uniquement les métadonnées ou ne rien précharger (peut dépendre du type de connexion)
	- `metadata` : Précharge uniquement les métadonnées
	- `none` : pas de pré-chargement
- `src` : URL du fichier. Cette attribut est optionnel si on utile l’élément `<source>`
- `crossorigin` : Indique si le CORS (Cross-Origin Ressource Sharing) doit être utilisé lors de la récupération de la ressource liée (Si l’attribut n’est pas présent le CORS n’est pas utilisé)
	- `"anonymous"`: autorise les requêtes cross-origin mai sans permettre l’authentification ou les cookies
	- `"use-credentials"`: permet également l’authentification et les cookies

Les formats audio les plus utilisés :

- MP3 `audio/mpeg`
- Vorbis/Ogg `audio/ogg`

`<video>` : Contenu vidéo. On peut indiquer à l’intérieur des balises un contenu alternatif qui s’affichera si le navigateur ne prend pas en charge l’élément.

- `autoplay`
- `controls`
- `loop`
- `muted`
- `preload`
- `src`
- `poster` : Image à afficher lorsque la vidéo n’est pas lancée. Par défaut le navigateur affiche la première image de la vidéo.
- `width` : Largeur du lecteur en px
- `height` : Hauteur du lecteur en px
- `buffered` :
- `playsinline` : Attribut booléen. Indique que la vidéo doit rester affichée en ligne (c.a.d. pas en plein écran) lorsqu'on lance la lecture sur certains appareils.

Les formats vidéos les plus utilisés :

- MP4 : contient de l’audio AAC ou MP3 avec de la vidéo H.264
- WebM : contient de l’audio Ogg Vorbis avec de la vidéo VP8/VP9

`<source>` : Permet d’indiquer plusieurs versions du média audio ou vidéo dans des formats différents. Le navigateur choisira dans la liste le premier média dont le format est pris en charge.

- `src` : URL du média
- `type` : Type MINE du média

`<track>` : Élément à utiliser à l’intérieur d’un élément `<audio>` ou `<video>` . Permet d’indiquer une piste de texte pour le média. Les formats pris en charge sont le WebVTT ( Web Video Text Tracks) ou le TTML (Timed Text Markup Language)

- `label` : Titre la piste
- `src` : URL de la piste
- `srclang` : Langue de la piste
- `kind`: Le type de piste
	- `subtitles` : Sous titres (défaut)
	- `captions`: Retranscription textuel du contenu
	- `descriptions` : Texte converti en audio
	- `chapters` : Titre de chapitre
	- `metadata` : Métadonnées destinées à un script
- `default` : Attribut booléen. Permet de définir la piste par défaut

Remarque : Un élément média ne peut pas avoir plusieurs pistes partageant les mêmes valeurs pour les attributs `kind`, `srclang` et `label`

```html
<video controls poster="image.png">
	<source src="video.mp4" type="video/mp4">
	<source src="video.ogv" type="video/ogv">
	<track kind="captions" src="sampleCaptions.vtt" srclang="en">
	<track kind="descriptions"src="sampleDescriptions.vtt" srclang="en">
	<track kind="chapters" src="chapitres.vtt" srclang="en">
	<track kind="subtitles" src="soustitres_de.vtt" srclang="de">
	<track kind="subtitles" src="soustitres_en.vtt" srclang="en">
	<track kind="subtitles" src="soustitres_ja.vtt" srclang="ja">
	<track kind="subtitles" src="soustitres_oz.vtt" srclang="oz">
	<track kind="metadata" src="keyStage1.vtt" srclang="en" label="Key Stage 1">
	<track kind="metadata" src="keyStage2.vtt" srclang="en" label="Key Stage 2">
	<track kind="metadata" src="keyStage3.vtt" srclang="en" label="Key Stage 3">
</video>
```

### Autres

`<iframe>` : Élément remplacé. Permet d’intégrer au sein de la page un sous contexte de navigation. La page qui contient l’élément étant le contexte de navigation parent de cet élément. On peut indiquer à l’intérieur des balises un contenu alternatif qui s’affichera si le navigateur ne prend pas en charge l’élément.

- `src` : URL de la page à intégrer
- `name`: Nom de l’iframe. Ce nom peut être utilisé comme valeur de l’attribut `target` d’un élément `<a>` ou `<form>` ou comme valeur de l’attribut `formtarget` d’un élément `<input>` ou `<button>`
- `width` Largeur du conteneur en px (par défaut 300)
- `height` : Hauteur du conteneur en px
- `allow`: Permet de définir une règle de fonctionnalité
	- `fullscreen` : L’ iframe peut être mis en plein écran via la méthode JS `Element.requestFullscreen()` ( API Fullscreen)
	- `payment` : permet d’appeler l’API Payment Request
- `sandox`: Permet de placer l’iframe dans un bac à sable afin de limiter les interactions possibles. Utiliser cet attribut sans valeur permet d’appliquer toutes les restrictions. On peut également indiqué en valeur une liste de permissions séparées par des espaces
	- `allow-forms` : Autorise l’envoie de formulaires
	- `allow-scripts`: Autorise l’exécution de scripts
	- `allow-same-origin` : Le contenu est considéré comme étant de la même origine que le contexte parent. Cela permet d’ autoriser les requêtes AJAX, l’utilisation du localStorage, des cookies… (Remarque : Deux URLs ont la même origine s’ils utilisent le même protocole, le même hôte et le même port. )
	- `allow-modals` : Autorise l’ouverture des fenêtres modales.
	- `allow-popups`: Autorise l’ouverture de fenêtres popup.
	- `allow-orientation-lock` : Autorise la désactivation du verrouillage de l’orientation de l’écran.
	- `allow-top-navigation`: Autorise l’accès à la page parente.
	- `allow-pointer-lock`: AUutorise l’utilisation de l’API Pointer Lock
- `scrdoc` : Peut être utilisé à la place de l'attribut `src` pour indiquer le contenu exact de l'iframe. Généralement utilisé avec l'attribut `sandbox`. Si le navigateur ne prend pas en charge l'attribut, c'est l'attribut `src` qui sera pris en compte si il est présent.
- `referrerpolicy`

Attention : il est fortement déconseillé pour des raisons de sécurité d’activer en même temps les permissions `allow-scripts` et `allow-same-origin`

```html
<!-- iframe avec toutes les restrictions appliquées -->
<iframe sandbox src=”file”></iframe>

<!-- iframe avec permissions activées -->
<iframe sandbox=”allow-same-origin allow-forms allow-popups” src=”file”></iframe>
```

Remarque : L’option d’entête HTTP `X-Frame-Options` permet d’autoriser ou non l’intégration des pages dans un iframe. (à paramétrer sur le serveur Web)

`<object>` ; Élément remplacé. Ressource externe qui sera, selon son type, traité comme une image, un sous contexte de navigation ou un plugin. On peut indiquer à l’intérieur des balises un contenu alternatif qui s’affichera si le navigateur ne prend pas en charge l’élément.

- `data` : Obligatoire. URL de la ressource
- `type` : Obligatoire. Type MINE de la ressource
- `width` : Largeur du conteneur en px
- `height` : Hauteur du conteneur en px
- `form`: Associer l’élément à un formulaire. Indiquer comme valeur l’Id de l’élément `<form>`

```html
<object type="application/pdf" data="file.pdf" width="250" height="200">
	<p><a href="file.pdf">télécharger le fichier.</a></p>
</object>
```

`<param>` : Balise autofermante. Permet de définir des paramètres pour un élément `<objet>` ( A indiquer à l’intérieur de l’élément).

- `name`: Nom du paramètre
- `value` : Valeur du paramètre

`<embed>` : Balise autofermante. Contenu externe embarqué (plugin). Considéré comme obsolète.

- `src` : URL du contenu
- `type` : Type MINE du contenu
- `width` : Largeur du contenu en px
- `height` : hauteur en px
