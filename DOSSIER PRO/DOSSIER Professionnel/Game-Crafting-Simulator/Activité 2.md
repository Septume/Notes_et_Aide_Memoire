**<6 - Concevoir une base de données/>

Idéalement au vu de notre base de données et de ses nombreuses jointures, nous aurions dû nous orienter vers une base de données de type Graphs comme “Neo4j”. Mais nous n’avions ni le temps, ni la connaissance de cette technologie pour respecter le planning dans les temps.

Nous avons alors décidé de travailler avec le système de gestion PostgreSQL. Mais la confection de MCD (Modèle Conceptuel des Données) y étant limitée en jointures, nous l’avons alors créé sur le sur le logiciel PowerDesigner qui offre plus de liberté de création.

![](https://lh5.googleusercontent.com/wxRE5Xe6mIrweJuPbl3pNCxLy11PvtO1E5gnoxirIIikIhwIzdAr9ayj44Sryf-cxgfIMtEEA7I9jsS6j7H0cXYGLXscNMv3R3t3UmucUZR3v2HAc9BdTyMvM_zAVaMfCzFdVUM47hHT)



**<7 - Mettre en place une base de données/>

Une fois le MCD réalisé et les jointures conformes à nos attentes, nous avons préféré créer la BDD en le codant directement.

![](https://lh5.googleusercontent.com/oYfnePXyVz8PrWF4VOGfOCDYH_9k7EIKim3jRQFT-wOQC9ZnyNCIgQckWYQr0SdKuXh3ElP2k2yAhUTALbRsxcG51Zb0Qdn5osd-7wbQWm3a-OATYjB9ZVDQSDF2zzk0A2gt4tZQ7o8d)

En intégrant les tables et jointures une par une, nous avons pu tester au fur et à mesure la bonne intégration et fonctionnalité des tables, préférant cette façons plus stable au vu de la petite base de donnée que nous devions réaliser.

A chaque création de table nous avons ajouter "IF NOT EXISTS" afin de nous assurer que chaque elements sont uniques.
La création d'un id avec la "PRIMARY KEY" pour identifier de façon unique chaque ligne du tableau.

**<8 - Développer des composants dans le langage d’une base de données/>

Afin de s'assurer que chaque ligne de notre tableau "users" comporte un E-mail unique, nous avons ajouter un trigger et une fonction.

Le triggers à l'action de lancer execution de la function "check_email_exists()" avant une insertion sur la table "users" sur chacune des lignes.

La function quant à elle est charger de vérifier si l'email existe déjà et de simuler une erreur avec un message personnalisé si il y en a déjà un. 

![[Capture d’écran du 2023-02-27 17-40-18.png]]