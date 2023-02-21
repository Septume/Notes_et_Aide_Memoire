# Déploiement d'une app Angular sur FIrebase


## Installer Firebase CLI


```bash
npm install -g firebase-tools
```

Pour se connecter à son compte : `firebase login` 
Puis accepter l'autorisation dans la fenêtre du navigateur 


## Étapes déploiement

Générer la version prod de l'application : `ng build` 

initialiser Firebase : `firebase init` 
- Sélectionner la fonctionnalité *hosting*
- Sélectionner  un projet existant  ou créer un nouveau projet
- indiquer le dossier public : `dist/nom-projet` 
- Répondre aux autres questions :
  - Configurer une single-page app ?
  - Utiliser le déploiement automatique depuis Github ? 
  - Écraser le fichier index.html ?
=> créé un fichier de configuration `firebase.json` 

Déployer sur Firebase : `firebase deploy` 
Génère deux URLs : 
- Project Console => URL vers la page d'admin
- Hosting URL => URL du projet






















