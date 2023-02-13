# Microformats

Fonctionnalités permettant d'apporter plus de sémantique au langage HTML

Deux attributs HTML permet de rajouter des microformats :

- **rel** : Utilisé que pour des éléments **a** ou **link**. Il permet de préciser le type de relation entre deux ressources. Les microformats permettent d'ajouter des types de relation
- **class** : servant principalement à l'identification d'éléments pour leur appliquer un style CSS, il peut également être utilisé pour les microformats

Remarque : ces attributs peuvent prendre plusieurs valeurs qui seront séparées par des espaces

Exemple de Microformats

- **hCalendar** : pour les événements (basé sur iCalendar)
- **hCard** : pour les contacts (basé sur Vcard)
- **Geo** : pour les coordonnées géographiques (latitude, longitude)
- **hResume** : pour un CV ou un résumé
- **XFN** : pour indiquer les relations existantes entre des individus

=> ces microformats sont définis par des profils XMDP donc l'URI doit être rajouté dans le head
