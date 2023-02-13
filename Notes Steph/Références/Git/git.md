# Git

## Aide de git

- Aide générale : `git help`
- Liste des commandes git : `git help -a` (Taper `q` pour quitter)
- Afficher l'aide pour une commande :`git help <command>`

## Configuration

Remarque : La configuration se trouve de le fichier *.gitconfig* (qui se trouve dans le dossier utilisateur)

**Afficher les paramètres**

`git config --list`

**Définir son identité**

`git config --global user.mail "monmai@mail.com"`

`git config --global user.name "Prenom Nom"`

**Activer l'affichage des couleurs**

`git config --global color.diff auto`

`git config --global color.status auto`

`git config --global color.branch auto`

Remarque : Pour définir les paramètres pour un projet spécifique, il faut utiliser l'option `--local`

**Créer des alias pour les commandes**

Exemple :

```
git config --global alias.st status
git st
```

## Créer un dépôt local

`git init` (à lancer dans le dossier du projet)

cette commande permet également de réinitialiser un dépôt existant.

### État du dépôt

`git status`

- *untracked files* : nouveaux fichiers non suivis (affichage rouge) => à indexer avec `git add`
- *Changes not staged for commit* : fichiers suivis modifiés ou supprimés (affichage rouge) => à indexer avec `git add` ou` git rm`
- *Changes to be committed* : fichiers suivis et indexés (affichage vert) => à valider avec `git commit`

## Indexation

Indexer des fichiers qui ont été ajoutés ou modifiés : `git add <nom-fichier-1> <nom-fichier-2>` …

Si on indique un nom de dossier, tout ses fichiers seront ajoutés de manière récursive

Pour ajouter tout les fichiers en attente d'indexation : `git add .`

Indexer des fichiers qui ont été supprimés : `git rm <nom-fichier>`

Cette commande supprimera le fichier du dossier du travail si il est toujours présent. Si on souhaite conserver le fichier il faut utiliser l'option --cached

Pour désindexer un fichier : `git reset <nom-fichier>`

Remarque : Pour ignorer des fichiers de l'indexation il faut créé à la racine du dossier du projet un fichier *.gitignore*

### Effectuer un stash

Consiste à mettre de côté les informations modifiées et non encore commités

`git stash` : faire une remise des fichiers suivis.

- `-u` : prendre en compte également les fichiers non suivis. (C'est à dire les nouveaux fichiers qui n'ont pas encore été indexés avec git add )

`git stash list` : afficher la liste des stash

Pour récupérer une remise : `git stash pop <id-stash>` (Il faut être positionné dans la branche où on souhaite récupérer la remise)

Récupérer la dernière remise : `git stash pop`

Remarque : on aussi peut utiliser `git stash apply (<id-stash>)` qui fait la même chose sauf que la remise n'est pas supprimée après avoir été appliquée. Cela peut être utile si on a besoin d'appliquer une remise sur plusieurs branches.

Supprimer un stash : `git stash drop <id-stash>`

Supprimer tout les stash : `git stash clear`

Utilités des remises :

- Si on a fait des modifications sur la mauvaise branche et que l'on a pas encore fait de commit, il suffit de faire une remise et de la récupérer sur la bonne branche
- Si on travail sur une branche et que l'on doit en urgence faire des modifications sur une autre, on peut mettre son travail de côté sans avoir besoin de faire un commit

## Commit

Consiste à valider les modifications. La validation enregistre l’instantané qui a été préparé dans la zone d’index.

Pour effectuer un commit : `git commit -m "Description du commit"`

l'option -m permet d'entrer directement la description dans la ligne de commande. Sans cette option l'éditeur de texte par défaut sera lancé pour pouvoir entrer le message

Remarque : Les modifications qui n'ont pas été indexés ne feront pas parti du commit mais resteront dans le répertoire de travail

Options :

-` -a` : Pour indexer automatiquement toutes les modifications avant le commit (évite de faire un git add )

### Modifier le dernier commit

Si on a oublié un fichier, l'ajouter avec `git add` puis modifier le denier commit avec `git commit --amend`

Pour modifier uniquement le message du dernier commit : `git commit --amend -m "nouveau message"`

Remarque : La modification va remplacer complètement le commit (Ce dernier ne sera plus visible dans l'historique). Cela est utile pour faire des petites corrections (orthographe, oubli d'un fichier, etc…) sans encombrer inutilement l'historique.

### Historique des commit

`git log` : permet de lister tout les commit pour ordre chronologique décroissant avec pour infos :

- L' id du commit (somme de contrôle SHA-1)
- L'auteur
- La date du commit
- Le message du commit

`git log <nom-branche>` : pour avoir uniquement les logs d'une branche

Options :

- `--author <nom-auteur>` : Affiche les commit en fonction de l'auteur
- `-n <x>` : Pour afficher que x commit (ex : log -n 2 pour afficher que les deux derniers commits)
- `--pretty=oneline` : affiche les infos d'un commit sur une seule ligne

`git show <id-commit>` : Affichage détaillé des modifications du commit (équivalent à un diff)

