# APIs REST

API = Application Programming Interface

REST = Representational State Transfer  => Ensemble de normes architecturales se basant sur le protocole HTTP
API respectant les principes REST =>  API RESTful


6 principes pour qu'une API soit RESTful
1. Architecture client/serveur basé sur le protocole HTTP
2. Sans état (stateless) : Le serveur n'a pas besoin de conserver l'état de la session et du client entre deux requêtes GET. Pour cela le client doit à chaque fois faire une requête complète . ( Une exception peut être faite concernant les informations d'authentification)
3. Avec une mise en cache : Le client peut garder en mémoire les réponses reçus
4. Interface uniforme
5. En couches (Layered system) : Utilisation de serveurs/composants intermédiaires invisible pour le client
6. Avec code à la demande (facultatif) : le serveur peut transmettre au client du code exécutable

 Contraintes pour avoir une interface uniforme
- Identification des ressources dans les requêtes via une URI (Uniform Resource Identifier). Cette ressource peut avoir plusieurs représentations utilisant différents formats (HTML, XML, JSON…)
- Les représentations fournissent suffisamment d'information pour permettre au client de manipuler la ressource
- Les messages entre le client et le serveur doit contenir des informations nécessaires pour interpréter le message, comme son type MINE par exemple
- Le client doit pouvoir accéder aux ressources connexes via des hyperliens

Une ressource comporte :
- un nom (Par convention au singulier) 
- les données représentées 
- des informations supplémentaires sur les données. 
Les ressources sont regroupées dans une collection (dont le nom est par convention au pluriel) 

Endpoints (Point de terminaison) : URL sur laquelle l'API reçoit les requêtes des clients 












