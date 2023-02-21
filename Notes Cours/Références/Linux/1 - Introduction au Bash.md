# Introduction au bash

### **Prompt**

Format (pouvant varier selon la configuration) : `login@host:current-folder[$|#]`

- `$` : signifie qu'il s'agit de l'utilisateur courant
- `#` : Signifie qu'il s'agit de l'utilisateur root

### **Raccourcis clavier**

### **Déplacement**

- `CTRL + A` : Place le curseur en début de ligne (même effet que la touche `Origine`)
- `CTRL + E` : Place le curseur en fin de ligne (même effet que la touche `Fin`)
- `CTRL + B` : Recule d'un caractère (Backward)
- `CTRL + F` : Avance d'un caractère (Forward)
- `ALT + B` : Recule d'un mot
- `ALT + F` : Avance d'un mot

### **Couper/coller**

- `CTRL + K` : Coupe la chaine depuis la le curseur jusqu'à la fin de la ligne
- `CTRL + U` : Coupe la chaine depuis le début de la ligne jusqu'au caractère qui précède le curseur
- `CTRL + W` ou `ALT + gauche`: Coupe la chaîne depuis le caractère qui précède le curseur jusqu’au début ou du mot (si le curseur est placé à la fin d’un mot, coupe le mot)
- `ALT + D` : Coupe la chaîne depuis le caractère situé sous le curseur jusqu’à la fin du mot (si le curseur est placé au début d’un mot, coupe le mot)
- `CTRL + Y` : Colle la chaîne du presse papier juste avant la position du curseur

### **Modification**

- `CTRL + T` : Inverse la position des deux caractères situés avant le curseur
- `ALT + T` : Inverse la position des deux mots situés avant le curseur
- `ALT + C` : Met en majuscule la lettre située sous le curseur et déplace le curseur à la fin du mot (en plaçant le curseur au début d’un mot, met la première lettre en majuscule)
- `ALT + L` : Met en minuscule toutes les lettres depuis la position du curseur jusqu’à la fin du mot(en plaçant le curseur au début d’un mot, met le mot en minuscule)
- `ALT + U` : Mt en majuscule toutes les lettres depuis la position du curseur jusqu’à la fin du mot(en plaçant le curseur au début d’un mot, met le mot en majuscule)
- `CTRL + _` : Annule la dernière modification

### **Autres**

- `CTRL + R` : Faire une recherche dans l'historique. À l'invite saisir les termes de la recherches. Des appuis successifs sur CTRL + R permet de remonter dans l'historique
- `CTRL + G` : Abandonner la recherche
- `CTRL + L`: Effacer le contenu du terminal. Equivalent la commande `clear`
- `CTRL + C` : Stopper la commande en cours
- `CTRL + Z` : Mettre en pause la commande en cours
- `CTRL + D` : Quitter. Equivalent de la commande `exit`

### **Historique**

On peut naviguer dans la liste de l'historique des commandes avec les flèches du clavier.

### **Commande history**

`history`

- `c` : efface l'historique
- `w NomFichier` : sauve l'historique dans un fichier
- `r NomFichier` : ajoute les commandes enregistrer dans le ficher à l'historique courant
- `history n` : affiche les n dernières entrées de l'historique

### **Expansion de l'historique**

- `!!` : Permet de rappeler la dernière commande. Ex : `sudo !!`
- `!chaine` : rappelle la commande la plus récente qui commence par la chaîne. Pour ne pas que la commande soit exécutée, il faut ajouter `:p`en fin de ligne. Exemple : `!cd:p`
- `!?chaine?` : rappelle la commande la plus récente qui contient la chaine (ajouter `:p` pour ne pas exécuter la commande)
- `^ancien^nouveau^` : rappelle la derrière commande en changeant le motif ancien par nouveau

Exemple

```
 $ pvd
 bash: pvd: command not found
 $ ^v^w^
 pwd
```

On peut également réutiliser les arguments de la dernière commande dans une nouvelle

- `!!:*` ou la forme abrégée `!*`: tous les arguments
- `!!:^` ou la forme abrégée `!^` : premier argument
- `!!:$` ou la forme abrégée `!$` : dernier argument
- `!!:n` : l'argument de position *n*
- `!!:n-m` : les arguments de position *n* à *m*

On peut utiliser en plus ces opérateurs :

- `:s/ancien/nouveau/` : permet de faire une substitution
- `:r` :permet de supprimer le préfixe d'un nom de fichier

Exemple 1 (le "1" dans le nom de fichier est remplacé par un "2")

```
 $ wc fichier1.txt
 9 443 3024 fichier1.txt
 $ !!:s/1/2/
 wc fichier2.txt
 7 322 2155 fichier2.txt
```

Exemple 2

```
 $ tar xzf projet.tgz
 $ cd !!:$:r
 cd projet
```

