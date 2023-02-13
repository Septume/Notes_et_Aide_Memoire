# Processus

### **Code retour**

Lorsqu'un processus se termine un code retour est envoyé au processus parent.

Pour afficher le code retour de la dernière commande :

`echo $?`

Par convention si le code de retour n'est pas `0` cela indique une erreur dans l'exécution de la commande

### **Attributs d'un processus**

- `PID (Process ID)` : identifiant du processus
- `PPID (Parent PID)` : identifiant du processus parent
- `UID (User ID)` : identifiant de l’utilisateur qui a lancé le processus.
- `TTY` : terminal à partir duquel a été crée le processus.
- `TIME` : durée d'exécution du processus
- `STIME` : heure de l'exécution du processus
- `CMD` : la commande qui a créé le processus

### **Lister les processus**

`ps` (processes snapshot) : Affichage statique des processus. Par défaut affiche seulement les processus de l'utilisateur courant

- `u` : affiche l'utilisateur des processus
- `a` : Affiche les processus de tout les utilisateurs
- `x` : affiche les processus sans terminal
- `f` : affichage en arbre

On peut utiliser `grep` pour limiter la liste.  
Ex : `ps aux | grep apache`

`top` : Affichage en temps réel des processus. Par défaut, les processus sont triés par taux d'utilisation du processeur (colonne `%CPU`). Les commandes internes sont :

- `f` : ajouter ou supprimer des colonnes dans la liste
- `u` : filtrer en fonction d'un utilisateur
- `k`: stopper un processus (le PID du processus sera demandé)
- `s` : change l'intervalle de temps entre chaque rafraîchissement de la liste (par défaut : toutes les trois secondes)
- `M` : classer en fonction de l'occupation de la mémoire.
- `P` : classe en fonction de l'occupation du CPU.

### **Arrêter un processus**

- `kill [PID]` : Arrêter le processus normalement
- `kill -9 [PID]` : Arrêter le processus brutalement. Attention : il y a un risque de perte de données non enregistrées
- `killall[commande]` : Arrêter l'ensemble des processus lié à une commande

### **Processus en arrière plan**

### **Lancer un processus en arrière plan**

On utilise le symbole `&`à la fin de la commande.

Exemple : `sleep 3600 &`

Le terminal renvoie un numéro de tâche d'exécution qui est indiqué entre crochet suivi du PID du processus. A noter que la commande peut continuer à envoyer des messages dans le terminal. Pour éviter cela il faut penser à faire une redirection de ces messages.

### **Gestion des processus en arrière plan**

- `jobs` : commande qui permet d' afficher les processus exécutés en arrière plan
- `bg` : Envoyer le processus en cours d' exécution en arrière plan. Il faut d'abord le mettre en pause avec le raccourci `CTRL + Z` pour pouvoir récupérer l'invite de commande.
- `fg %n`: ramener un processus en premier plan en indiquant son numéro de tâche. Exemple : `fg %2`

### **Détacher le processus de la console**

`nohup`: permet de lancer un processus qui reste actif même après la déconnexion de l'utilisateur qui l'a lancé. A combiner avec `&` pour que le processus soit en arrière plan. Par défaut la sortie de la commande est redirigée vers un fichier`nohup.out`.
