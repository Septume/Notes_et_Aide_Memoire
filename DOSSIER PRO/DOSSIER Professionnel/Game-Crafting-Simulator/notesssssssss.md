Comme expliquer dans la partie 9 (Collaborer à la gestion d’un projet informatique et à l’organisation de l’environnement de développement), nous avons décider de partager notre travail en deux. 
Adrien pour développer le Front-End et moi pour développer le Back-End, afin de nous donner plus le temps de parfaire un projet un commun.

Créant une “Organization” pour notre projet sur GitHub, nous avons séparé mon travail sur le Back-end et le travail d’Adrien sur le Front-end en deux “Repositories” distinct et une documentation pour regrouper tous les informations complémentaire(MCD, code SQL, etc...). Cela afin de bien séparer le code du Front-End et celui du Back-End, facilitant le deployment futur à Render.
![[Capture d’écran du 2023-02-28 12-36-33.png]]

Pour le Front-End nous avons décidé d'utiliser React avec l'emplois de TypeScript afin de ce parfaire sur cette technologie. 
Pour le Back-End nous avons décidé d'utiliser Node.js afin que je me familiarise plus avec cette environnement.

Nous avons déployer un token avec "JSONwebToken" permettant de sécuriser plusieurs routes et verifier l'identités des utilisateurs.
![[Capture d’écran du 2023-02-28 12-46-45.png]]

Pendant sa création nous faisons circuler le "user_id" et "email" à l’intérieur du token et récupérer par le Front-End pour permettre d'afficher les informations de l'utilisateur uniquement si il a le token.
![[Capture d’écran du 2023-02-28 12-48-05.png]]

Pour s'assurer de stocker les mots de passes chiffrer dans la Base de Donnée pour éviter de répéter d'erreur de l'entreprise RockYou. Nous utilisons le hasher unidirectionnel "Bcrypt".
![[Capture d’écran du 2023-02-28 13-00-35.png]]
