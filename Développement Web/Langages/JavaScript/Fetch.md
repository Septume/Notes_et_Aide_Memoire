# API fetch
Permet de faire des requêtes HTTP avec un support natif des Promesses

On utilise la méthode `fetch()`  qui prend comme arguments :
- L'URL cible
- Facultatif : Les options de la requête sous forme d'objet
Par défaut (sans options) la requête est de type GET 

Une promesse `fetch()` est rejetée seulement si la requête n'a pas abouti à cause d'un problème réseau. Il faut donc en plus traiter les erreurs HTTP 

