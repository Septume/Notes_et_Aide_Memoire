# Taches planifiées

### **Retarder l'exécution d'une commande**

Commande `at` suivi de l'heure à laquelle exécuter la commande sous la forme `HH:MM` et éventuellement la date sous la forme `MM/JJ/AA` (format américain)

Exemple : `at 14:17 11/15/19`

Un invite s'affiche pour entrer les commandes qui devront être exécutées. Pour terminer utiliser `Ctrl + D`

`atq` : permet d'afficher la liste des tâches en attente

`atrm` : permet de supprimer une tâche en attente. Indiquer le numéro de la tâche en paramètre

### **Planificateur de tâches**

`crontab` : permet de lire et modifier le fichier `crontab` qui contient la liste des tâches qui seront régulièrement exécutées via la le programme `cron` . Chaque utilisateur, ainsi que root, possède sa propre crontab.

- `l` : Affiche le contenu du crontab
- `r` : supprime tout le contenu
- `e` : éditer le fichier crontab

Les champs du crontab :

- `m` : minutes (0-59)
- `h` : heures (0-23)
- `dom` : day of month - jour du mois (1-31)
- `mon` : month - mois (1-12)
- `dow` : day of week - jour de la semaine (0-6 , 0 étant le dimanche )
- `command` : la commande à exécuter

Notation :

- `` : indiquer n'importe quelle valeur
- `3,5,10` : indiquer plusieurs valeurs (ne pas mettre d'espace après la virgule)
- `3-7` : indiquer une intervalle.
- `/3` : indiquer un multiple (par exemple tout les 3 heures)

Exemple :

- `47 15 * * * commande :` toutes les jours à 15h47
- `47 * * * * commande`  
: toutes les heures à 47 minutes (00h47, 01h47, etc)
- `0 0 * * 1 commande`  
: tous les lundis à minuit
- `0 4 1 * * commande` : tous les premiers du mois à 04h00
- `0 4 * 12 * commande` : tous les jours du mois de décembre à 04h00
- `0 * 4 12 * commande` : toutes les heures les 4 décembre
- `* * * * commande` : toutes les minutes
- `30 5 1-15 * * commande` : à 05h30 du 1er au 15 de chaque mois
- `0 0 * * 1,3,4 commande` : à minuit le lundi, mercredi et jeudi
- `0 */2 * * * commande` : toutes les deux heures
- `/10 * * * 1-5 commande` : toutes les 10 minutes du lundi au vendredi

On peut également utiliser des raccourcis :

- `@reboot`
- `@yearly`
- `@annually`
- `@monthly`
- `@weekly`
- `@daily`
- `@midnight`
- `@hourly`

Il est possible de rediriger la sortie de la commande programmée

Ex : `15 * * * touch /home/bob/fichier.txt >> /home/bob/cron.log`
