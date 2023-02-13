# Formulaires

### Créer un formulaire

`<form>` : Pour construire un formulaire. Doit contenir tout les autres éléments du formulaire.

- `action` : URL de la page qui va traiter les informations.  
la valeur peut être surchargée par l'attribut `formaction` des éléments `button` et `input`
- `rel` : Type de relations
	- `help`
	- `license`
	- `next` et `prev`
	- `search`
	- `external`
	- `nofollow`
	- `noopener`
	- `noreferrer`
- `method` : méthode HTTP d’envoie des données.
	- `get` : Méthode GET (Défaut)
	- `post` : Méthode POST
	- `dialog` : A utiliser quand le formulaire est placé dans un élément `dialog`. Permet de fermer la boite de dialogue à l'envoi du formulaire

	la valeur peut être surchargée par l'attribut `formmethod` des éléments `button` et `input`

- `name` : Nom du formulaire
- `target` : Contexte de navigation dans lequel s’affiche la réponse du serveur. La valeur peut être surchargée par l'attribut `formtarget` des éléments `button` et `input`
- `autocomplete`: Autoriser l’autocomplétion des champs du formulaire par le navigateur. Les valeurs possible sont `on` (défaut) et `off`. Les éléments du formulaire peuvent outrepasser cette valeur avec leur propre attribut `autocomplete`
- `enctype` : Dans le cas de la méthode POST, permet de définir le type MIME de l’encodage des données envoyées au serveur.
	- `application/x-www-form-urlencoded` : Valeur par défaut.
	- `multipart/form-data` : A utiliser pour un `<input>` de type `file` (envoie de fichier)
	- `text/plain`

	la valeur peut être surchargée par l'attribut `formenctype` des éléments `button` et `input`

- `novalidate` : Attribut booléen. Désactive la validation automatique du formulaire par le navigateur.  
la valeur peut être surchargée par l'attribut `formvalidate` des éléments `button` et `input`

### Champs et contrôles de formulaire

`<input />` : Champs et contrôles de formulaire

- `type` : Type de données
	- `text` : Texte normal (Défaut)
	- `password` : Mot de passe
	- `email` : Adresse mail. Le validateur automatique du navigateur vérifie que la valeur saisie correspond bien à un format d’adresse mail valide.
	- `url` : Lien. Le validateur automatique du navigateur vérifie que la valeur saisie correspond bien à un format d’URL valide.
	- `tel` : Numéro de téléphone.
	- `number` : Nombre. La valeur est vérifiée par le validateur automatique
	- `range` : Curseur. On peut indiquer un nombre comme valeur par défaut. La valeur est vérifiée par le validateur automatique.
	- `color` Couleur. On peut indiquer une valeur par défaut en indiquant un code couleur hexadécimal. (Par défaut : `#000000` ). La valeur est vérifiée par le validateur automatique. Le contrôle utilise le sélecteur de couleur natif du système d’exploitation.
	- `date` : Date. On peut indiquer une valeur par défaut sous la forme AAAA-MM-JJ. La valeur est vérifiée par le validateur automatique.
	- `time` : Heure
	- `datetime-local`: Date et heure
	- `month`: Mois et année
	- `week` : Numéro de semaine et année
	- `search` : Champ de recherche. La plupart des navigateurs affiche une croix dans le champ permettant d’ effacer la saisie et proposent une autocomplétion des termes déjà saisies.
	- `file` : Fichiers à envoyer.
	- `checkbox` : Case à cocher
	- `radio` : Bouton radio
	- `submit` : Bouton d’envoi.
	- `image` : Bouton d’envoi sous forme d’image (URL à indiquer avec l’attribut `src` )
	- `reset` : Bouton de remise à zéro
	- `button` : Bouton générique. À utiliser conjointement avec du JavaScript pour programmer des actions.
	- `hidden` : Contrôle non affiché mais dont la valeur est envoyée au serveur. Cet élément ne peut pas recevoir le focus et les évènements DOM `input` et `change` ne s’appliquent pas.

Attributs communs à l’ensemble des types de champ :

