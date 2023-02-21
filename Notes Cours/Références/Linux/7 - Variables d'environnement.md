# Variables d'environnement

Variables accessibles à l'ensemble des processus du système.

Pour afficher la liste : `printenv`

Pour afficher la valeur d'une variable :

- `printenv nomVariable` . Ex : `printenv LANG`
- `echo $nomVariable`. Ex: `echo $LANG`

Les principales variables d'environnement :

- `HOME`
- `PWD`
- `OLDPWD` (chemin absolu vers le courant précédent)
- `PATH` (répertoires des exécutables accessibles en ligne de commande)
- `LANG`
- `EDITOR` (chemin d'accès de l'éditeur de texte par défaut. Ex : `usr/bin/nano`)
- `SHELL`

3 types de scopes :

- le scope session : variables accessibles que pendant la session (la variable est accessible que pour le shell courant et ses processus enfants. Elle est détruite à la fermeture de la session)
- le scope utilisateur : variables propres à un utilisateur (Les processus lancés par un autre utilisateur n'auront pas accès à ces variables)
- le scope global : variables accessibles à tout les utilisateurs

Créer une variable d'environnement :

`export NOM_VARIABLE = valeur`

- Pour la session : Exporter la variable dans la console
- Pour tout les utilisateurs : Exporter la variable dans le fichier `/etc/profile`
- Pour l'utilisateur courant : Exporter la variable dans le fichier `~/.profile` (surcharge la configuration du profil global).
