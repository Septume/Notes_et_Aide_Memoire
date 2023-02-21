# Traitement de données

### **Afficher un fichier texte**

- `cat file.txt` : Affiche le contenu d'un fichier texte
	- `n` : Affiche les numéros de ligne
- `head file.txt` : Affiche par défaut les 10 première lignes
	- `n` : Affiche les x première lignes
	- `c` : Affiche les x premiers caractères
- `tail file.txt` : Affiche par défaut les 10 dernière lignes
	- `n` : Affiche les x dernières lignes
	- `c` : Affiche les x derniers caractères
	- `f` : permet de continuer à lire la fin du fichier si du nouveau contenu est ajouté. (utile pour suivre un fichier de log). La lecture se fait toutes les secondes. Il faut terminer la commande avec `CTRL + C`

### **Consulter et naviguer dans un fichier texte**

- `less file.txt` : Affiche le fichier page par page
	- `N` : affiche les numéros de ligne
	- `S` : affiche chaque ligne du fichier sur exactement une ligne de l’écran

Commandes interne de `less` :

- `Espace` : faire défiler le fichier d'un écran vers le bas
- `Entrée` : affiche la ligne suivante.
- `flèches haut/bas` : Monter/descendre d'une ligne. Précédé d'un nombre *n* : monter/descendre de *n* lignes
- `h` : Aide
- `q` : Quitter
- `b` : Défilement d'un écran vers le haut. Précédé d'un nombre *n* : monter de *n* écran
- `f` : Défilement d'un écran entier vers le bas. Précédé d'un nombre *n* : descendre de*n* écran
- `g` : Affiche le début du fichier. Précédé d'un nombre *n* : affiche le début après *n* lignes
- `G` : Affiche la fin du fichier
- `=` : indique où on se trouve dans le fichier (numéro de ligne et pourcentage).
- `/motif` : Recherche la première occurrence du motif entre la position courante et la fin du fichier. Précédé d'un nombre *n* : recherche la nième occurrence. La touche `n` permet de rechercher l'occurrence suivante et `N` permet de rechercher l'occurrence précédente
- `?motif` : Recherche la première occurrence du motif entre la position courante et le début. Précédé d'un nombre : recherche la nième occurrence
- `&motif` : Sélectionne et affiche les lignes contenant le motif

### **Filtrer les données**

`grep[motif][fichier]`: permet de faire une recherche de chaine de caractères dans un fichier texte et d'afficher les lignes correspondantes. On peut utiliser des expressions régulières

- `i`: ne pas tenir compte de la casse
- `n` : afficher les numéros de ligne
- `v`: inverser la recherche (les lignes ne correspondants pas au motif de recherche seront affichées)
- `r`: rechercher de manière récursive. Il faut indiquer un répertoire en deuxième paramètre

### **Autre traitements**

- `sort [fichier]` : permet de trier les lignes par ordre alphanumérique
	- `o`: écrire le résultat dans un fichier. (indiquer un nom de fichier en deuxième paramètre)
	- `r`: permet de trier en ordre inverse
	- `n` : permet de faire un tri numérique
- `wc [fichier]:` affiche le nombre de lignes , de mots et d'octets
	- `l` : compter le nombre de ligne
	- `w`: compter le nombre de mots
	- `o`: compter le nombre d'octets
	- `m`: compter le nombre de caractères
- `uniq [fichier]` : permet de supprimer des lignes en double. Il faut d'abord trier le fichier car seules les lignes successives sont traitées. On peut indiquer en deuxième paramètre un nom de fichier dans lequel enregistré les résultats
	- `c` : comme le nombre d'occurrences
	- `d` : affiche les lignes qui sont en doubles
- `cut [fichier]`: couper une partie du fichier. Attention : cette commande fonctionne mal avec les accents
	- `c` : couper selon le nombre de caractères. Par exemple si on souhaite conserver uniquement les caractères 2 à 5 de chaque ligne : `cut -c 2-5 fichier.txt`
	- `d` : couper selon un délimiteur. Doit être associé à l'option `f` qui permet d'indiquer les champs à extraire. Par exemple si on souhaite extraire le 1er et le 3ème champ et que le délimiteur est un `;` :

		`cut -d ; -f 1 3 notes.csv`
