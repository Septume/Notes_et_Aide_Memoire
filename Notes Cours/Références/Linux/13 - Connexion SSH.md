# Connexion ssh

### **Installation et configuration d'un serveur openssh**

- Installation : `sudo apt-get install openssh-server`
- Gestion du service : `sudo systemctl [start|stop|restart|reload|status] sshd`
- Fichier de configuration : `/etc/ssh/sshd_config`
- Fichier contenant les clés d'authentification des clients autorisées : `~/.ssh/config/authorized_keys`
- Manuel : `man sshd_config`
- Consulter les logs : `less /var/log/auth.log | grep sshd`

Exemple de configuration du service `sshd` (A indiquer à la fin du fichier pour écraser les options par défaut)

```
 # Port utilisé par SSH (par défaut 22)
 # Indiquer un numéro de port non utilisé entre 1024 et 65535
 Port 22
 
 # autoriser uniquement les connexions sur une interface IPv4
 AddressFamily inet
 
 # Authentification par mot de passe
 # (Mettre les deux directives à 'no' pour désactiver)
 PasswordAuthentication yes
 UsePAM yes
 
 # Authentification par clés
 PubkeyAuthentication yes
 
 # Interdire l'accès direct à root
 PermitRootLogin no
 
 # nombre max de tentatives d'authentification par connexion
 MaxAuthTries 2
 
 # Limiter le nombre de connexions concurrentes acceptées sans identification
 # 10 est le nombre de connexions acceptées
 # 30 est la propabilités en % que les suivantes soient bloquées
 # ce % augmente linéairement jusqu'à 100 % lorsque le full est atteint à 60 connexions 
 MaxStartups 10:30:60
 
 # A la connexion (avant authentification ) affiche le contenu du fichier indiqué
 Banner /etc/banner.txt
 
 # login des utilisateurs autorisés à se connecter en SSH
 AllowUsers user1 user2
 
 # utilisateurs non autorisés à se connecter en SSH
 DenyUsers user1 user2
 
 # nom des groupes dont les utilisateurs sont autorisés à se connecter
 AllowGroups group1 group2
 
 # Interdire les utilisateurs de ces groupes 
 DenyGroups group1 group2
 
 # Durée pendant laquelle une connexion sans être loggée sera ouverte.
 # si connexion par mot de passe laisser 2 minutes (2m)
 # sinon mettre 20 secondes (20s)
 LoginGraceTime 2m
 
```

### **Se connecter via ssh**

`ssh <login>@<hote> -p <num_port>`

Lors de la première connexion, un message d'avertissement apparait si le serveur ne fait pas parti des hôtes connus par le client.

```
 The authenticity of host (...) can't be established.
 ECDSA key fingerprint is (...)
 Are you sure you want to continue connecting (yes/no)?
```

Accepter la connexion permet d'ajouter l'empreinte de la clé publique du serveur dans le fichier `known_hosts` du client.

Pour connaitre cette empreinte lancer sur le serveur la commande :

`ssh-keygen -l -f /etc/ssh/ssh_host_ecdsa_key.pub`

Si la clé SSH a été changée sur le serveur un message d'avertissement apparait lors de la prochaine connexion :

`Warning: remote host identification has changed!`

On peut supprimer la clé du fichier `known_hosts` avec la commande :

`ssh-keygen -R <ip_hote>`

Type d'authentification :

- par mot de passe (Défaut). Par sécurité il est préférable de le désactiver :

	`PasswordAuthentication no`

	`UsePAM no`

- Authentification par clé publique/privée : Nécessite d'avoir une clé privée enregistrée sur le client et de connaitre la phrase de passe de cette clé

### **Authentification par clé**

Une paire de clés asymétriques est créé sur le client :

- La clé publique est enregistrée sur le serveur dans le fichier : `~/.ssh/authorized_keys`
- La clé privée est protégée par une passphrase (demandée lors de l'authentification sur le serveur)

Pour créer une paire de clé (Algorithme ECDSA) : `ssh-keygen -t ecdsa`

Pour envoyer la clé publique sur le serveur on utilise la commande :

`ssh-copy-id -i ~/.ssh/id_ecdsa.pub <login>@<hote>`

Si `StrictModes` est activé, il faut attribuer les droits adéquats au fichier `authorized_keys`

```
 chmod 700 ~/.ssh
 chmod 600 ~/.ssh/authorized_keys
```

### **Configuration du client ssh**

Le fichier de configuration est :

- Linux : `~/.ssh/config`
- Windows : `%USERPROFILE%\.ssh\config`

Il est possible de définir un raccourci pour établir une connexion à un serveur

```
 Host serveur # raccourci utilisé pour la connexion
  HostName 10.42.0.1 # nom ou IP du serveur
  User alice # nom d'utilisateur 
  Port 22 # port de connexion
  IdentityFile ~/.ssh/.id_ecdsa # clé d'authentification
```

Dans cette exemple : la commande `ssh serveur` sera équivalente à `ssh -p 22 -i ~/.ssh/.id_ecdsa alice@10.42.0.1` (Préciser la clé d' authentification à utiliser permet d'en définir plusieurs )

Pour éviter les coupures, on peut utiliser ces paramètres qui permettent de maintenir la connexion active

```
 # relancer la connexion toutes les 30 secondes 120 fois (donc pour une heure)
 ServerAliveCountMax 120 
 ServerAliveInterval 30
```

### **Agent ssh**

Utilitaire (tournant en arrière plan) qui permet de garder en mémoire la passphrase de la clé du client le temps de la session (Afin d'éviter de la saisir à nouveau à chaque connexion sur le serveur)

Lancer l'agent SSH en lui indiquant un sous-interpréteur à utiliser : `ssh-agent $SHELL`

Ajouter une clé : `ssh-add`

Tout les sous-processus de SSH agent se rappelleront automatiquement de la passphrase.

Lister les clés en mémoire : `ssh-add -l`

Retirer une clé : `ssh-add -d`

Retirer toutes les clé : `ssh-add -D`

### **Copie de fichiers**

`scp[fichierSource][dossierDestination]`

- `r` : copier récursivement un répertoire
- `P` : Indiquer le numéro de port (si ce dernier n'est pas celui par défaut)

Les fichiers distants sont indiqués sont la forme `<login>@<hote>:<fichier>`

du poste local au serveur distant : `scp <fichierSource> <login>@<hote>:<dossierDestination>`

du serveur distant au poste local : `scp <login>@<hote>:<fichierSource> <dossierDestination>`

Exemple

`scp fichier.txt alice@192.168.1.103:/home/alice`

`scp -r répertoire alice@192.168.1.103:/home/alice/`

`scp alice@192.168.1.103:/home/alice/fichier.txt .` ( le point à la fin de commande indique de copier le fichier dans le répertoire courant)

`scp alice@192.168.1.103:/home/alice/fichier.txt ./monFichier.txt` : renomme le fichier copié
