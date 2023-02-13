# Rechercher des fichiers

### **Recherche rapide**

`locate [motif]` : Effectue une recherche de fichier à partir d'une base de donnée.

Pour mettre à jour la base : `sudo updatedb` (Remarque : la base est mise à jour automatiquement toutes les 24 h)

### **Recherche approfondie**

`find` : permet à la fois de faire une recherche de fichiers et d'effectuer des opérations sur les fichiers trouvés.

Options :

- `name` : Recherche d'un fichier par son nom
- `iname` : Même chose que `name` mais insensible à la casse
- `size`: Recherche en fonction de la taille
- `type` : Recherche en fonction du type de fichiers
	- `d` : répertoires
	- `f` : fichiers
- `atime` : Recherche en fonction de la date de dernier accès
- `mtime` : Recherche en fonction de la date de dernière modification
- `user` : Recherche de fichiers appartenant à l'utilisateur donné
- `group` : Recherche de fichiers appartenant au groupe donné
- Actions :
	- `exec` : Exécute la commande donnée aux fichiers trouvé.

		Doit être sous la forme : `exec commande {} \;`

		Les accolades `{}` seront remplacées par le nom du fichier trouvé

		La commande ne doit pas être entre guillemets

	- `ok` : Même chose que `exec` mais demande une confirmation
	- `ls` : exécute la commande ls à chaque fichier trouvé
	- `printf` : affichage avec un format personnalisé
	- `delete` : supprimer les fichiers trouvés (attention pas de confirmation)
- Opérateurs :
	- `a` : Opérateur ET
	- `o` : Opérateur OU
	- `!` ou `not` : Opérateur NOT

Exemple de commande simple :

- `find -name "logo.png"` : recherche le fichier `logo.png` à partir du répertoire courant (sous répertoires compris)
- `find /var/log/ -name "*log"` : recherche à partir du répertoire `/var/log` tout les fichiers donc le nom se termine par `log`
- `find -size +10M` : recherche les fichiers qui font plus de 10 Mo (on peut également utiliser le signe `` pour rechercher, par exemple, les fichiers qui font moins de 10 Mo)
- `find -name "*.odt" -atime 6` : recherche des fichiers `.odt`modifiés depuis 7 jours (remarque : la numération commence à zéro)
- `find /var/log -name "syslog" -type d` : recherche des répertoire ayant pour nom `syslog`

Exemple de commande avancée avec manipulation des résultats :

- `find -name "*.jpg" -printf "%p - %u\n"`: rechercher les fichiers `.jpg` et afficher chaque résultat avec le nom du fichier, un tiret, le nom du propriétaire et un retour à la ligne
- `find -name "*.jpg" -exec chmod 600 {} \;` : rechercher les fichiers `.jpg` et et appliquer un chmod 600