### **Aide et documentation**

### **Aide d'une commande**

`h` ou `-help` : option pour obtenir l'aide d'une commande

### **Manuel**

Documentation sur les commande, fonctions, formats de fichiers …

`man [nomCommande]` : afficher le manuel de la commande. Remarque : utilise le programme `less` pour afficher le manuel

- `L fr` : option pour avoir la manuel en français

Sections du manuel :

1. commandes pour l’utilisateur
2. appels système (fonctions fournies par le noyau)
3. appels e bibliothèque (fonctions fournies pour le développement de programmes)
4. fichiers spéciaux (situés généralement dans /dev)
5. formats des fichiers et conventions. Par exemple `/etc/passwd`
6. jeux
7. Divers
8. commandes de gestion du système (généralement réservées au super utilisateur)
9. documentation du noyau.

Convention pour le synopsis (Résumé du format de la commande) :

- `texte gras` : à taper exactement comme indiqué
- `texte souligné` : à remplacer par l’argument approprié
- `[-abc]` : les arguments entre sont facultatifs
- `a|-b` : les options séparées par | ne peuvent pas être utilisées simultanément
- `argument…` : les trois petits points signifient que l’argument peut être répété
- `[expression]…` : les trois petits points signifient que toute l’expression située à l’intérieur de peut être répétée (en plus d’être facultative)

### **Autres commandes**

- `help [nomComande]` : aide sur les commandes internes au bash. Sans argument affiche la listes des commandes internes
- `apropos [expression]` : permet de faire une recherche dans les manuels via l'expression passée en argument
- `info` : outil permettant de naviguer en hypertexte dans la documentation des outils GNU
- `whatis [nomCommande]` : affiche l'entête d'une page de manuel (Section NAME)

### **Caractères spéciaux (wildcards)**

A utiliser en substitution dans les noms de fichiers

### **Caractères de base**

- `` : séquence de caractères
- `?` : Un seul caractère
- `[abc]` : un des caractères indiqués entre crochets
- `[a-c]` : un des caractères de l'intervalle indiqué entre crochet
- `[!…]` : aucun caractère de l'ensemble
- `[[:classe:]]` : une classe de caractères

Classes de caractères :

- `[:alnum:]` : Caractères alphabétiques et numériques (équivalent à : `A-Za-z0-9`)
- `[:alpha:]` : Lettres (équivalent à : `A-Za-z`)
- `[:lower:]` - Lettres minuscules (équivalent à : `a-z`)
- `[:upper:]` : Lettres majuscules (équivalent à : `A-Z`)
- `[:digit:]` : Chiffres (équivalent à : `0-9`)
- `[:blank:]` : Espace ou tabulation

Exemple

- `ls f*` : Liste tout les fichiers commençant par f
- `ls *` : Liste tout les fichiers du répertoire courant
- `ls /*`: Liste tout les dossiers situés à la racine
- `echo [aef]*` : Affiche tout les fichiers commençant par a, e ou f
- `echo [a-m]*`: Affiche tout les fichiers dont la première lettre est comprise entre a et m
- `echo [A-Z]*[0-9]`: Affiche tous les fichiers dont le nom commence par une majuscule et dont le dernier caractère est un chiffre
- `echo [!A-Z]*` : Affiche tous les fichiers qui ne commencent pas par une lettre majuscule
- `rm -rf *` : supprime sans confirmation et de manière récursive tous les fichiers du répertoire courant. **Attention : commande dangereuse !**

### **Option extglob (extended globbing)**

Pour activer cette option : `shopt -s extglob`

Permet d’utiliser des motifs étendus composés éventuellement d’une liste de sous-motifs, c’est-à-dire de motifs séparés par le caractère `|`

- `?(liste-de-motifs)`  
: le nom de fichier peut contenir 0 ou 1 fois un des sous-motifs de la liste
- `(liste-de-motifs)`  
: le nom de fichier peut contenir un nombre quelconque de fois (zéro compris) un des sous-motifs de la liste
- `+(liste-de-motifs)`  
: indique que le nom de fichier doit contenir au moins une fois un des sous-motifs de la liste
- `@(liste-de-motifs)`  
: indique que le nom de fichier doit contenir exactement un des sous-motifs de la liste
- `!(liste-de-motifs )`: indique que le nom de fichier ne doit contenir aucun des sous-motifs de la liste

Exemple :

- `echo X+(a|b)*+(a|b)` : afficher la liste des fichiers dont le nom commence par un `X` suivi d’au moins un caractère `a` ou `b` et se termine par un caractère `a` ou `b`
- `echo !(*aa)` : affiche la liste des fichiers dont le nom ne se termine pas par les deux caractères `a`

### **Substitution de commande**

