Oui, en plus des attaques XSS et d'injection SQL, il existe d'autres vulnérabilités fréquentes dans les sites Web, notamment :

1.  Injection de commandes : Cela se produit lorsqu'un attaquant injecte une commande malveillante dans une entrée utilisateur, ce qui peut permettre à l'attaquant de prendre le contrôle de la machine cible.
    
2.  Déni de service distribué (DDoS) : Cela se produit lorsqu'un attaquant envoie une quantité massive de requêtes à un site Web pour le rendre inaccessible pour les utilisateurs légitimes.
    
3.  Cross-Site Scripting de Stockage (XSS Stored) : Cela se produit lorsqu'un attaquant injecte du code malveillant dans une page Web qui est ensuite stockée sur le serveur et exécuté sur le navigateur de tous les utilisateurs qui visitent la page.
    
4.  Injection de code à protocole (POP) : Cela se produit lorsqu'un attaquant injecte du code malveillant dans une réponse protocole, telles que les réponses d'un serveur DNS ou d'un serveur web.
    
5.  Défaillance de la gestion des sessions : Cela se produit lorsqu'une application Web ne gère pas correctement les sessions utilisateur, ce qui peut permettre à un attaquant de prendre le contrôle de la session d'un autre utilisateur.
    
6.  Fuite de données sensibles : Cela se produit lorsqu'une application Web n'utilise pas correctement les protocoles de sécurité pour protéger les données sensibles telles que les mots de passe ou les informations de carte de crédit.
    

En conclusion, il est important de prendre en compte les vulnérabilités potentielles dans les sites Web et de les corriger rapidement pour maintenir la sécurité des utilisateurs. Il est également important de maintenir les applications Web à jour avec les derniers correctifs de sécurité.

## 1. Code injection

L'injection de code est l'un des **types d'attaques par injection** les plus courants. Si les attaquants connaissent le langage de programmation, le framework, la base de données ou le système d'exploitation utilisé par une application Web, ils peuvent **injecter du code via des champs de saisie de texte** pour forcer le serveur Web à faire ce qu'ils veulent.

Ces types d'attaques par injection sont **possibles sur les applications qui manquent de validation des données d'entrée.** <u>Si un champ de saisie de texte permet aux utilisateurs de saisir ce qu'ils veulent, alors l'application est potentiellement exploitable</u>. Pour éviter ces attaques, l'application doit **restreindre autant que possible les utilisateurs d'entrée sont autorisés à entrer.**

