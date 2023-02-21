# WSL

[Voir documentation](https://docs.microsoft.com/fr-fr/windows/wsl/)  
Sous-système Windows pour Linux  

WSL permet de :

- Exécuter les applications Windows (par exemple : notepad.exe) à partir de Linux (Ligne de commande WSL)
- Exécuter les applications Linux  (par exemple : `grep`) à partir de Windows (Ligne de commande CMD ou PowerShell)
- Partager des variables d’environnement entre Linux et Windows. (Build win10 17063+)

## Installation

`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

## Mise à jour vers WSL 2

WSL2 peut être utilisé en parallèle de WSL 1  

Avantages

- Meilleures performances du système de fichiers Linux (accès plus rapide aux fichiers locaux)
- Noyau Linux complet  et compatibilité complète des appels système => Permet d' exécuter plus de services et des apps comme Docker  

Inconvénients

- L'accès au système de fichier Windows est plus lent. (car utilisation d'une machine virtuelle)  
Prérequis :
- Version de Win10 1903 ou supérieure, avec Build 18362 ou supérieure
- La virtualisation est activée dans le BIOS

Activer la fonctionnalité Plateforme de machine virtuelle : `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

Télécharger la mise à jour vers WSL2 : [Package de mise à jour du noyau Linux WSL2 pour machines x64](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

Définir WSL2 comme version par défaut  lors de l’installation de nouvelles distributions Linux : `wsl --set-default-version 2`

## Installation et configuration des distributions Linux

- Télécharger la distribution depuis le Microsoft Store
- Lancer le logiciel pour terminer l'installation et créer un compte utilisateur et mot de passe

Pour voir les commandes propres à une distribution : `<nom-distribution> /?.`

Afficher la liste des distributions : `wsl --list --verbose`

Changer la distribution par défaut : `wsl -s <nom-distribution>`

Changer la version WSL pour une distribution :  
`wsl --set-version <nom-distribution> <numero-version-WSL>`  
Exemple : `wsl --set-version ubuntu 2`

Pour désinstaller une distribution (supprime toutes les données) : `wsl --unregister <nom-distribution>`

Importer/exporter une distribution : `wsl --exportwsl --import`  
Remarque : les services de sauvegarde classiques qui sauvegardent les fichiers de Appdata (comme la sauvegarde Windows) n’endommageront pas les fichiers Linux.

## Utilisation

### Exécuter WSL

via la terminal :  `bash` ou `wsl` => Ouvre une session de la distribution par défaut dans le répertoire utilisateur de Windows  

Via l'explorateur Windows
- *MAJ + clic droit* -> *Ouvrir l'interpréteur de commandes Linux ici*
- Entrer `bash` ou `wsl` dans la barre d'adresse pour lancer le shell dans le dossier courant  

Autres commandes WSL
- `wsl -h` : obtenir l'aide
- `wsl -d <nom-distribution>` : Lancer une distribution spécifique  
Il est également possible de lancer directement des commandes bash dans le répertoire courant avec la commande `wsl`  
Exemple :  
- `wsl date`  
- `wsl sudo apt-get update`

### Accéder au fichiers Windows depuis Linux

Le disque C est automatiquement monté dans le répertoire : */mnt/c*  
Tous les fichiers du système Windows appartiennent à l'utilisateur courant avec toutes les permissions (777)

### Accéder aux fichiers Linux depuis Windows

**Attention : il faut la mise à jour 1903 ou supérieure**  

Lancer l'explorateur Windows depuis WSL (affiche le répertoire home) : `explorer.exe .`  

Il est possible de faire des opérations (copier, supprimer, etc.) ou utiliser le menu contextuel pour ouvrir le fichier avec une application Windows.  

Via PowerShell  : `cd \\wsl$\<nom-distribution>\`  

Attention : Il ne faut jamais tenter d'accéder aux fichiers Linux via le dossier AppData (risque de corruption des fichiers)

### Utilisation d'Ubuntu

La commande `ubuntu` permet d'ouvrir une session dans le répertoire utilisateur d'Ubuntu plutôt que celui de Windows  

Mettre en français  
```
sudo apt-get update  
sudo apt-get install language-pack-fr language-pack-fr-base manpages-fr manpages-fr-extra  
sudo update-locale LANG=fr_FR.UTF8
```

## Extension Remote-WSL pour Visual Studio Code

Permet d'exécuter VS Code dans WSL (pour éditer les fichiers Linux)  
[https://docs.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-vscode](https://docs.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-vscode)  

L'extension ajoute plusieurs commandes à VS Code. Pour les afficher :
- Palette de commande =>  Taper *Remote-WSL*
- Via le bouton dans le coin inférieur gauche de la barre d'état => indique le contexte dans lequel VS code se trouve (local ou distant)  

Exécuter VS Code dans WSL  : `code .`

## Autres

- [Configurer NodeJS sur WSL 2](https://docs.microsoft.com/fr-fr/windows/nodejs/setup-on-wsl2)
- [Prise en main des bases de données sur WSL](https://docs.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-database) (MySQL, MongoDB, etc…)
