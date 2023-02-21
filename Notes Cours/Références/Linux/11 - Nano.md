# Nano

### **Raccourcis clavier**

`^` : touche `CTRL`

`M`: touche `ALT`

- `CTRL + G` : afficher l'aide
- `CTRL + K` : couper la ligne de texte (et la mettre dans le presse-papier)
- `CTRL + U` : coller la ligne de texte
- `CTRL + C` : afficher à quel endroit du fichier le curseur est positionné (numéro de ligne…)
- `CTRL + Y` : page précédente
- `CTRL + V` : page suivante
- `CTRL + W` : rechercher dans le fichier (`Ctrl + C` pour annuler). Faire à nouveau`Ctrl + W`pour  
rechercher la prochaine occurrence (La recherche précédente est sauvegardée et  
apparaît entre crochets)
- `CTRL + O` : enregistrer le fichier
- `CTRL + X` : quitter Nano
- `ALT + 6` : copier (Faire la combinaison `ALT MAJ -`)
- `ALT + A` : marquer. Permet de faire une sélection du texte à partir de la position du curseur. Refaire `ALT+A` pour enlever la marque.

### **Paramètres de la commande nano**

- `l` : affiche les numéros de ligne
- `c` : affiche la position du curseur
- `m` : autorise l'utilisation de la souris sous Nano
- `i`: indentation automatique

### **Configurer nano**

Créer dans le répertoire personnel le fichier `.nanorc` à partir du fichier de configuration global `/etc/nanorc` :

`cp /etc/nanorc ~/.nanorc`

- `set mouse` : activer la souris
- `set autoindent`  
: activer indentation automatique
