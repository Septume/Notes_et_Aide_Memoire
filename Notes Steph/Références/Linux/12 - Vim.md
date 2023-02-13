# Vim

Deux modes :

- mode commande (par défaut)
- mode insertion pour la saisie de texte

### **Commandes de base**

- `:h` : Aide
- `:q` : Quitter
- `:w` : Enregistrer
- `:wq` : Enregistrer et quitter
- `:q!` : Quitter sans enregistrer  
:
- `set number` : Afficher les numéros de ligne

### **Commandes de navigation**

Les commandes de navigation dans le fichier sont similaires à celles de `less`. Certaines peuvent être  
préfixées par un nombre pour être répétées.

- `0` : Placer le curseur en début de ligne
- `$` : Placer le curseur en fin de ligne
- `w` : Placer le curseur sur le mot suivant. (Peut être préfixée par un nombre).
- `b` : Placer le curseur sur mot précédent. (Peut être préfixée par un nombre).
- `G` : Placer le curseur à la fin du fichier
- `CTRL + f` : Placer le curseur sur la page suivante (forward)
- `CTRL + b` : Placer le curseur sur la page précédente (backward)
- `/motif` : Rechercher et placer le curseur sur la première (ou Nième) occurrence du motif entre la position courante et la fin du fichier.
- `?motif` : Rechercher et placer le curseur sur la première (ou Nième) occurrence du motif entre la position courante et le début du fichier

### **Mode insertion**

- `i` : Insérer des caractères avant le curseur. Echap pour quitter
- `a` : Insérer des caractères après le curseur. Echap pour quitter
- `c w` : Insérer des caractères à la place du mot courant. Peut être préfixée par le nombre de mots à supprimer.
- `r (caractère)` : Remplace le caractère situé à la position du curseur par le caractère indiqué

### **Suppression de texte**

Remarque : le texte supprimée est copié dans le presse papier

- x : Supprimer un caractère (Peut être préfixée par un nombre)
- d w : Pour supprimer un mot. (Peut être préfixée par un nombre)
- d [N] : Pour supprimer N lignes à partir de la ligne courante. Si on indique pas de valeur N, une seule ligne est supprimée

### **Copier-coller**

- `y w` : Copier un mot
- `y [N] y` : Copier N lignes à partir de la ligne courante. Si on n'indique pas de valeur de N, une seule ligne sera copiée
- `p` : Copier du contenu du presse papier à la position du curseur
