Installation : `npm install eslint --save-dev` 
Configuration : `npm init @eslint/config` 

Exemple de configuration

![[Pasted image 20221205092747.png]]

Les options sont enregistrés dans le fichier *.eslintrc.json* 

Puis indiquer dans le fichier *package.json* :

```
"scripts": {
  "lint": "eslint *.js"
}
```

Pour lancer le script : `npm run lint` 

Utilisation avec vs-code 
- Installer l'extension ESLint 
- Installer ESLint localement puis créer le fichier de configuration

Cette extension ajoute les commandes suivantes à la palette de commandes.
-   `Create '.eslintrc.json' file`: crée un nouveau `.eslintrc.json`fichier.
-   `Fix all auto-fixable problems`: applique les résolutions de correction automatique ESLint à tous les problèmes réparables.