# Utilisateurs, groupes et droits

### **Utilisateurs et groupes**

### **Description des utilisateurs et des groupes**

Chaque utilisateur appartient à un groupe principal et éventuellement à des groupes secondaires.

Le fichier `/etc/passwd` contient les informations de connexion de tous les utilisateurs. Chaque ligne correspond à un utilisateur et chaque éléments sont séparés par un double point. Les informations sont :

- Le login
- Le mot de passe. Le caractère `x` indique que le mot de passe est stocké de manière chiffré dans le fichier `/etc/shadow` (Visible que par l'utilisateur root)
- UID (User Identification) : Numéro unique identifiant un utilisateur
- GID (Groupe Identification) : Numéro unique identifiant un groupe
- Champ Gecos : informations sur l'utilisateur (Nom et prénom, adresse, commentaires, etc). Les élements sont séparés par une virgule.
- Le répertoire personnel de l'utilisateur
- Le chemin d'accès du shell utilisé

Exemple : `john:x:1939:1000:John Cleese:/home/john:/bin/bash`

Le fichier `/etc/group` contient les informations sur les groupes . Chaque ligne correspond à un groupe. Les informations sont : le nom du groupe, le numéro unique d’identification et la liste des utilisateurs qui appartiennent au groupe

La commande `id` (Pour Identity) permet d' obtenir des informations sur l'utilisateur courant ou sur celui indiqué en paramètre

### **Gestion des utilisateurs et des groupes**

### **Utilisateurs**

- `adduser [userName]` : Ajouter un utilisateur. Un groupe de même nom sera également créé.
- `passwd [userName]` : Modifier le mot de passe d'un utilisateur. Sans paramètre modifie le mot de passe de l'utilisateur sous lequel on est connecté.
- `deluser [UserName]` : Supprimer un utilisateur
	- `-remove-home` : option permettant de supprimer également le repertoire personnel de l'utilisateur

Attention : `adduser` et `deluser` sont des commandes qui n'existent que sous les distributions basées sur Debian/Ubuntu. Pour les autres distributions on doit utiliser `useradd` et `userdel`,  
qui sont les commandes Unix traditionnelles fonctionnant partout mais de manière plus basique.

- `usermod` : permet d'éditer un utilisateur
	- `l [newUserName]` : renomme l'utilisateur. Le nom de son répertoire personnel ne sera pas changé
	- `d [NewHomeDir]` : change le répertoire personnel de l'utiliateur.
	- `m` : Associer à l'option `d`. Permet de déplacer le contenu de l'ancien répertoire personnel vers le nouveau
	- `g [NewGroup]`: permet de changer le groupe de l'utilisateur
	- `G [group1] , [group2]…` : Ajouter l'utilisateur à un ou plusieurs groupes (nom séparé par une virgule) Attention : l'utilisateur sera enlevé des groupes auxquels il appartient déjà. Pour éviter cela utiliser en plus l'option `a`

	Exemple :

	`usermod -d /home/nouveauNom -m -l nouveauNom NomUtilisateur`

	`usermod -g nouveauGroupe NomUtilisateur`

	`usermod -aG NomGroupe1, NomGroupe2 NomUtilisateur`

### **Groupes**

- `addgroup [GroupName]` : Créer un nouveau groupe
- `delgroup [GroupName]` : Supprimer un groupe

Attention : `addgroup` et `delgroup` n'existent que sous Debian/Ubuntu. Les commandes traditionnelles fonctionnant partout sont `groupadd` et `groupdel`

### **Droits**

### **Type de public et de droits d'accès**

Publics :

- `u` : User (Propriétaire du fichier)
- `g` : Groups (Groupe propriétaire du fichier)
- `o` : Others (Tout les autres utilisateurs)
- `a` : All (tout le monde)

Droits d'accès :

- `r` : Read - L'utilisateur peut lire le fichier ou lister le contenu du répertoire
- `w` : Write - L'utilisateur peut modifier/supprimer le fichier ou le contenu du répertoire
- `x` : eXecutable - L'utilisateur peut exécuter le fichier ( s’il est exécutable) ou se positionner dans le répertoire

Exemple : `rwxr-xr--`

- Droits de lecture, écriture et exécution pour le propriétaire
- Droits de lecture et exécution pour le groupe
- Droits de lecture pour les autres

La commande `ls -l`permet de lister le contenu d'un répertoire en affichant les droits. Ces derniers sont précédé soit du symbole " d " pour indiquer un répertoire ou du symbole " - " pour indiquer un fichier.

### **Système de notation octale**

- `r` : 4
- `w` : 2
- `x` : 1

En additionnant les droits on obtient une valeur entre 0 (aucun droit) et 7 (tous les droits)

- `0` : Aucun droit
- `1` : droit d'exécution seulement
- `2` : droit d'écriture seulement
- `3` : droit d'exécution et d'écriture
- `4` : droit de lecture seulement
- `5` : droit de lecture et d'exécution
- `6` : droit de lecture et d'écriture
- `7` : tous les droits

Exemple : `rwxr-xr--` =>(4 +2+1) + (4+0+1) + (4+0+0) = 754

### **Modifier les droits d'accès**

Il faut être propriétaire du fichier et utiliser la commande `chmod` (CHange MODe)

### **Avec la notation littérale**

`chmod public opération droit fichier`

- `+` : Ajouter un droit
- `` : Supprimer un droit
- `=` : Affecter un droit

Quelques exemples

- `chmod o-r file.txt` : supprime le droit de lecture pour tous les autres utilisateurs
- `chmod go=rx file.txt` : affecte le droit de lecture et exécution pour le groupe et tous les autres utilisateurs
- `chmod g=u-x file.txt` : affecte au groupe les mêmes droits que ceux du propriétaire sauf le droit d’exécution
- `chmod u=rwx,og=r` : affecte tous les droits à l'utilisateur et seulement le droit de lecture pour les autres

### **Avec la notation octale**

Exemple

`chmod 777 file.txt` : Donne tous les droits pour tous les utilisateurs

### **Droits par défaut lors de la création d'un fichier**

- Fichier : `rw-r--r--` (644)
- Répertoire : `rwxr-xr-x` (755)

La commande `umask` (User MASK) permet de changer ces droits par défaut  
Elle prend en argument un masque constitué de 3 valeurs octales qui détermine les droits à effectuer par différence à :

- `666` : pour les fichiers
- `777` : pour les répertoires

Le masque par défaut est `022` ( car 666 - 022 = 644 pour les fichiers et 777 - 022 = 755 pour les répertoires)

Remarque : la commande `umask` n'est pas rétroactif et ne change donc pas les droits des fichiers précédemment créés

### **Changement de propriétaire et groupe**

- `chown [user] [file]` : CHange OWNer. Permet de changer le propriétaire d'un fichier. L'utilisateur est indiqué par son nom ou son UID. On peut également changer le groupe avec `chown [user:group] [file]`

	Exemple : `chown NomUtilisateur:NomGroup fichier.txt`

	- `R` : appliqué à un répertoire permet de changer le propriétaire de tous les fichiers qu'il contient de manière récursive
- `chgrp [group] [file]`: (CHange gRouP) permet de changer le groupe auquel appartient le fichier. Le groupe est indiqué par son nom ou GID.
