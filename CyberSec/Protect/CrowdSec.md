C'est un IPS (Intrusion Prevention System), qui ca déteter des cyber attaques et prendre des décisions.
CrowdSec à l'avantage d'être **Gratuit** et **Open Source**.

[Installation](https://www.crowdsec.net/)

Architecture de CrowdSec:
![[Pasted image 20230209132918.png]]

La console de CrowedSec permet de lister et referencer les attaques sur votre ordinateur.

## Utilisation

Il se comporte en deux gros point:

### Les Scenarios
Ce sont des paramètres qui vont permettre de détecter des attaques spécifique. 

(exemple : Détecter les attaque bruteforce sur le système d'authentification de Windows)

Il va agir de deux façons de détection :
- Par signature comme les antivirus, un système avec des adresses IP connues.
- Par comportement suspect

La grande force de CrowdSec est, que si il detect une adresse IP réalisant une action suspect sur votre ordinateur, elle sera automatiquement partager avec la communauté. L'adresse IP sera alors bloquée sur toutes les machine protéger par CrowdSec. 

### Les Bouncers
Ce sont des prises de décisions déterminé qui se lance à la suite d'une activité suspecte détecter par un scenario.

Pouvant par exemple bloquer une activité d'une adresse IP détecter par le scénario.