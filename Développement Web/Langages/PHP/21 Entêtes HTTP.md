# Entêtes http

Pour manipuler les entête HTTP on utilise la fonction `header()`. Arguments :

- chaine à envoyer comme entête HTTP
- (facultatif) : f`alse` pour indiquer qu’il faut ajouter une nouvelle entête au lieu de la remplacer
- (facultatif) : code réponse HTTP (entier)

Attention : la fonction doit être appelée avant tout code PHP ou HTML et sans espaces avant

L’ instruction header permet la redirection URL automatique : `header('Location: page.php')`
