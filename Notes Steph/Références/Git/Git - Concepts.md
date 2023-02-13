# Git - Concepts

Logiciel de gestion de versions (VCS = Version Control System)  décentralisé => Chaque copie locale du projet conserve l'histoire complet de tout les changements.

Effectue des instantanés de l’état du projet et enregistre une référence à cet instantané via une empreinte SHA-1

## Concepts de base

### Éléments

- `Working Directory` : Répertoire de travail. Contient les fichiers du projet. (Version courante)
- `Repository` : Base de données qui contient toutes les versions du projet (Se trouve dans le dossier caché *.git* à la racine du projet)
- `Stage` : Zone transitoire où sont stockés les informations de modifications pour le prochain instantané

### Étapes

1. Indexation => Ajout des modifications dans la zone index
2. Validation (commit)  =>  l'instantané est ajouté dans la base de donnée!

![[fonctionnement-git-1.png]]  
![[fonctionnement-git-2.png]]

### États des fichiers

- Fichiers en suivi de version : fichiers qui font parti du dernier instantané. Ils peuvent être dans l'état inchangés, modifiés ou indexés
- Fichiers non suivi : fichiers qui ne font pas parti du dernier instantanés et qui n'ont pas été indexés  

![[fonctionnement-git-3.png]]

### Branches et commit

#### Contenu d'un objet commit

- id unique de 40 caractères = SHA-1
- Les modifications enregistrées
- nom et mail de l'auteur , date et message
- Les SHA-1 des commit parents si existant

#### Notion de branche

Ensemble de commit relié entre eux par un pointeur (vers le parent)  
![[fonctionnement-git-4.png]]

### Notion de tags

= intitulé  d'un pointeur vers un commit

Toutes les branches possèdent un tag qui pointent vers le dernier commit (et donc qui se déplace au fur à et mesure qu'on ajoute des commits)

La branche principale a pour tag `main` (ou `master` pour les anciennes versions)  
On peut également créer ses propres tags et les associer à un commit

### Le HEAD

Pointeur spécial qui indique le dernier commit de la branche courante

![[fonctionnement-git-5.png]]  
Lorsqu'on récupère un commit avec la commande `git checkout <id-commit>` on se retrouve dans un état *detached HEAD* (Le HEAD ne pointent plus sur le même commit que le tag de la branche)  
![[fonctionnement-git-6.png]]  
Si on créé des commit à partir de cet état, le HEAD détaché pointe vers le dernier commit  
![[fonctionnement-git-7.png]]  
Lorsqu'on est dans un état de HEAD détaché et que l'on veut revenir à état normal il y a deux cas de figures:

- On ne souhaite pas conserver les modifications =>  On peut retourner sur une branche avec la commande `git checkout <nom-branche>`
- On souhaite conserver les modifications => On créé une nouvelle branche et on bascule sur celle-ci. (les commits effectués seront conservés)
	

Remarque : Le HEAD détaché est utile pour faire des modifications expérimentales

### Conflit de fusion

Les modifications qui n'ont pas pu être fusionnées à cause d'un conflit sont marquées `unmerged`

Git ajoute des marques de résolution dans les fichiers concernés afin de permettre la résolution manuelle

Exemple

```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
======
<div id="footer">
please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

  

`<<<<<<< HEAD` : version de la branche en cours

`>>>>>>> iss53` : version de la branche à fusionner (ici `iss53` )

`======` : séparateur entre les deux versions

### Dépôt distant

Cloner un dépôt = l'intégralité du dépôt est dupliqué en local![[fonctionnement-git-8.png]]  
Lors du clone git créé un pointeur vers le dépôt distant avec pour nom  `origin`

La branche principale du dépôt local possède donc deux tags :
- `main` (ou `master` ) : pointe le dernier commit sur le dépôt local
- `origin/main` : pointe le dernier commit sur le dépôt distant
