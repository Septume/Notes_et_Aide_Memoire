**<7 - Mettre en place une base de données/>

Pour ce projet d’application de commande de nourriture en ligne, j’ai décidé de m'orienter vers un base de données utilisant le système de gestion NoSQL MongoDB et sa bibliothèque de programmation orientée JavaScript, Mongoose. 

J’y ai créé trois tables de models, une pour stocker mes produits, une seconde pour stocker les données d’utilisateur et une troisième pour stocker les produits enregistrés dans le panier et ainsi que des données de ventes de l’utilisateur.

  ![[Capture d’écran du 2023-02-28 10-47-46.png]]
Pour la création de la table "User", j'ai commencé à importer les fonctionnalités de Mongoose { Schema, model }.
Commencer par créer le typage de cheque ligne de la table.
Puis j'ai créer une function typique de Mongoose listant chaque propriétés  et permettant la création de la table désiré.

J’ai utilisé bien sûr le service de base de données MongoDB Atlas pour mettre ma base de données sur un compte gratuit que j’ai créé.

Une fois correctement mise en place, j’ai testé son bon fonctionnement en utilisant l’application Postman.

