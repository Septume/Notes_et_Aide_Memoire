# Sécurité des applications Web

## Vocabulaire 

**Faille SQLi (Injection SQL)** : injection d'instructions SQL malveillantes pouvant compromettre la base de données. 

**Faille XSS (Cross-Site Scripting)** : Injection de code directement interprétable par le navigateur Web (JavaScript, HTML). Celle peut permettre à l'attaquant de modifier l'application Web (par exemple pour créer des liens vers des sites  malveillants) et de voler des informations (cookies, sessions)

**Faille LFI/RFI (Local/Remote File Inclusion)** : Inclusion de fichiers (locaux ou accessibles à distance) non prévue par l'application

**Faille CSRF (Cross-Site Request Forgery)** : Consiste à transmettre à un utilisateur un lien permettant d'exécuter à son insu une requête HTTP falsifiée vers l'application en utilisant ses propres droits. Pour que cela fonctionne l'utilisateur doit avoir une session ouverte en cours sur l'application. 

**Faille SSRF (Server Side Request Forgery)** : Se produit lorsqu'une application Web récupère une ressource distante sans valiser l'URL fournie par l'utilisateur. Cela permet à l'attaquant de contraindre  l'application à envoyer des requêtes HTTP falsifiée pouvant compromettre le serveur et le réseau où il se trouve. 

**Contrôle d'accès** : consiste à configurer  l'application web pour s'assurer que les utilisateurs ne peuvent accéder qu'aux données permises par leur rôle

**Principe de moindre privilège**  : Chaque fonctionnalité ne doit posséder que les privilèges et ressources strictement nécessaires à son exécution. Les utilisateurs doivent avoir également disposer un droit d'accès limiter au strict nécessaire. Appliquer le refus d'accès par défaut. 

**Principe de défense en profondeur** : Chaque composant de l'application doit avoir son propre mécanisme de sécurité.  

**Faille IDOR (Insecure Direct Object Reference)** : Références directes d'objets non sécurisées. Consiste à contourner le contrôle d'accès en modifiant les paramètres de l'URL pour accéder de manière non autorisée à une ressource. 

**Fuzzing** : Technique de tests automatisés qui consiste à injecter des données aléatoires  pour vérifier que qu'il n'y a pas de vulnérabilités au niveau des entrées 

**Audit de code** : Consiste à tester manuellement ou automatiquement le code ligne par ligne pour trouver des éléments vulnérables 

**HSTS ( HTTP Strict Transport Security)** : Mesure de sécurité qui consiste à indiquer au navigateur d'utiliser automatiquement le HTTPS. Pour cela le serveur envoi une entête HTTP `Strict-Transport-Security` 

**Same-Origin Policy** : Politique de sécurité des navigateurs qui permet de restreinte l'accès à une ressource depuis une origine différente. Voir [[Same-origin policy]]

**CORS (Cross-origin resource sharing)** : Méthode  qui consiste, via des entêtes HTTP, à autoriser les requêtes multi-origines pour accéder à des ressources qui par défaut obéissent à la règles du Same-Origin Policy. Voir [[Cross-origin resource sharing (cors)]]

**CSP (Content Security Policy)** : Politique de sécurité qui consiste, via des entêtes HTTP,  à indiquer au navigateur les contenus qu'il peut exécuter ou non.  Permet de limiter les attaques  XSS . Voir [[Content security policy (CSP)]]

**TLS (Transport Layer Security)** : Protocole de sécurisation des échanges de données sur Internet permettant l'authentification du serveur (via un certificat numérique)  ainsi que le chiffrement et l'intégrité des données. Ce protocole est utilisé dans la mise en œuvre du HTTPS

**SSL (Secure Sockets Layer)** : Prédécesseur de TLS. On utilise parfois le terme SSL/TLS pour permet indifféremment des deux protocoles 

**Certificat numérique** : Sorte de carte d'identité numérique permettant d'identifier et d'authentifier une personne physique ou morale et de chiffrer ses échanges. Le certificat doit être signé par une autorité de certification qui permet de garantir que les informations d'indentification soient exacts et qu'il correspondent bien à une entité réel. Pour un site Web on utilise un certificat SSL

**X.509**  : Standard le plus utilisé pour créer des certificats numériques. 

**Let's Encrypt** : Autorité de certification qui permet d'obtenir gratuitement un certificat X.509

**OWASP (Open Web Application Security Project)** : Organisme international qui fournis des lignes directrices contre les 10 principaux risques pour la sécurité des applications Web. Voir [[OWASP]]

## 6 aspects de la sécurité d’une application

- L’authentification 
- Le contrôle d’accès 
- L’intégrité des données
- La confidentialité des données 
- La non-répudiation 
- La protection contre l’analyse du trafic


## Recommandations

**Pendant la phase de conception** 
- Lister les données sensibles de l'application 
- Définir les exigences de sécurité de l'application
- Définir les rôles des utilisateurs et des privilèges associées (en appliquant le principe du moindre privilège)
- Prendre en compte les contraintes de sécurité fonctionnelles lors de l'écriture des scénarios utilisateurs 
- Établir une liste de contrôle de codage sécurisé 


**Contre les injections SQL**
-   Valider les entrées de formulaire
-   Faire des requêtes préparées
-   Utiliser des procédures stockées à la place du SQL dynamique
-   Utiliser un ORM
-   Utiliser des comptes utilisateurs SQL à accès limité (en lecture-seule) quand cela est possible
- Supprimer les comptes par défaut

**Pour les cookies**
- Sécuriser les cookies avec les instructions `Secure` et `HttpOnly`
-   Définir une date d'expiration sur le cookie de session

**Pour les mots de passe**
- Exiger des utilisateurs un mot de passe fort
- Mettre en place le verrouillage de compte en cas de nombreux échec de connexion
- Changer ou désactiver les comptes par défaut
- Utiliser une authentification forte
- Hachage et salage des mots de passe en base de données 
- Lors d'une action sensible, redemander le mot de passe à l'utilisateur (Protection contre la faille CSRF)

**Contrôle d'accès** 
-  Toutes les requêtes doivent passer par un mécanisme de contrôle d'accès unique situé côté serveur
-  Tout bloquer par défaut 
- Limiter le nombre de requêtes vers une ressource
- Utiliser la journalisation pour garder une trace des accès. 
- Utiliser des jetons JWT à durée de vie courte

**Pour les requêtes**
-   Utiliser GET que pour récupérer des informations
-   Utiliser POST pour les informations qui seront manipulés
-   Toutes les requêtes POST doivent utilisé HTTPS

**Empêcher la vulnérabilités IDOR** 
- Toutes les pages doivent avoir un contrôle d'accès
- Personnaliser les exceptions et code d'erreur (pour ne pas révéler les noms de colonnes de la base de données)
- Ne pas utiliser de nom prévisibles ou de références directes à la base de données dans l'URL. Utiliser à la pace des références, d'objet indirectes avec des paramètres et des combinaisons clé-valeur.