- `name` : Nom de l’élément. Permet de recueillir la valeur du champ après validation du formulaire.
	- champ de type `radio` : Les options qui ont le même nom appartiennent au même groupe. (Une seule option par groupe est sélectionnable)
	- champ de type `hidden`: Si l’attribut `name` utilise la valeur spéciale `_charset_`, la valeur du champ envoyée avec le formulaire sera l’encodage utilisé pour l’envoi du formulaire.
- `value` : Valeur par défaut de l’élément.
	- champ de type `radio` ou `checkbox` : La valeur sera envoyée au serveur uniquement si l’élément a été sélectionné/coché par l’utilisateur au moment de l’envoi du formulaire. Si la valeur n’a pas été définie par le developpeur, c’est la chaine de caractères `on` qui sera envoyée. Pour tout éléments non sélectionnés par l’utilisateur, aucune valeur n’est transmise.
	- champs de type `submit`, `reset` et `button` : La valeur permet d’indiquer un texte à afficher sur le bouton.
	- champ de type `image` : Ce type n’accepte pas de valeur pour l’attribut `value`
- `autofocus` : Attribut booléen. Le champ sera automatiquement sélectionné au chargement de la page. Un seul élément peut avoir cet attribut. Ne fonctionne pas sur les champs de type `hidden`.
- `disabled` : Attribut booléen. Le champ est désactivé (aucune interaction possible)
- `readonly` : Attribut booléen. Le champ ne peut pas être modifié.
- `required`: Attribut booléen. Le champ est obligatoire.
- `autocomplete` (Surcharge la valeur de l’attribut `autocomplete` du formulaire)
- `form` : Permet d’associer le champ à un formulaire. La valeur doit correspondre à celle de l’id du formulaire. Si l’attribut est absent le champ est rattaché au formulaire le plus proche. Un champ ne peut être associé qu’à un seul formulaire. Cet attribut est utile si on souhaite placer le champ n’importe où dans la page.
- `list` : Permet d’associer au champ une liste `[<datalist>](about:blank#datalist)` . La valeur doit être l’id de la liste associée. Cet attribut n’est pas pris en charge pour les champs de type `hidden`, `password`, `checkbox`, `radio` et `file` ou pour les boutons.

Attributs pour les champs de type `text`, `password`, `email`, `url`, `tel`, `search`

- `minlength` : Nombre min de caractères autorisés
- `maxlength` : Nombre max de caractères autorisés
- `placeholder` : Permet d’afficher dans le champ une texte court servant d’indication.
- `size` : Nombre de caractères affichés à l’écran, ce qui permet de définir la largeur du champ. La valeur par défaut est `20`
- `pattern` : Expression rationnelle à laquelle le texte saisie doit correspondre pour être valide. Le format à utiliser pour le motif est le même que pour le JavaScript (Ne pas mettre de barre oblique autour du motif). Si le format n’est pas valide, l’attribut sera ignoré.

```html
<!-- Le champ demande un texte en minuscules entre 4 et 8 caractères. -->
<input type="text" name="username" placeholder="votre nom d'utilisateur" size="45" minlength="4" maxlength="8" pattern="[a-z]{4,8}" required>
```

Attribut complémentaire pour le champ de type `email`:

- `multiple` : Attribut booléen. Indique si plusieurs adresses peut ête saisies (séparées par des virgules)

Attributs pour les champs de type `checkbox` et `radio`

- `checked` : Attribut booléen. Indique l’élément qui est coché/sélectionné par défaut

Attributs pour les champs de type `number` , `range`, `date`, `datetime-local`, `time`, `month` et `week`

- `min` : Valeur ou date min acceptée
- `max` : Valeur ou date max acceptée
- `step` : Le pas à utiliser pour incrémenter la valeur.

Attributs pour le champ de type `file`:

- `accept` : Les types de fichiers acceptées. Indiquer les identifiants de type de fichiers séparés par des virgules. La forme de l’identifiant peut être :
- une extension de fichier (ex : `.jpg`)
	- un type MIME
	- La chaine `audio/*` pour indiquer n’importe quel fichier audio
	- La chaine `video/*` pour indiquer n’importe quel fichier vidéo
	- La chaine `image/*` pour indiquer n’importe quel fichier image
