
J’ai réalisé ce projet avec un camarade de promotion, Mr Adrien Gouacide. Nous nous sommes aidés mutuellement même si dans un optique de productivité et de formation à un travail équipe, j’ai décidé de m’occuper exclusivement du Back-end avec Node.js et Adrien du Front-end avec React. Le but étant de se mettre dans les conditions d’une entreprise étant dépendant du travail et des besoins de l’autre équipe et de se perfectionner à l’utilisation de GitHub (commit, branch, merge, etc…).

**<1 - Maquetter une application/>

Le Front-end de notre application ne nécessite pas une infrastructure complexe, mais devait répondre à un besoins essentielles d’un utilisateur et à l’orchestration de l’arbre de craft.
Nous avons commencé par créer un Wireframe sur l’éditeur graphique Figma afin de structurer l’application et surtout le positionnement des diverses fonctionnalités.

![[Capture d’écran du 2023-02-28 11-05-30.png]]
 
 Une fois en accord sur son agencement nous avons créé son maquettage toujours sur l’éditeur graphique Figma comme vu au dessus. Le maquettage étant la phase la plus graphique du développement, il fallait trouver les images pour le background, le thème couleur, les formes et agencement des div, etc…
 
**<2 - Développer une interface utilisateur de type desktop/> :

Pour développer notre application web en une application multi-plateforme de bureau, nous avons décidé d’utiliser Electron.

Pour son installation nous somme aller sur le site officiel ou nous avons suivi la documentation à la lettre qui est très bien fourni.

Mais notre Front-end, Back-end et Base de données étant déjà hébergé sur Render et à ce jour n’ayant pas encore suffisamment de contenu hors-ligne à proposer sur notre application, nous avons opté pour une application "vide", qui est plus légère et tout aussi fonctionnelle.

En ligne 9 ci-dessous nous utilisons “win.loadURL” afin de lancer directement le site à l’ouverture de l’application, au lieu de mettre du classique “win.loadFile(‘index.html’)” qui ouvre l’index.html de l’application de bureau.

![](https://lh6.googleusercontent.com/FTx0UMF6CJG7xNmfADZHJ5xYXeJw-qLTlfgY8pfifOzHzJceWd9Zq8H65tFoplcqTW0uWL-cK7MUaSQJ9hLxO9ErAKyJluhiE8MCQ9fbnWXO_-hUJNUdiTIflBgM5QYUypE2G0RloNjv)

De ce fait, nous avons un dossier plus léger qui ne prend que peu de place et tout aussi fonctionnel. Bien sûr cette idée n’est que temporaire, ayant bien l’intention de poursuivre ce projet, du contenu hors ligne spécifique au desktop est prévu et sera ajouté une fois développées.

  

**<3 - Développer des composants d’accès aux données/> : pg

Afin d'établir le dialogue entre Node.js et PostgreSQL, j’ai utilisé la librairie "node-postgres" (pg) comme constaté sur l’image ci- dessous. 

![](https://lh5.googleusercontent.com/3lqnFAtRvBtxdhhSf3b_sjFdwEqq9weVhElfW7QSnvDuKMQlIUuACxtSG7rRJVKkZIO9vxoxEg9rAwkl7LSTIVgF_kW_d0b9xfZwBUusz7wSKuySdtfVLTwsl8_IY9cCd1rawowzP7GV)

Une fois la communication effectué il me suffit d’importer la connection:
![](https://lh4.googleusercontent.com/Zpc5sD7XR4WcVfuxrGR-GP5QsIIb1aNcq0-T4LhQvUj5BdwA5Oxy_LbFon5G6mFcP3n-3LhSCaii-d4nBnKhUYr55Rt3ztOl_xEtxk62u1V-B0Ty0fN_kQUMQheGoZonhTgyQw6Cd0SS)

Puis de créer les requêtes à la base de données en utilisant le langage SQL.
![](https://lh4.googleusercontent.com/lsCIqgh3B4e1CwGR_PM3TDRJol98E_vajWBhaGcKG_Ic11R8sr8O6CyeGqHh5oGnmBvzhtg2HAb_bQHD9m-FfOEWnbK3Bs5hGh-TURxh5ntGDL1r0EM1Kdbi5UuKB3PFXyZbX9rL_-wv)

Il faut par contre bien faire attention d'intégrer des paramètres à la requête pour éviter les injections SQL, comme vu en ligne 52 et ligne 54.

**<5 - Développer la partie back-end d’une interface utilisateur web/>

Pour le développement de notre application, nous avons décidé d’utiliser la plateforme Node.js avec le framework Express.

![[Capture d’écran du 2023-02-28 11-39-52.png]]

Afin de rendre le code plus lisible, j’ai séparé mon serveur.js en deux fichiers: 
- le "server.js" étant le point d'entrée, comprenant le port et le listen.
- le "app.js" qui comprend toutes les modalités, comme le CORS, express et le départ des routes.

J'ai créer un dossier accueillant toutes les routes, trillées par tables de Base de Données. Elles ne comprennes que les routes, les erreurs de connections et appelles les fonctions.
![[Capture d’écran du 2023-02-28 11-50-43.png]]

Puis les fonctions sont placer dans un dossier "controllers". Cette disposition permet de conserver des fonctions réutilisable si besoins et permet d'aller droit à l’essentielle.
![[Capture d’écran du 2023-02-28 11-54-49.png]]

Le dossier "database" accueil les connections avec la Base de Donnée.
Le dossier "middleware" contend les fichiers d'authentification, notamment la partie verification de JSONwebToken qui sera appeler des les routes voulu.
Le dossier "template" comprend le HTML et CSS de ma page template utiliser lors de la vérification par mail à l'inscription avec "NodeMailer".
Le dossier "utils" lui comprend toutes le fonction utilitaire utiliser comme le "getMissingParameters" appeller ligne 6 de l'image des routes au dessus.