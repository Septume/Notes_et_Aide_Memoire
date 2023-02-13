# Éléments textuels en ligne

### Liens

`<a>` : Lien. Il est possible de créer un lien sur des éléments de type bloc comme un titre, un paragraphe, etc.

- `href` : **Obligatoire**. URL de la cible absolue ou relative. On peut également indiquer une ancre ( dièse suivi d’une valeur correspondant à l’ id de l’élément qui constitue l’ancre). On peut indiquer une adresse dans un autre protocole que HTTP (FTP, mailto, etc.)
- `hreflang` : Code langue de la cible
- `download` : Attribut booléen. Indique que la cible doit être téléchargée. On peut également utiliser une valeur indiquant un nom de fichier différent pour l’enregistrement.
- `rel` : Relations avec la cible
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
- `target` : Contexte de navigation dans lequel le lien doit s’afficher
- `type` : Type MIME de la cible
- `referrerpolicy` : Politique concernant le referrer
- `ping` : Contient une liste d’URL séparées par des espaces vers lesquelles sont envoyées des requêtes `POST` avec le corps `PING` lorsque l’utilisateur suit le lien. Cet attribut est généralement utilisé pour tracer un utilisateur.

```html
<!-- Liens absolu vers un autre site -->
<a href="http://www.google.fr">Google</a>

<!-- Lien absolu vers une page située à la racine  -->
<a href="/mentions.html">Mentions légales</a>

<!-- Lien absolu vers la racine du site -->
<a href="/">Accueil du site</a>

<!-- Lien relatif vers une page située au même niveau d’arborescence - -->
<a href="contact.html">Contactez-nous</a>
<!-- Lien relatif vers une image située dans un sous répertoire (par rapport au document courant) -->
<a href="media/maphoto.jpg">Admirez ma photo</a>

<!-- Lien relatif vers une page située dans le répertoire parent (niveau au dessus du document courant) -->
<a href="../categorie.html">Revenir à la catégorie</a>

<!-- Lien relatif vers une page située deux niveaux au dessus -->
<a href="../../categorie.html">Revenir à la catégorie</a>

<!-- Lien pour adresse e-mail -->
<a href="mailto:moi@monsite.com">Contact</a>

<!-- Lien vers l'élément #contact -->
<a href="#contact">Accédez au formulaire de contact</a>
<div id="contact"> </div>

<!-- Lien vers l'élément #contact situé sur la page mentions.html-->
<a href="mentions.html#contact">Accédez au formulaire de contact</a>

<!-- Lien vers le haut de la page (on peut aussi utiliser #top) -->
<a href="#">Haut de page</a>

<!-- Lien de téléchargement -->
<a href="/images/batman_batmobile_007.png" download> Télécharger l'image de la batmobile </a>

<!-- Lien de téléchargement avec renommage  -->
<a href="/images/batman_batmobile_007.png" download="batmobile.png"> Télécharger l'image de la batmobile </a>

<!-- navigation avec relations -->
<nav>
	<a href="/" rel="index up up">Accueil</a>
	<a href="/categorie/" rel="up">Niveau supérieur</a>
</nav>
```

### Édition

`<ins>`: Pour indiquer une portion de texte qui a été ajouté. Par défaut le texte est affiché en souligné.

- `cite` : URL d’une ressource expliquant le changement
- `datetime` : Date du changement (voir `<time>` pour le format à utiliser)

`<del>` : pour indiquer une portion de texte qui a été supprimé (Mais que l’on souhaite conserver à l’affichage pour référence). Par défaut le texte est affiché en barré

- `cite`
- `datetime`

### Marqueurs

`<strong>` : Contenu de forte importance. ̈Par défaut le texte est affiché en gras.

`<em>` : Emphase. Contenu de moyenne importance. Par défaut le texte est affiché en italique.

`<mark>` : Contenu marqué en raison de sa pertinence dans un contexte particulier (Exemple : résultat d’une recherche, date sélectionnée). Par défaut le texte est surligné en jaune vif.

`<b>` : Mise en valeur du contenu mais sans lui donner une importance. Par ex: mot clés, nom de produits, introduction d’un article etc… Par défaut le texte est affiché en gras

`<i>` : Pour marquer un contenu qui se différencie du texte principal. Par exemple : termes techniques, phrases dans une langue étrangère, pensée, nom propre, etc…Par défaut le texte est affiché en italique

`<s>` : Pour marquer un contenu qui n’est plus d’actualité ou pertinent. Par défaut le texte est affiché en barré. Attention, cet élément ne doit pas être utilisé pour indiquer des suppressions de texte. A la place on utilise l’élément `del` (souvent associé à l’élément `ins`)