![](https://geekflare.com/wp-content/uploads/2020/02/Code-injection-e1580817731194.jpg)

Par exemple, il doit :
   -    limiter la quantité de données attendues, 
   -    vérifier le format des données avant de l'accepter, 
   -    restreindre le jeu de caractères autorisés.

**Les vulnérabilités d'injection de code peuvent être faciles à trouver**, simplement en **testant l'entrée de texte d'une application Web** avec **différents types de contenu**. Une fois trouvées, les vulnérabilités sont moyennement difficiles à exploiter. Mais lorsqu'un attaquant parvient à exploiter l'une de ces vulnérabilités, l'impact peut inclure la perte de confidentialité, d'intégrité, de disponibilité ou de fonctionnalité de l'application.

## 2. SQL injection

De la même manière que l'injection de code, cette attaque **insère un script SQL** - le langage utilisé par la plupart des bases de données pour effectuer des opérations de requête - **dans un champ de saisie de texte**. Le script est envoyé à l'application, qui **l'exécute directement sur sa base de données.** Par conséquence, **l'attaquant pourrait passer par un écran de connexion ou faire des choses plus dangereuses**, comme : 

  -     lire des données sensibles directement à partir de la base de données, 
  -     modifier ou détruire les données de la base de données 
  -     exécuter des opérations d'administration sur la base de données.

![](https://geekflare.com/wp-content/uploads/2019/11/sql-injection.jpg)

Les applications PHP et [ASP](https://qodop.com/faq/asp-informatique) sont sujettes à [Attaques par injection SQL](https://geekflare.com/fr/sql-injection-prevention-php/) en raison de ses **interfaces fonctionnelles plus anciennes.** <u>Les applications</u> [J2EE](https://www.ibm.com/docs/fr/configurepricequote/9.4.0?topic=implementing-introduction-j2ee-web-applications) <u>et ASP.Net sont généralement plus protégées contre ces attaques.</u> Lorsqu'une vulnérabilité d'injection SQL est détectée - et qu'elle peut être facilement trouvée - **l'ampleur des attaques potentielles ne sera limitée que par les compétences et l'imagination de l'attaquant.** Ainsi, l'impact d'une attaque par injection SQL est sans aucun doute élevé.

### Protection
Pour ce protéger d'une éventuelle attaque par injection SQL, il faut mettre des `Paramètre` à votre requête SQL.

```js
createAccout = async (username, email) => {
	try {
		await pool.query(
			`
				INSERT INTO app_user (
						username,
						email
					)
					VALUES(
						$1,
						$2
					)
			`,
			[
				username,
				email
			]
		);
	
	return [true, "user account created !"];
	
	} catch (error) {
		return [false, "server error"];
	}
};
```

## 3. Command injection

Ces attaques sont également possibles, principalement en raison d'une **validation d'entrée insuffisante.** <u>Elles diffèrent des attaques par injection de code en ce que l'attaquant insère des commandes système au lieu de morceaux de code de programmation ou de scripts.</u> Par conséquent, le pirate n'a **pas besoin de connaître le langage de programmation dans lequel l'application est basée** ou le **langage utilisé par la base de données**. Mais ils ont besoin de connaître le **système d'exploitation utilisé** par le serveur d'hébergement.

![](https://geekflare.com/wp-content/uploads/2020/02/Command-injection-e1581362803677.png)

Les commandes système insérées sont **exécutées par le système d'exploitation hôte** avec le [privilèges de l'application](https://geekflare.com/fr/privilege-escalation-attacks/), qui pourrait permettre **d'exposer le contenu de fichiers arbitraires** résidant sur le serveur :
   - d'afficher la structure de répertoires d'un serveur, 
   - de changer les mots de passe des utilisateurs entre autres,
   - etc...

### Protection

Ces attaques peuvent être évitées par un administrateur système, en limitant le niveau d'accès système des applications Web exécutées sur un serveur.


## 4. XSS (Cross-site scripting)

Chaque fois qu'une application insère une **entrée d'un utilisateur** dans la **sortie qu'elle génère**, sans la valider ni l'encoder, elle donne la **possibilité à un attaquant d'envoyer du code malveillant** à un autre utilisateur final. Les attaques de type Cross-Site Scripting (XSS) saisissent ces opportunités pour **injecter des scripts malveillants dans des sites Web de confiance**, qui sont finalement **envoyés à d'autres utilisateurs** de l'application, qui deviennent les victimes de l'attaquant.

Le navigateur des victimes **exécutera le script malveillant sans savoir qu'il ne devrait pas être fiable.** Par conséquent, le navigateur lui permettra d'accéder : 
   - aux tokens, 
   - aux cookies, 
   - aux informations sensibles stockées par le navigateur. 

S'ils sont correctement programmés, les scripts **pourraient même réécrire le contenu d'un fichier HTML.**

![](https://geekflare.com/wp-content/uploads/2020/02/Cross-site-scripting.png)

Les attaques XSS peuvent généralement être divisées en deux catégories différentes: **stored** et **reflected.**

###### Les Attaques XSS "Stockée"
Le script malveillant **réside en permanence** sur le serveur cible : 
   - dans un formulaire, 
   - dans une base de données, 
   - dans un "visitor log", 
   - etc... 

La victime l'obtient lorsque son **navigateur demande les informations stockées.**

###### Les Attaques XSS "Reflected"
Le script malveillant se **reflète dans une réponse** qui inclut l'entrée envoyée au serveur. Cela peut être un **message d'erreur** ou un **résultat de recherche**, par exemple.


## 5. XPath injection

Ce type d'attaque est possible lorsqu'une **application Web utilise des informations** fournies par un **utilisateur** pour créer une requête [XPath](https://fr.wikipedia.org/wiki/XPath) pour des données XML. Le fonctionnement de ces attaques est similaire à [Injection SQL](https://geekflare.com/fr/find-sql-injection/): les attaquants envoient des **informations mal-formées** à l'application afin de savoir comment les données XML sont structurées, puis ils **attaquent à nouveau** pour accéder à ces données.

XPath est un langage standard avec lequel, **comme SQL**, vous pouvez **spécifier les attributs** que vous souhaitez rechercher. Pour effectuer une requête sur des données XML, les applications Web utilisent **l'entrée utilisateur pour définir un modèle** auquel les **données doivent correspondre.** En envoyant une entrée mal-formée, le motif peut se **transformer en une opération** que l'attaquant souhaite appliquer aux données.

Contrairement à ce qui se passe avec SQL, dans XPath, **il n'y a pas de versions différentes**. Cela signifie que l'injection XPath peut être **effectuée sur n'importe quelle application Web utilisant des données XML**, quelle que soit l'implémentation. Cela signifie également que l'attaque peut être automatisée; par conséquent, contrairement à l'injection SQL, il a **le potentiel d'être déclenché** contre un nombre arbitraire d'objectifs.


## 6. Mail command injection

Cette méthode d'attaque peut être utilisée pour **exploiter des serveurs de messagerie** et des **applications qui construisent IMAP ou [SMTP](https://geekflare.com/fr/recommends/smtp/ "SMTP")** déclarations avec une **entrée utilisateur incorrectement validée.** Parfois, les serveurs IMAP et SMTP n'ont **pas une protection solide** contre les attaques, comme ce serait le cas avec la **plupart des serveurs Web**, et pourraient donc être plus exploitables. En entrant via un serveur de messagerie, les attaquants pourraient échapper à des restrictions telles que :
   - des captchas, 
   - un nombre limité de requêtes, 
   - etc...

![](https://geekflare.com/wp-content/uploads/2020/02/Mail-command-injection.png)

###### Les serveurs SMTP
Pour exploiter un serveur SMTP, les attaquants ont besoin d'un **compte de messagerie valide** pour envoyer des messages avec des commandes injectées. Si le serveur est vulnérable, il répondra aux demandes des attaquants, leur permettant, par exemple, de **contourner les restrictions du serveur** et d'utiliser ses services pour **envoyer du spam.**

###### Les serveurs IMAP
L'injection IMAP pourrait être effectuée **principalement** sur des applications de **messagerie Web**, en exploitant la fonctionnalité de **lecture de messages.** Dans ces cas, l'attaque peut être réalisée en saisissant simplement, dans la **barre d'adresse** d'un navigateur web, une **URL** avec les commandes injectées.


## 7. CRLF injection

L'insertion de caractères de retour chariot et de saut de ligne **combinaison connue sous le nom de CRLF** dans les champs d'entrée de formulaire Web représente une méthode d'attaque appelée **injection CRLF**. Ces **caractères invisibles** indiquent la **fin d'une ligne** ou la **fin d'une commande** dans de nombreux protocoles Internet traditionnels, tels que HTTP, MIME ou NNTP.

Par exemple, l'insertion d'un CRLF dans une requête HTTP, suivie d'un certain code HTML, pourrait **envoyer des pages Web personnalisées** aux visiteurs d'un site Web.

Cette attaque peut être effectuée sur des applications Web vulnérables qui **n'appliquent pas le filtrage approprié** à l'entrée de l'utilisateur. Cette **vulnérabilité** ouvre la porte à d'autres types d'attaques par **injection, telles que XSS et l'injection de code**, et pourrait également provenir d'un site Web piraté.


## 8. Host Header injection

Dans les serveurs qui **hébergent** de nombreux sites Web ou applications Web, **l'en-tête d'hôte** devient nécessaire pour déterminer lesquels des sites Web résidents ou des applications Web **chacun d'entre eux appelé hôte virtuel** doit traiter une demande entrante. La valeur de l'en-tête indique au serveur vers lequel des hôtes virtuels envoyer une demande. Lorsque le serveur reçoit un **en-tête d'hôte non valide**, il le transmet généralement au **premier hôte virtuel de la liste**. Cela constitue une **vulnérabilité** que les attaquants peuvent utiliser pour **envoyer des en-têtes d'hôte** arbitraires au **premier hôte virtuel** d'un serveur.

La manipulation de l'en-tête de l'hôte est **généralement liée** aux applications **PHP**, bien qu'elle puisse également être **effectuée avec d'autres technologies** de développement Web. Les attaques d'en-tête d'hôte fonctionnent comme des **catalyseurs pour d'autres types d'attaques**, telles que **l'empoisonnement du cache Web**. Ses conséquences pourraient inclure l'exécution d'opérations sensibles par les attaquants, par exemple la **réinitialisation des mots de passe**.


## 9. LDAP injection

LDAP est un protocole conçu pour **faciliter la recherche de ressources** (appareils, fichiers, autres utilisateurs) dans un réseau. Il est très utile pour les intranets et, lorsqu'il est utilisé dans le cadre d'un système d'authentification unique, il peut être utilisé pour **stocker** les noms d'utilisateur et les **mots de passe**. Les requêtes LDAP impliquent l'utilisation de caractères de contrôle spéciaux qui affectent son contrôle. Les attaquants peuvent potentiellement modifier le comportement prévu d'une requête LDAP s'ils peuvent y insérer des caractères de contrôle.

![](https://geekflare.com/wp-content/uploads/2020/02/LDAP-injection.jpg)

Encore une fois, le problème racine qui permet les attaques par injection LDAP est une entrée utilisateur incorrectement validée. Si le texte qu'un utilisateur envoie à une application est utilisé dans le cadre d'une requête LDAP sans le nettoyer, la requête pourrait finir par récupérer une liste de tous les utilisateurs et l'afficher à un attaquant, simplement en utilisant un astérisque (*) à droite place à l'intérieur d'une chaîne d'entrée.

## Prévenir les attaques par injection

Comme nous l'avons vu dans cet article, toutes les attaques par injection sont dirigées vers des serveurs et des applications en libre accès à tout internaute. La responsabilité de prévenir ces attaques est répartie entre les développeurs d'applications et les administrateurs de serveur.

Les développeurs d'applications doivent connaître les risques liés à la validation incorrecte des entrées utilisateur et apprendre les meilleures pratiques pour nettoyer les entrées utilisateur à des fins de prévention des risques. Les administrateurs de serveur doivent régulièrement auditer leurs systèmes pour [détecter les vulnérabilités](https://geekflare.com/fr/open-source-web-security-scanner/) et corrigez-les dès que possible. Il existe de nombreuses options pour réaliser ces audits, à la demande ou automatiquement.