- `multiple` : Attribut booléen. Indique si plusieurs fichiers peuvent être envoyés (L’utilisateur peut sélectionner plusieurs fichiers avec la touche `CTRL` ou `MAJ`)

```html
<!-- fichiers images ou PDF -->
<input type="file" accept="image/*,.pdf">

<!--fichiers Word -->
<input type="file" accept=".doc,.docx,application/msword">
```

Attributs pour les champs de type `submit` et `image`

- `formaction` : URL de la page qui va traiter les informations. Surcharge pour ce champ la valeur de l’attribut `action` de l’élément `<form>`. Permet d'avoir deux boutons d'envoi dans le formulaire qui fonctionnent séparément.
- `formenctype` : Type MIME de l’encodage des données envoyées au serveur. Surchage pour ce champ la valeur de l’attribut `enctype` de l’élément `<form>`
- `formmethod` : Méthode HTTP d’envoie des données. Surchage pour ce champ la valeur de l’attribut `method` de l’élément `<form>`
- `formnovalidate` : Attribut booléen. Désactive la validation automatique du navigateur. Surchage pour ce champ la valeur de l’attribut `novalidate` de l’élément `<form>`
- `formtarget` : Contexte de navigation dans lequel s’affiche la réponse du serveur. Surchage pour ce champ la valeur de l’attribut `target` de l’élément `<form>`

Attributs complémentaires pour le champ de type `image`

- `src`
- `alt`
- `heigth`
- `width`

```html
<input type="image" width="100" height="30"src="login.png" alt="Login">
```

### Autres éléments de formulaires

`<button>` : Affiche un bouton. Nouveau élément destiné à remplacer les `input` de type `submit`, `reset`, `button`. Le texte du bouton est à indiquer entre la balise ouvrante et fermante (on peut également indiquer une image)

- `type` : Type du bouton. Si non indiqué le type par défaut est `submit`
	- `submit` : Bouton d’envoi du formulaire
	- `reset` : Bouton de réinitialisation
	- `button` : Bouton générique pour programmer des actions en JS.
- `name`
- `value`
- `autofocus`
- `disabled`
- `form`
- `formaction`
- `formenctype`
- `formethod`
- `formnovalidate`
- `formtarget`

```html
<button name="button" onclick="alert('Vous avez cliqué !')">Cliquez moi ! </button>
```

`<textarea>` : Zone de texte multiligne. On peut indiquer le texte à afficher par défaut entre la balise ouvrante et fermante.

- `rows`: Nombre de ligne de la zone de texte
- `cols` : Nombre de colonnes (largeur moyenne des caractères) de la zone de texte (Par défaut : 20)
- `wrap` : Gestion du retour à la ligne automatique
	- `hard` : Le navigateur insère automatiquement des sauts de ligne lorque celle-ci dépasse la largeur de la zone de texte. L’attribut `cols` doit être défini.
	- `soft`: Valeur par défaut. Le navigateur n’insère pas automatiquement des sauts de ligne
- `maxlength` : Nombre max de caractères autorisés
- `minlength` : Nombre min de caractères autorisés
- `name`
- `autocomplete`
- `autofocus`
- `disabled`
- `required`
- `readonly`
- `placeholder`
- `form`

Remarque : Sur la plupart des navigateurs, on peut redimensionner un élément `<textarea>` en glissant le coin inférieur droit. Pour désactiver cette fonctionnalité on utilise la propriété css `resize` avec la valeur `none`

`<select>` : Pour créer une liste déroulante. Chaque élément de la liste est indiqué avec la balise `<option>`

- `multiple` : Attribut booléen. Indique qu’il est possible de sélectionner plusieurs options.
- `size`: Indique le nombre de ligne visible à l’écran.
- `name`
- `autocomplete`
- `autofocus`
- `disabled`
- `required`
- `form`

`<option>` : Permet d’indiquer les options d’une liste déroulante

- `value`: Valeur qui sera envoyée au serveur si l’option a été sélectionné par l’utilisateur. Si non définie c’est le contenu textuel de la balise qui sera envoyée.
- `selected` : Attribut booléen indiquant l’option sélectionné par défaut.
- `label` : Texte affiché dans la liste. Si non défini c’est le contenu textuel de la balise qui sera affiché
- `disabled` : Désactive la sélection de l’option