`<u>` : Pour marquer un contenu avec une annotation non textuelle dont le sens n’est pas précisé. Par défaut le texte est souligné. Par exemple : marqué un texte mal orthographié

`<dfn>` : Pour marquer un terme comme étant défini dans le document. La définition du terme doit être indiqué dans l’élément `p` ou `section` parent, ou par un groupe de liste de définitions (via les éléments `dt`et `dd`)

```html
<p><dfn>Firefox</dfn> est le navigateur créé et développé par la Fondation Mozilla.</p>
```

### Type de contenu

`<cite>` : Titre d’une œuvre mentionné dans le document

`<q>` : Citation courte

- `cite` : URL de la source

`<abbr>`: Description d’une abréviation, sigle ou acronyme. L’attribut `title` permet d’indiquer la description du terme qui sera affiché dans une infobulle au survol de la souris

`<code>` Code informatique. Par défaut le texte est affiché dans une police à chasse fixe. Pour représenter pusieurs lignes de code, on peut utiliser en parent l’élement `<pre>` qui permet de conserver les espaces blancs.

`<var>`: Variable dans une expression mathématique ou informatique. Ou pour indiquer un espace textuel que le lecteur peut mentalement remplacé par une autre valeur

`<samp>` : Sortie d’un programme informatique

`<kbd>` : Entrée au clavier (ou autre périphérique d’entrée comme une saisie vocale). Pour indiquer une saisie de plusieurs touches il faut imbriquer plusieurs éléments `<kbd`> dans un élement `<kbd>` représentant l’ensemble.

```html
<p>
Pour créer un nouveau document, utilisez le raccourci clavier<kbd><kbd>Ctrl</kbd> + <kbd>N</kbd></kbd>
</p>
```

`<time>` : Date, heure ou durée.

- `datetime` : Doit utiliser un format standardisé
	- `YYYY` : Année. Exemple : `2001`
	- `YYYY-MM` : Année et mois. Exemple : `2001-01`
	- `YYYY-MM-DD` : Date complète. Exemple : `2001-01-31`
	- `hh:mm:ss` : heure. Exemples : `12:57` - `12:57:30`
	- `YYYY-MM-DDThh:mm:ss` ou `YYYY-MM-DD hh:mm:ss` : heure et date (On utilise un espace ou un `T` comme séparateur). Exemples : `2000-12-25T12:57` - `2000-12-25` - `12:57`
	- `+hh:00` ou `hh:00`: Indication du décalage horaire. Exemples : `13:37+01:00` - `13:37:20-02:00`
	- `z` : fuseau horaire de référence. Exemple : `2000-12-25``13:37Z`
	- `P` : pour introduire une durée. Doit être suivi d’un nombre correspondant à la durée et un caractère indiquant une unité de temps.
		- `W` : semaine
		- `D` : jour
		- `H` : heure
		- `M` : minutes
		- `S` : seconde

		
		```html
        <time datetime="2012-02-11 23:26"> 11 février 2012 à 23 heures 26 </time>
        <time datetime="P30M">30 minutes</time>
        ```
		

`<small>` : Petits caractères d’imprimerie permettant d’indiquer une annotation. Par ex : mentions spécifiques ou légales, licences, avertissement discrets, etc…

### Autres

- `<sub>` : Pour mettre le texte en indice (en bas). À utiliser uniquement dans le cas d’une convention typographique (et non pour des effets de mise en forme)
- `<sup>` : Pour mettre le texte en exposant (en haut)
- `<br>` : Balise autofermante. pour indiquer un saut de ligne (retour chariot)
- `<wbr>` : (Word Break). Balise autofermante. Indique un endroit du texte où le navigateur doit faire un retour à la ligne si la longueur du texte dépasse l’espace réservé par son conteneur. Utile pour les URL et les mots longs. Correspond au caractère U+200B (espace de largeur nulle)
- `<span>` : Conteneur en ligne non sémantique pour l’application de style CSS ou autre.
- `<data>` : permet d'associer du contenu à une version de ce contenu pouvant être interprété par un programme informatique et que l'on indique via l'attribut `value`.

	
	```html
    <p>Nouveaux produits</p>
    <ul>
      <li><data value="3251546">Mini voiture</data></li>
      <li><data value="5867654">Grande voiture</data></li>
      <li><data value="9887635">Énorme voiture</data></li>
    </ul>
    ```
	

	Remarque : si le contenu à une composante temporelle, il faut utiliser `time` à la place
