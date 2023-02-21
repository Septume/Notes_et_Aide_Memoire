# NPM
Node Package Manager => Gestionnaire de paquets (Livré avec NodeJS)

## Gestion des paquets

`npm install <package-name>` ou `npm i <package-name>`  : Installe le paquet localement (au niveau du projet)

options : 
- `--save` : indiquer que le paquet est une dépendance du projet. cette option est maintenant obsolète car incluse par défaut de manière implicite lors d'une installation locale
- `--save-dev` : le paquet est utilisé uniquement pour la phase de développement (*devDepencies*)
- ` -g` : Installe le paquet globalement (au niveau du système)


`npm uninstall <package-name>` : désinstalle le paquet 

 `npm init` : Créer un fichier *package.json* 
`npm install` :  installer les dépendances d'un projet (indiqués dans le fichier *package.json*) 

## Gestion des dépendances 

```json
"dependencies": {
    "express": "^4.18.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.19"
  }
```

Convention pour les numéros de version => Utilisation de 3 nombres séparés par des points. Représente dans l'ordre : 
- version majeure (ajout de fonctionnalités  qui ne sont pas compatibles avec les versions précédentes). Une version "0" est en général une version alpha ou beta. 
- version mineure (ajout de fonctionnalités compatibles avec les versions précédentes) 
- correctifs

Préfixe :
- `^` : autoriser les correctifs et les versions mineures (par défaut)
- `~` : autoriser uniquement les correctifs lors de la mise à jour des paquets 
- aucun : ne pas mettre à jour

## Utilisation des scripts

Indiquer dans le fichier *package.json* la commande à utiliser pour exécuter un script  
pour lancer le script : `npm run <command-name>

<u>Exemple</u>

```json
"scripts": {
	"start": "nodemon app.js"
},
```

Exécuter le script : `npm run start` 











