# Arborescence

### **Hiérarchie du système de fichier**

- `/` : racine du système
- `/bin` : exécutables des commandes essentielles disponibles pour tous les utilisateurs
- `/boot` : fichiers du chargeur d’amorçage et du noyau
- `/dev` : fichiers spéciaux des périphériques
- `/etc` : fichiers de configuration des programmes et services
- `/home` : répertoires personnels des utilisateurs
- `/lib` : bibliothèques système
- `/media` : points de montage pour les médias amovibles
- `/mnt` : points de montage pour les systèmes de fichiers temporaires
- `/opt` : emplacement pour des applications aditionnelles installées manuellement
- `/proc` : répertoire virtuel pour les informations système (états du noyau et des processus système)
- `/root` : répertoire personnel du super-utilisateur (Vide par défaut sous ubuntu.)
- `/run` : informations relatives au système depuis son dernier démarrage (ex : utilisateurs actifs, services en cours d'exécution, etc.)
- `/sbin` : exécutables système disponible pour root
- `/srv` : données pour les services du système
- `/tmp` : fichiers temporaires des applications
- `/usr` : hiérarchie secondaire pour les applications utilisateurs
	- `/usr/bin` : exécutables des applications disponibles pour tous les utilisateurs
	- `/usr/sbin` : exécutables des applications disponibles pour root
	- `/usr/lib` : bibliothèques partagées par les applications
	- `/usr/local` : emplacement des exécutables compilés par l'utilisateur
	- `/usr/share` : fichiers partagés par les applications (documentation…)
- `/var` : données variables diverses (logs, mail, sites web, base de données, …)

### **Chemin d'accès**

Type de chemin

- Chemin absolu : chemin partant de la racine et commençant par `/`
- Chemin relatif : relatif au répertoire courant

Symboles :

- `..` : Répertoire parent
- `.` : Répertoire courant
- `~`: Répertoire personnel de l'utilisateur courant
- `~nomDossier` : Pour désigner un autre répertoire personnel que celui de l'utilisateur courant

Exemple 1

Si le répertoire courant est `Documents` de l'utilisateur `alice`, alors les chemins suivants mènent tous au même fichier `monfichier.txt`

Chemin absolu :  
`/home/alice/Documents/monfichier.txt`

Chemin relatif :

- `monfichier.txt`
- `./monfichier.txt`
- `../Documents/monfichier.txt`
- `~/Documents/monfichier.txt`

Exemple 2

Si l'utilisateur courant est Alice

`~` désigne le répertoire personnel d' Alice : `/home/alice`

`~bob` désigne le répertoire personnel de Bob : `/home/bob`

### **Navigation**

- `pwd` : Print Working Directory - Affiche le répertoire courant
- `cd` : Change Directory - Changer de répertoire.  
Prend en argument un chemin absolu ou relatif. Sans argument amène vers le répertoire personnel de l'utilisateur courant
	- `cd ~` ou `cd` : accéder au répertoire de l'utilisateur courant
	- `cd ..` : remonter dans le répertoire parent
	- `cd -` : revenir au répertoire précédent
- `ls` : Liste les fichiers contenus dans le répertoire courant ou du répertoire indiqué en argument
	- `l` : affichage détaillé : Type de fichier (`` pour un fichier standard, `d` pour un repertoire, `l` pour un lien symbolique) droits, nombre de liens physiques, propriétaire, groupe, taille en octet, date de la dernière modification, nom du fichier + chemin d'accès du fichier d'origine si le fichier est un lien symbolique )

		Astuce : indiquer un nom de fichier en paramètre de `ls` avec l' option `l`permet d'avoir accès aux informations sur le fichier.

	- `a` : afficher les fichiers cachés
	- `F`: affiche un symbole à la fin du nom pour indiquer le type d'élément
		- `@` : Lien symbolique
		- `` : exécutable
		- `/` : répertoire
	- `h` : afficher la taille des fichiers de façon lisible ( en Ko, Mo, Go…)
	- `t` : trier par date de dernière modification
	- `s` : trier par taille décroissante
	- `r` : inversé l'ordre d'affichage
	- `i` : affiche les numéros d'inode (voir lien physique)

### **Modification**

- `mkdir [nomDossier]…` : MaKe DIRectory - Créer des répertoires
	- `p` : permet de créer une arborescence complète. Ex : `mkdir -p foo/bar/toto`
- `rmdir [nomDossier]…` : ReMove DIRectory - Supprimer des répertoires. Attention : le répertoire ne doit pas être vide.  
Sinon utiliser la commande `rm -r` à la place
- `touch [nomFichier]…` : Créer des fichiers textes vide. Si le fichier existe déjà, change la date de la dernière modification.
- `rm [nomFichier]…` : ReMove - Supprimer des fichiers et répertoires
	- `d` : supprimer des répertoires vides
	- `r` : supprimer l'arborescence contenu dans un répertoire
	- `f` : forcer la suppression sans confirmation
	- `i`: demander une confirmation
	- `v` : mode verbose
- `cp [cheminSource] [cheminDestination]` : CoPy - Copier des fichiers et répertoires.
	- `r` : Copier récursivement l'arborescence contenu dans un répertoire. Si le répertoire de destination existe le répertoire source et son contenu sera copié à intérieur. Sinon le répertoire destination sera créé et se sera uniquement le contenu du répertoire source qui sera copié à intérieur.
- `mv [cheminSource] [cheminDestination]` : MoVe - Déplacer des fichiers et répertoires. Permet également de renommer. On peut également utiliser l'option `r` pour les répertoires

### **Liens**

Deux types de liens :

- Physique : Permet d'avoir deux noms de fichier qui partagent le même contenu (=inode). Ne fonctionne pas sur les répertoires. Si on supprime un des fichiers l'autre fichier reste présent avec le contenu. L'inode est supprimé uniquement lorsque plus aucun nom de fichier ne pointe dessus
- Symbolique : permet de créer un lien qui pointe vers un autre nom de fichier (et non vers l'inode). Fonctionne également sur les répertoires. Si le fichier d'origine est supprimé le lien symbolique ne fonctionnera plus (lien cassé)

`ln [cheminSource] [cheminDestination]` : créer un lien physique

- `s` : créer un lien symbolique
