**<9 - Collaborer à la gestion d’un projet informatique et à l’organisation de l’environnement de développement/>

Nous avons réalisé ce projet avec un camarade de promotion, Mr Adrien Gouacide. Nous nous sommes aidés mutuellement même si dans un optique de productivité et de formation à un travail équipe, j’ai décidé de m’occuper exclusivement du Back-end avec Node.js et Adrien du Front-end avec React. Le but étant de se mettre dans les conditions d’une entreprise étant dépendant du travail et des besoins de l’autre équipe et de se perfectionner à l’utilisation de GitHub (commit, branch, merge, etc…). 

Nous avons utilisé la méthode Agile dans notre projet, se fixant des objectifs chaque semaine et utilisant l’outil de gestion Trello pour organiser notre travail.  


**<10 - Concevoir une application/>

Nous avons mis en place un cahier des charges répondant à plusieurs problématiques:

Premièrement, répondre à ce qu’est l’application, ses fonctionnalités et quelle est la problématique que l’application est sensé résoudre.

Ensuite, énumérer tous les points que nous voulions voir validé pour la version final.

En troisième point, nous avons décortiqué chaque étape de son développement et en accord avec la méthode agile et concevoir les attentes pour le MVP (Minimum Viable Poduct) ainsi que pour la Version 1, puis 2, jusqu’à la version finale spécifier dans le cahier des charges.

Afin de nous organiser, nous avons mis en place un todo avec l'application "Trello" afin de 
- sectoriser les taches, 
- savoir qui était charger de les réaliser, 
- la date d’échéance fixer,
- le travaille "à faire", "en cours" et "terminer".
![[Capture d’écran du 2023-02-28 12-15-13.png]]

**<11 - Développer des composants métier/>

Nous avons réaliser un diagramme d'utilisation afin de nous imager  les cas possibles et les différents "acteurs" qui agirons sur l'application. AU vu de notre travail en méthode agile, les diagrammes et les différents cas de développement de l'application étaient vouer à évoluer et être modifier au fil de l'avancer du projet.
![[Pasted image 20230228111252.png]]


Voici-ci dessous les trois functions qui font le cœur de l'application et du générateur dynamique de recettes de craft.
![[Capture d’écran du 2023-02-28 14-53-41.png]]

![[Capture d’écran du 2023-02-28 14-54-28.png]]

![[Capture d’écran du 2023-02-28 14-54-59.png]]

**<12 - Construire une application organisée en couches/>

Dans notre architecture 3-tier, nous avons en premier lieux la présentation (Le Client), qui ci-dessous créer une route disons "login" qui est surligner. Qui envoi une request 'post' à l'URL "/api/user/login"
![[Capture d’écran du 2023-02-28 13-56-43.png]]
![[Capture d’écran du 2023-02-28 14-06-09.png]]

![[Capture d’écran du 2023-02-28 14-00-18.png]]
*exportation du .environement*

La request est récupérer par le traitement (Serveur d'applications).
![[Capture d’écran du 2023-02-28 14-01-35.png]]

Et s'assurer de la véracité des données, avant de les renvoyer au "userController".
![[Capture d’écran du 2023-02-28 14-20-36.png]]

Toujours dans le Serveur d'Application, la fonction va récupérer les données et vérifier si l'email est conforme et qu'il n'est pas déjà utiliser par quelqu'un d'autre en sollicitant la Base de Donnée (ligne 240 ci-dessous).
Comparer le Mot de Passe entre celui envoyer avec la request et celui dans la BDD en utilisant le .compare de Bcrypt.
Créer un Token avec JSONwebToken pour s’authentifier dans ses prochaines requests.
![[Capture d’écran du 2023-02-28 14-09-01.png]]
Puis effectuer une request vers la Base de Donnée (Serveur Base de Données) lui demandant de modifier dans la table la dernière connection.
Et enfin retourner le token qui a été créer précédemment. 

**<13 - Développer une application mobile/>

Nous avons décidé d’utiliser Capacitor sachant que nous ne voulions pas re-créer une application avec React Native, Flutter ou Ionic. 
Nous avons donc suivis la documentation à la lettre, qui est très bien fournie, nous demandant d'installer plusieurs modules.

Une fois les fonctionnalités mobiles de Capacitor installer, nous avons utilisé l’environnement de développement Android Studio pour créer une application Android.

Pour créer une application IOS il a fallu nous fournir un Mac avec l’environnement de développement Xcode, car il est toujours incertains d'utiliser des application exclusive à Appel (comme Xcode) sur un autre environnement que sur un Mac.

**<14 - Préparer et exécuter les plans de tests d’une application/>

Afin d’effectuer un plan de test sur mon application, j’ai décidé de mettre en place un Test Unitaire.

Utilisant Node.js pour construire mon Back-end, j’ai décidé d’utiliser le framework de test Jest, qui est réputé et intégré de base à l’installation du gestionnaire de paquet NPM.

  

(Test Unitaire à gauche et function testé à droite) 
![](https://lh4.googleusercontent.com/ER5WFNtNPpG6xSRlRKYLvhlfzf2KTurtMxdMPQJaHZ7qBjcofOidjCG8y-RNDpQYuiGizcSBQMuo79RgX6Z7NKunlK2QlG3QBHwWp8u35zy1wqDwKIfmk9OrF7etADYMDG5bKktoRFm1)![](https://lh5.googleusercontent.com/h99rzAGdycvhrcGRJE2E4UQKEdmKGCnNN2cg-GF4w82f15vwHEiZ4pGn2bFitRWOhW4sZxJNB7R6lV5NhNVUjiBJzoWPWZ4UhLrWjb84cLJlxcDRFfFXpyD08ki7KT7H5hCGX3KAt7Ye)  

Afin de m’assurer du bon fonctionnement de mon test unitaire, je crée également une erreur forcée en changeant un des résultats attendu (Key 1 et 3 au lieu de Key 2 et 3).

![](https://lh6.googleusercontent.com/BIfnu4nNU0KlOmpo0L06lt_dHp1BDoJ-yJp4XyK9BGjfE0TmgDg5BZZ7J0ISsrC9R-PlFoar5TznZrGesw-THxlbtPxc_Oi32HBTmvXacKaYOeB9ozTMNoaDxNnOzkgGfBL0wMB7tJXL)![](https://lh5.googleusercontent.com/g3RKPD_zcau_g3025O-q-dZuBwHDsKaoOMdmTHcWspQ5IGMlhoYPq04kzZrGic6ldicPC-bPqwckv4pBmYbQDX00VCspM5jnjFSP5OI2wlzw2I-PlMOvQeNaj3o6q5y9JBRrBj4ZOpCI)  
  
**<15 - Préparer et exécuter le déploiement d’une application/>

Afin de préparer le déploiement de notre application, nous avons décidé d’utiliser Render. Étant un projet que nous avons l'ambition de poursuivre même après notre période de formation, il fallait un hébergeur pouvant simplifier les mises à jour. Render est en lien direct avec GitHub permettant de s’update à chaque “git push”. dist

Nous avons commencé alors par “build” l’application afin de compacter le code et de le rendre moins lourd. Sur Render nous avons hébergé l’application dans les types correspondant, le Front-end dans le Static Site, le Back-end dans le  web service et la Base de données dans PostgreSQL (de Render).

Une fois en ligne nous nous sommes assurés de son bon fonctionnement que vous pouvez également apprécier à cette adresse : [https://game-crafting-calculator-front.onrender.com/recipes](https://game-crafting-calculator-front.onrender.com/recipes).