`<optgroup>` : Permet de regrouper les options d’une liste déroulante `<select>`

- `label` : Affiche un nom pour le groupe (non sélectionnable)
- `disabled`: Attribut booléen. Aucun élément du groupe ne peut être sélectionné

```html
<select>
	<optgroup label="Europe">
		<option value="fr">France</option>
		<option value="ch">Suisse</option>
	</optgroup>
	<optgroup label="Amerique">
		<option value="us">Etats Unis</option>
		<option value="ca">Canada</option>
	</optgroup>
	<optgroup label="Asie" disabled>
		<option>Chine</option>
		<option>Japon</option>
	</optgroup>
</select>
```

`<datalist>` : Associé à un élément `<input>`. Pemet d’afficher une liste de valeurs à suggérer à l’utilisateur pour ce champ. (La liste de suggestions apparait lors de la frappe en autocomplétion) Chaque valeur est indiquée dans un élément `<option>`Les valeurs qui ne sont pas compatible avec le type de champs ne seront pas affichées dans les suggestions.

```html
<input list="browsers">
<datalist id="browsers">
	<option value="Chrome">
	<option value="Firefox">
	<option value="Internet Explorer">
	<option value="Opera">
	<option value="Safari">
</datalist>
```

`<output>` : Conteneur permettant d’afficher le résultat d’un calcul ou d’une action utilisateur.

- `for`: la liste des id (séparés par des espaces) des éléments qui ont joué un rôle dans le calcul.
- `name`
- `form`

`<progress>` : Permet d’indiquer la progression d’une tâche au cours du temps (Affiché sous la forme d’une barre de progession)

- `value`: Valeur indiquant l’état actuel de la progesssion. . Doit être un nombre décimal compris entre `0` et `max`. Si la valeur est absente la progression est dans un état indéterminé.
- `max` : Valeur maximum (nombre décimal positif). La valeur par défaut est `1`

`<meter>` : Représente une mesure comprise dans une intervalle. Les valeurs négatives et les nombres décimaux peuvent être utilisés. Son usage est principalement destiné à indiquer un état stable ou évoluant au cours du temps.

- `value` : Obligatoire. Valeur courante (entre `min` et `max`)
- `min`: Limite minimale de l’intervalle
- `max` : Limite maximale de l’intervalle
- `low`: Valeur à partir de laquelle la mesure est considérer comme basse
- `high` : Valeur à partir de laquelle la mesure est considérer comme haute
- `optimum`: Valeur idéale pour la mesure

### Organisation du formulaire

`<label>` : Permet d’associer un libellé à un élément de formulaire `input` (sauf ceux permettant de créer des boutons), `select` ou `textarea`. Un clic sur le libellé donne le focus à l’élément correspondant. L’élément `<label>` peut être indiqué en tant que frère de l’élément associé (il est séparé de l’élément) ou en tant que parent (il encadre l’élément)

- `for` : Doit contenir la même valeur que celle de l’attribut `id` de l’élément qui est associé.

```html
<label for="pseudo">Votre pseudo :</label>
<input id="pseudo" type="text">
```

```html
<label for="pseudo">Votre pseudo : <input id="pseudo" type="text"> </label>
```

`<fieldset>` : Permet de grouper des éléments du formulaire. Peut contenir un élément `<legend>` pour indiquer une légende

- `disabled`: tout les élements appartenant au groupe sont désactivés
- `form`
- `name`

`<legend>` : Légende pour un groupe `fieldset` . Accepte des éléments enfants

```html
<fieldset>
	<legend>Vos informations personnelles</legend>
	<label id="nom">
		Votre nom <input id="nom" name="nom" type="text">
	</label>
	<label id="mail">
		Votre mail <input id="mail" name="mail" type="email">
	</label>
</fieldset>

<fieldset disabled>
	<legend>Inscription à la newsletter</legend>
	<label id="oui"> 
		oui <input id="oui" name="newsletter" type="radio">
	</label>
	<label id="non">
		non <input id="non" name="newsletter" type="radio">
	</label>
</fieldset>
```
