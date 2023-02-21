# Archives

### **Archive tar**

`tar` : permet de rassembler plusieurs fichiers dans une seule archive

- `c` : créer l'archive
- `x` : extraire l'archive
- `f` : utiliser le fichier indiqué en paramètre
- `v` : mode verbose
- `z` : permet d'activer la compression gzip
- `j` : permet d'activer la compression bzip2
- `t` : afficher le contenu d'une archive sans l'extraire
- `r` : ajouter un fichier à une archive

Remarque : Bzip2 est moins utilisé que Gzip. Il compresse mieux mais il est plus lent.

Exemple :

- `tar cvf archive.tar fichier1 fichier2` : créer une archive à partir de plusieurs fichier
- `tar cvf archive.tar dossier/` : créer une archive à partir d'un dossier
- `tar xvf archive.tar` : extraire une archive
- `tar -tf archive.tar` : afficher le contenu d'une archive
- `tar -rvf archive.tar fichier` : ajouter le fichier à l'archive
- `tar czvf archive.tar.gz dossier/` : créer une archive compressée en gzip
- `tar xzvf archive.tar.gz` : décompresser et extraire une archive compressée en gzip
- `tar jcvf archive.tar.bz2 dossier/` : créer une archive compressée en bzip2
- `tar jxvf archive.tar.bz2` : décompresser et extraire une archive compressée en bzip2

### **Compression / décompression**

Gzip et Bzip2 ne permet pas d'assembler des fichiers avant la compression.

- `gzip fichier` : compresser un fichier en Gzip
- `gunzip fichier.gz` : décompresser un fichier compressé en Gzip
- `gunzip archive.tar.gz` : décompresser une archive compressée en Gzip
- `bzip2 fichier` : compresser un fichier en Bzip2
- `bunzip2 fichier.bz2` : décompresser un fichier compressé en Bzip2
- `bunzip2 archive.tar.bz2` : décompresser une archive compressée en Bzip2
- `zcat fichier.gz` : équivalent de la commande `cat` qui permet de lire un un fichier compressé en Gzip
- `zless fichier.gz` : équivalent de la commande `less` qui permet de lire un un fichier compressé en Gzip

### **Archive zip et rar**

Installer les programmes nécessaires :

`sudo apt-get install zip unzip unrar`

Pour créer une archive zip :

- `zip archive.zip fichier`
- `zip -r archive.zip dossier/`

Pour extraire un zip : `unzip archive.zip`

Pour voir le contenu d'un zip : `unzip -l tutoriels.zip`

Pour extraire un rar : `unrar e archive.rar`

Pour voir le contenu d'un rar : `unrar l archive.rar`
