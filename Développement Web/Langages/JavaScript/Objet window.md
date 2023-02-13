# Objet window

Objet représentant la fenêtre ou l'onglet du navigateur.

L'objet `window` étant implicite, il n'est pas nécessaire de le spécifier lors des appels de méthodes.  
Par exemple, on peut écrire `alert()` plutôt que `window.alert()`

Les variables globales du script sont des propriétés de `window` , on peut donc y accéder avec `window.nomVariable`

## **Méthodes**

`alert()` : boite d'alerte. Affiche la chaine de caractères indiquée en paramètre

`prompt()` : boite de saisie. Renvoie une chaine de caractère (qui peut être vide si absence de saisie). Le bouton Annuler renvoie la valeur `null`. Peut prendre en paramètre une chaine de caractères qui sera affichée à l'écran.

`confirm()` : boite de confirmation. le bouton Ok renvoie `true` et le bouton Annuler renvoie `false`

## **Propriétés**

`innerWidth` et `innerHeight` : Largeur et hauteur du viewport

`outerWidth` et `outerHeight` : Largeur et hauteur de la fenêtre (en prenant en compte les éléments d'interface)

## Sous-objets

`document` : Représente le document HTML (DOM)

`location` : Réprésente l'URL de la page courante

- `location.href` : URL complète de la page
- `location.host` : Domaine de la page et numéro de port
- `location.hostname` : Domaine de la page
- `location.port`
- `location.pathname` : Chemin relatif de la page par rapport à l'hôte
- `location.protocol` : Protocole (*http* ou *https)*
- `location.search` : Paramètres (chaine commençant par `?`)
- `location.hash` : Fragment (chaine commençant par `#`)
- `location.origin` : Origine de l'URL

`navigator` : Information sur la navigateur

- `navigator.userAgent`
- `navigator.language`
- `navigator.geolocalisation` : Retourne un objet Geolocation

`Screen` : Réprente l'écran de l'appareil de l'utilisateur

- `screen.width` : largeur totale l'écran en pixels
- `screen.height` : hauteur totale de l'écran en px
- `screen.availWidth` : Largeur disponible de l'écran en px
- `screen.availHeight` : Hauteur disponible de l'écran en px
- `screen.orientation` : Orientation de l'écran

`history` : Navigation dans l'historique du navigateur

- `history.back()` : Retourne en arrière dans l'historique. Permet de simuler le bouton précédent du navigateur
- `history.forward()` : Avance dans l'historique. Permet de simuler le bouton suivant du navigateur
- `history.go(nb)` : Avancer du nombre de page indiqué en argument. On peut mettre une valeur négative pour reculer.

Remarque : Pour des raisons de confidentalité il n'est pas possible d'avoir accès aux informations de l'historique de navigation
