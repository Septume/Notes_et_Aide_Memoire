(Référencer par l'OWASP)

1. Injection
2. Piratage de session
3. Exposition de données sensibles
4. Entités externes XML ou XXE
5. Contournement du Contrôle d'accès
6. Mauvais configurations de sécurité
7. Failles XSS
8. Désérialisation non sécurisée
9. Utilisation de composants avec des vulnérabilités
10. Exploitation du manque de monitoring

### 1. Injection
Une attaque par injection est une attaque permettant l’injection de **code arbitraire** dans l’application. Cela se produit lorsque des données non maîtrisées sont exécutées par le moteur présent sur le backend de l’application. Les données de l’attaquant sont exécutées **sans** **autorisations** **adéquates**.

L’injection de code non autorisée peut permettre à un attaquant d’accéder à des données auxquelles il n’a normalement pas accès.

### 2. Piratage de session
Beaucoup d'applications exigent qu'un utilisateur se connecte pour arriver sur des pages auxquelles lui seul a accès. L’application est vulnérable à une attaque si un utilisateur malveillant peut obtenir un **accès non autorisé** aux mots de passe, clés et jetons pour pirater la session d'un autre utilisateur.

### 3. Exposition de données sensibles
Les données stockées ou échangées via une application doivent être protégées pour éviter l’interception par une personne malveillante. Les bases de données qui enregistrent les données personnelles, les données de cartes de crédit, les noms d'utilisateur et les mots de passe représentent une cible de choix pour un pirate. Si ces données ne sont pas **chiffrées**, elles ne sont pas sécurisées et peuvent être récupérées lorsqu’elles sont en transit par exemple. L'utilisation de **techniques de chiffrement** et de pratiques de sécurité peut atténuer ce type d’attaques.

### 4. Entités externes XML ou XXE
Le **format** **XML** permet de faciliter l’échange de données sous forme d'arborescence. Il est largement utilisé sur Internet. Il peut être exploité via l’injection XXE ou XML External Entity. XML External Entity est une attaque contre les applications qui parsent des entrées XML (exemple flux RSS). Cette attaque a lieu lorsque l'analyseur XML est mal configuré et contient une référence à une entité externe.

### 5. Contournement du Contrôle d'accès
Cette attaque vise les fonctionnalités des applications web qui nécessitent un **contrôle d'accès**. Dans ce cas, les pirates peuvent utiliser l'URL pour contourner l'authentification, par exemple. Ce type d’exploitation peut par exemple révéler comment une base de données est organisée.

### 6. Mauvais configurations de sécurité
Une mauvaise configuration de sécurité est le plus souvent observée dans les en-têtes HTTP qui permettent de donner des indications sur la configuration du serveur, ou via la gestion des exceptions par défaut. Les codes d'erreur et les exceptions courantes peuvent donner à un attaquant un aperçu de l'application.

### 7. Failles XSS
Les **failles XSS** se produisent chaque fois qu'une application inclut des **données non fiables** dans une nouvelle page web sans validation ou échappement. Les failles XSS permettent aux attaquants d'exécuter des scripts dans le navigateur de la victime, ce qui peut détourner des sessions utilisateur, altérer des sites web ou rediriger l'utilisateur vers un site malveillant.

### 8. Désérialisation non sécurisée
Une vulnérabilité de type “insecure désérialisation” permet à un utilisateur malveillant d'accéder et de modifier les fonctionnalités de l’application ciblée.

### 9. Utilisation de composants avec des vulnérabilités
Même si votre application est sécurisée, vous devez vous assurer que le framework, les bibliothèques, les appels API et la plateforme que vous utilisez ne sont pas vulnérables.

Lorsqu'une nouvelle vulnérabilité est découverte, un **correctif** est généralement proposé. Il faudra alors l’appliquer pour garantir la sécurité de l’application.

### 10. Exploitation du manque de monitoring
Pour garantir la sécurité d’une application, il est nécessaire de surveiller et de **monitorer** les connexions. De nombreux serveurs vulnérables servent de rebond aux attaquants. La mise en place de monitoring permettra de détecter une anomalie sur le serveur.