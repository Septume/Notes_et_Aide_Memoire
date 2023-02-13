# URL absolue vs relative

## Chemin relatif
-   `dossier/page.html` : La page est cherchée à partir de la page courante dans le sous-répertoire "dossier".
-   `./page.html` : La page est cherchée à partir du répertoire courant.
-   `../page.html` : La page est cherchée à partir du répertoire parent (on remonte d'un niveau)
-   `../../dossier/page.html` : ici on remonte de 2 niveaux
    
## Chemin absolu
`/dossier/page.html` : la page sera cherchée directement à partir de la racine du domaine => http://www.domaine.tld/dossier/page.html.

Le slash initial précise que l'on ne se réfère plus à l'emplacement courant mais que l'on remonte directement à la racine pour ensuite préciser le chemin complet.

Dans bien des cas, le chemin absolu est la convention d'écriture la plus sûre, mais aussi la moins souple si l'arborescence est amenée à changer.