Consiste à remplacer une commande par le résultat de l'exécution de cette commande. (Utile pour donner comme argument à une commande le résultat  
d’une autre commande)

`$(commande)`

Exemple :

`echo le répertoire courant est : $(pwd)`

Remarque : la commande `pwd` est exécutée avant la commande `echo`

### **Inhibitions**

Permet de contrôler l'interprétation des caractères spéciaux

inhibition totale : empêche toute interprétation. Utilisation de simple quote

Exemple

```
 $ echo $(pwd)
 /home/alice    
 $ echo '$(pwd)'
 $(pwd)
```

inhibition partielle : autorise les substitutions de variables et commandes ainsi que l'anti-slash `\` . Utilisation de double quote

inhibition de caractère spécial : utilisation de l'anti-slash `\`

Exemple

```
 $ echo Aujourd\’hui : $(date)
```

Exemple

Si le répertoire courant est `/home/alice` et qu'il ne contient que le fichier `f1.txt`

```
 $ i=*
 $ echo $i
 f1.txt
 $ echo "$i"
 *
 $ echo '$i'
 $i
 $ echo \$i
 $i
```

- `echo $i` revient à effectuer `echo *` . Le caractère `` est remplacé par les noms de fichiers du répertoire courant : `f1.txt`.
- `echo "$i"` a pour résultat `` car en cas de substitution partielle les caractères spéciaux pour les noms de fichiers ne sont pas interprétés
- `echo '$i'` a pour résultat `$i`. Car il n'y aucune substitution lorsqu'on utilise des simple quote
- `echo \$i` revient à effectuer `echo '$i'`car l'anti-slash empêche l'interprétation du caractère `$`

Cas des espaces  
:

Les espaces sont utilisées par le shell comme séparateur de mots. Lorsqu’elles sont utilisées à l’intérieur de quotes (simple ou double) elles ne sont plus interprétées mais prises littéralement. Ainsi le nombre d’espaces est conservé.

Exemple :

```
 $ echo ":  :"
 :  :
```

Les espaces peuvent également être inhibées avec l'anti-slash

Exemple :

```
 $ echo : \ :
 :   :
```

On peut également faire une inhibition de la fin de ligne

```
 $ a="une \
 > deux"
 $ echo $a
 une deux
```

L'effet des simples quotes est annulé à l'intérieur de double quote et vice versa (Ils sont interprétés comme des simples caractères)  
De même que l'effet de l'anti-slash est annulé à intérieur de quote, simple ou double

Exemple

```
 $ banniere="$(uname) says to $(whoami) : \"hello don't stop\"" 
 $ echo $banniere
 Linux says to alice : "hello don't stop"    
```

Ordre de substitution :

1. substitution de variable
2. substitution de commande
3. substitution de noms de fichier

La commande `eval` permet de relancer la phase d’interprétation du shell.  
Le résultat de la première interprétation sert à constituer la ligne de commande pour la seconde interprétation. C’est le résultat de cette interprétation qui sera exécuté.

Exemple

```
 $ var1=test
 $ var2=var1
 $ echo $var2
 var1
 $ echo \$$var2
 $var1
 $ eval echo \$$var2
 test
```

### **Enchainements de commandes**

On peut lancer plusieurs commande sur la même ligne en les séparant par un `;`

Exemple : `uname -a; whoami`

### **Redirections et pipe**

### **Les entrées/sorties**

- `stdin` : entrée standard (par défaut : le clavier)
- `stdout` : sortie standard (par défaut : l'écran)
- `stderr` : sortie d'erreurs (par défaut : l'écran)

### **Redirection des sorties**

- `commande > fichier`: écrit la sortie standard de la commande dans un nouveau fichier. Attention : Si le fichier existe déjà il sera écrasé sans demande de confirmation.
- `commande >> fichier`: ajoute la sortie standard de la commande à la fin du fichier (le fichier sera créé si il n'existe pas)
- `commande 2> fichier` : écrit la sortie d'erreur dans le fichier
- `commande 2>> fichier` : ajoute la sortie d'erreur à la fin du fichier

Exemple : `ls > liste.txt`

On peut également rediriger la sortie vers nulle part avec `> /dev/null`

### **Fusionner les sorties**

- `2>&1` : redirige la sortie erreur vers la sortie standard
- `1>&2` : redirige la sortie standard vers la sortie erreur

Exemple :

`echo "ERROR" 1>&2`

`cut -d , -f 1 file.csv >> file.txt 2>&1`

### **Redirection de l'entrée**

`commande < fichier` : redirige le contenu du fichier vers l'entrée de la commande

Exemple : `wc -l <log.txt`

### **Chainer les commandes (pipe)**

`commande1 | commande2 :` Consiste à connecter la sortie d'une commande à l'entrée d'une autre commande

Exemple :

`du | sort -nr | less`