`git show <nom-branche>` : détails du dernier commit de la branche

### Changer de commit

`git checkout <id-commit>` : Le pointeur spécial HEAD se déplace sur le commit indiqué par son id (l'id est affiché sur le prompt à la place du nom de la branche)

Le répertoire de travail est initialisé dans l'état du commit

Attention : On se retrouve dans un état de HEAD détaché. SI on souhaite conservé les modifications à partir de cette état il faut créer une nouvelle branche et basculer sur celle ci. Sinon on peut revenir sur le dernier commit d'une branche existante (dans ce cas les modifications seront perdus)

### Créer des tags

Permet d'indiquer un libellé à un commit. Il faut dans un premier temps se déplacer sur le commit concerné avec `git checkout <id-commit>` (Ne pas oublier de revenir à l'état normal)

Créer un tag : `git tag <nom-tag>`

Supprimer un tag : `git tag --delete <nom-tag>`

Options :

- `-m` : Indiquer un message descriptif du tag

Lister les tags : `git tag`

## Branches

Créer une branche : `git branch <nom-branche>`

Changer de branche : `git checkout <nom-branche>`

Créer une branche et se positionner dessus : `git checkout -b <nom-branche>`

Attention : le changement de branche modifie les fichiers du répertoire de travail (Ce dernier est réinitialisé dans l'état du dernier commit de la branche)

Lister les branches : `git branch` (l'étoile indique la branche dans laquelle on se situe).

- `-v` : afficher le dernier commit de chaque branche
- `--merged `: lister uniquement les branches qui ont été fusionnées avec la branche courante
- `--no-merged` : idem mais pour les branches non fusionnées

Pour fusionner une branche avec une autre : `git merge <nom-branche>` . Il faut être positionné dans la branche qui sera mise à jour (en général il s'agit de la branche main)

Supprimer une branche qui a été fusionnée : `git branch -d <nom-branche>` (Remarque : les branches qui ont été fusionnés dans une autre avec un merge ne sont plus utiles et peuvent donc être supprimées)

Supprimer une branche qui n'a pas été fusionnée : `git branch -D <nom-branche>` (Attention : on perd tout le travail réalisé sur cette branche)

Renommer une branche : `git branch --move old-name new-name`

## Dépôt distant

### Cloner un dépôt distant

`git clone <URL-DEPOT>`

Il est possible de renommer le dossier du dépôt en local : `git clone <URL-DEPOT> new-folder-name`

Deux protocoles de transfert peut être utilisés

- HTTPS
- SSH (*user@server:/path.git*)

### Relier un dépôt local à un dépôt distant vide

 `git remote add origin <URL-DEPOT>`

Remarque : *Origin* est le nom donné au pointeur vers le remote. ( On peut indiquer un autre nom si on le souhaite mais en général on garde ce nom car c'est celui qui est créé automatiquement lors d'un clone)

### Informations sur les remotes

remote = dépôt distant vers lequel pointe un dépôt local

Pour lister les remote d'uun dépôt local : `git remote -v`

deux deux types de remote

- fetch : sur lequel on récupère les informations
- push sur lequl on envoie les informations

=> En général on utilise le même remote pour le fetch et le push

Obtenir des informations détaillés sur le dépôt distant : `git remote show origin`

Remarque : *origin* est le nom par défaut du pointeur vers le remote

### Envoyer les informations

`git push` : Envoie les informations sur la branche principale du remote origin

`git push <nom-remote> <nom-branche>` : permet de préciser le nom du remote ou/et de la branche où envoyer les informations

Remarque : les informations sur les tags personnalisés ne sont pas envoyés par défaut. Il faut pour cela utiliser la commande `git push <nom-tag>` pour un tag particulier ou `git push --tags` pour tout les tags

autres options :

- `--all` : faire un push de toutes les branches  
-` --prune` : supprimer les branches distantes qui n'ont pas d'équivalent local.

### Récupérer les informations

`git fetch` : mis à jour des informations sur le remote (référence des pointeurs)

`git pull` : Récupéré les dernières modifications puis fait un merge avec dépôt local

### Autres commandes

renommer un remote : `git remote <old-name> <new-name>`

Supprimer un remote : `git remote rm <nom-remote>`

### Cas du conflit lors d'un push

Si il y a conflit avec les fichiers du dépôt distant le push est rejeté.

Dans ce cas il faut faire un `git pull` pour mettre à jour le dépôt local et ensuite corriger manuellement le conflit.

## Informations sur les fichiers

`git diff` : Compare les fichiers entre répertoire de travail avec le dernier commit

`git blame <nom-fichier`> : obtenir des informations sur les modifications effectuées sur un fichier

Chaque ligne de code indique l'id du dernier commit qui a modifié la ligne (si précédé par un ^ il s'agit du commit qui a créé le fichier), ainsi que l'auteur et la date de modification.

-` -L x,y` : afficher uniquement les lignes indiqués dans un intervalles (Ex: `git blame -L 10,20 file` pour afficher les lignes 10 à 20)
