
Pour ce projet j’ai décidé de créer une application de commande de nourriture en ligne.

J’ai décidé pour ce projet d’utiliser le framework Angular avec le langage TypeScript pour le front-end, Node.js et express pour le back-end et MongoDB comme base de données.

**<3 - Développer des composants d’accès aux données/> 

Pour la base de données j’ai utilisé le système de gestion NoSQL MongoDB pour sa praticité et son langage JSON.

J’ai utilisé la bibliothèque Mongoose pour créer une connexion entre MongoDB et le fichier Models de l’environnement de Node.js.

![](https://lh5.googleusercontent.com/qZKVfTBehvuJsNRwJtwfOFraOsA_eat3mLU0lmKzBAcp4OoRt5KV-oq56Am7qkQoom23EtxVrhbKue7ncZ1BNuUdQDmDwzqGQ3en6JH_rjrR51eNPeBp2LSRxbgLyiXmsMOjF24q_XQl)

**<4 - Développer la partie front-end d’une interface utilisateur web/>

J'ai décidé d'utiliser Angular dans la conception du Front-end.
![[Capture d’écran du 2023-02-28 15-00-43.png]]
J'ai commencer par répertorier les pages du site dans un dossier "components" comprenant le dossier "page" pour les components parents prenant tous l'écran et le dossier "partials" qui correspond aux components enfants.

Le dossier "service" correspond aux différentes routes mises en places dans le site.

les "shared/models" sont des classes de types TypeScript pour alléger les code sur les autres pages.
![[Capture d’écran du 2023-02-28 15-08-48.png]]

app.component.html qui représente le cœur de la composition principale  de l'application, important les components pour composer le site.
![[Capture d’écran du 2023-02-28 15-12-07.png]]

Le dossier "assets", comprenant le stockage physique de toutes images ou icônes étant utiliser dans le site.

Le fichier index.html représentant le cœur html de l'application client.