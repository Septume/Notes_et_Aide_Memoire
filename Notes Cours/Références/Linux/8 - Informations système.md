# Informations système

### **Général**

- `uptime` : uptime du système, le nombre d'utilisateurs connectés et la charge CPU moyenne
- `uname` : informations sur le noyau
	- `s` : nom du noyau.
	- `n` : nom de la machine
	- `r` : révision du noyau
	- `v` : version du noyau
	- `m` : type de processeur de la machine (i386, i686, etc.)
	- `o` : nom du système d'exploitation
	- `a` : Affiche toutes les informations

### **Date**

`date` : affiche la date en cours

- `r` : affiche la date de modification du fichier donné en paramètre

Pour personnaliser l'affichage de la date on utilise le signe `+` suivi des caractères spéciaux correspondant au format souhaité :

Format :

- `%H` : heure (sur 24h)
- `%M` : minute
- `%S` : secondes
- `%d` : jour du mois
- `%m` : mois
- `%Y` : année (sur 4 chiffres)
- `%x` : représentation de la date conforme aux paramètres régionaux (`%d/%m/%Y`)
- `%X` : représentation de l'heure conforme aux paramètres régionaux (`%H:%M:%S`)

### **Utilisateurs**

- `who` : informations sur les utilisateurs connectés (nom, terminal utilisé et heure de connexion)
- `w` : informations détaillés sur les utilisateurs connectés
	- `USER` : nom de l'utilisateur
	- `TTY` : nom de la console utilisée
	- `FROM` : adresse IP ou nom d'hôte de l'utilisateur
	- `LOGIN@` : heure de connexion
	- `IDLE` : depuis combien de temps l'utilisateur est inactif
	- `WHAT` : la commande en cours d'exécution
- `whoami` : affiche le nom de l'utilisateur courant
- `id` : informations sur l'utilisateur courant ou sur celui indiqué en paramètre

### **Mémoire**

`free` : affiche la mémoire disponible / utilisée du système

- `b` : Affiche la mémoire en octets (bytes)
- `k` : Affiche la mémoire en kilooctets
- `m` : Affiche la mémoire en mégaoctets
- `g` : Affiche la mémoire en gigaoctets
- `h` : Affiche la mémoire en unités pertinentes pour l'humain
- `s` : Spécifie le délai de réaffichage (en secondes)
- `t` : Affiche en plus la ligne des totaux (RAM + swap)

Exemples :

`free -m -s 5` : Affiche la mémoire du système en mégaoctets toutes les 5 secondes

### **Espace disque**

`du` : Affiche l' espace disque utilisé par les fichiers et/ou les répertoires

- `a` : Afficher pour tous les fichiers et pas uniquement les répertoires
- `s` : Afficher le total sans lister les différents fichiers
- `c` : Faire un total après avoir tout affiché.
- `h` : Ajoute un suffixe correspondant à l'unité (K, M, G)

Exemple d'utilisation :

- `du -sh /home/user` : taille totale du répertoire utilisateur
- `du -ach /home/user`: taille des fichiers et répertoires contenus dans le répertoire utilisateur + taille totale
