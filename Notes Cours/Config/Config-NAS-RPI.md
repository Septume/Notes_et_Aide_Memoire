# Configuration du NAS
## Préparation

### Matériels utilisés

- [Un Raspberry Pi 3 Model B+](https://fr.wikipedia.org/wiki/Raspberry_Pi) (En abrégé RPI) + son alimentation
- Une carte SD de 16 Go de classe 10 (pour le système)
- Un câble Ethernet (Pour brancher le RPI sur la box Internet)
- Un disque dur externe de 1 To (pour les données)

Pour les besoins de l'installation uniquement :
- Un écran + câble HDMI
- Un clavier

### Installation de Linux

**Distribution utilisée** : Raspberry Pi Lite

- Se rendre sur la page de téléchargement [des images systèmes](https://www.raspberrypi.com/software/operating-systems/) (Il faut faire attention à bien télécharger l'image qui correspond à la version Lite et non celle de la version Desktop )
- Utiliser l'utilitaire [Rufus](https://rufus.ie/fr/) pour écrire l'image sur la carte SD
- Ensuite insérer la carte SD dans le RPI et brancher sur celui-ci un écran (avec un câble HDMI) et un clavier pour effectuer la configuration initiale

## Configuration initiale

### Pendant l'installation

- Choisir la disposition du clavier
- Définir un nom d'utilisateur et un mot de passe

### Après l'installation

Lancer la commande `sudo raspi-config`

- *système options -> hostname* : Indiquer un nom pour la machine (éviter absolument d'utiliser des espaces, accents et caractères spéciaux autres que le `-` ou le `_`)
- *interface options -> SSH* : Activer le SSH

Mettre à jour le système : `sudo apt-get update && sudo apt-get upgrade -y`  
Arrêter le système avec la commande `sudo shutdown now`

### Se connecter en SSH

Après avoir brancher le RPI sur un port Ethernet de la box, lancer un terminal depuis une ordinateur connecté au réseau local et taper la commande `ssh username@hostname` (En remplaçant *username* et *hostname* par le nom d'utilisateur et le nom de la machine définis lors de l'installation)  
Lors de la première connexion taper *yes* pour accepter le fingerprint.

## Attribuer une IP fixe au RPI

#### Récupérer les informations sur la configuration réseau actuelle

- Récupérer l'adresse IP actuelle du RPI : `hostname -I`
- Récupérer l'adresse IP de la box : `ip r | grep default`
- Récupérer l' adresse IP du DNS actuel : `sudo cat /etc/resolv.conf`

Noter toutes les informations. Par exemple :

- Adresse IP : `192.168.0.50`
- Adresse de la box : `192.168.0.254`
- DNS : `192.168.0.254`

#### Modifier la configuration

Éditer le fichier de configuration du serveur DHCP du RPI : `sudo nano /etc/dhcpcd.conf`  
Et indiquer en bas du fichier (En utilisant les infos récupérer plus haut)

```
interface eth0
static ip_address=192.168.0.50/24
static routers=192.168.0.254
static domain_name_servers=192.168.0.254
```

Puis redémarrer le RPI : `sudo reboot`

## Configuration du disque externe

### Formatage du disque

Lancer la commande `sudo fdisk -l`  
Dans la liste des informations affichées par la commande repérer celle qui concerne le disque dur externe.

Par exemple

```
Disk /dev/sda: 931.51 GiB, 1000204883968 bytes, 1953525164 sectors
Disk model: External USB 3.0
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x9d71040c
```

Noter le nom du disque (Dans notre exemple il s'agit de `sda`)  
Lancer la commande `sudo fdisk /dev/sda` (en remplaçant *sda* par le nom noté si besoin)  
Entrer la commande `n` pour créer une partition. Pour chaque questions posées appuyer sur entrée pour valider le choix par défaut.

Exemple

```
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):
Partition number (1-4, default 1):
First sector (2048-1953525163, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-1953525163, default 1953525163):

Created a new partition 1 of type 'Linux' and of size 931.5 GiB.
```

Une fois que la partition est créée, taper la commande `w` pour valider  
Ensuite taper `q` pour quitter l'utilitaire

### Montage de la partition

Lancer la commande `sudo fdisk -l`

Dans la liste des informations affichées par la commande repérer celle qui concerne la partition

Par exemple

```
Device     Boot Start        End    Sectors   Size Id Type
/dev/sda1        2048 1953525163 1953523116 931.5G 83 Linux
```

Noter le nom de la partition (Dans notre exemple il s'agit de `sda1`)

Créer le dossier où sera monté la partition : `sudo mkdir /data` (Dans cet exemple le dossier de montage est nommé *data*)  
Fixer les droits d'accès au dossier : `sudo chown root:root /data`  
Monter la partition : `sudo mount /dev/sda1 /data` (en remplaçant *sda1* si besoin)

Vérifier le montage : `df /dev/sda1`

Si tout est ok, éditer le fichier */etc/ fstab* avec la commande : `sudo nano /etc/fstab`  
Copier tout en bas la ligne suivante

```
/dev/sda1       /data ext4    defaults        0       2
```

(en remplaçant le nom de la partition *sda* si besoin)  
Puis redémarrer le système : `sudo reboot`  
Re-vérifier le montage : `df /dev/sda1`

## Création des utilisateurs

### Utilisateur avec droit sudo

`sudo adduser username`

Pour donner les droits sudo à un utilisateur, lancer commande `sudo visudo`

Dans le fichier qui s’ouvre, ajoutez la ligne : `username ALL=(ALL:ALL) ALL` (Remplacer *username* par le nom d'utilisateur créé ). Cette ligne doit être ajouté sous la ligne `root ALL=(ALL:ALL) ALL` de la section `# User privilege specification`

Taper Ctrl + O pour enregistrer et Ctrl + X pour quitter visudo

### Utilisateur avec droit restreint

- Pas de droit root
- utilisateur chrooté (consiste à emprisonner l'utilisateur dans un son répertoire personnel sans possibilité de remonter à la racine de l'arborescence de fichier)
- La connexion ne pourra se faire que via SFTP

#### Création du dossier de l'utilisateur

Dans cette exemple l'utilisateur est nommé *digifab* et son dossier personnel a pour chemin */data/digifab/home*

```
sudo mkdir -p /data/digifab/home
sudo chown root:root /data/digifab
sudo chmod 755 /data/digifab
sudo chmod 750 /data/digifab/home
```

Remarque : Le dossier qui sera chrooté doit avoir les droits root. Il faut donc utiliser un sous dossier qui sera le dossier personnel de l'utilisateur chrooté

#### Création de l'utilisateur

```
sudo useradd digifab -m -d /data/digifab/home
```

## Configurer SSH

Éditer le fichier de configuration : `sudo nano /etc/ssh/sshd_config`

````
# Changer le port par défaut ( Indiquer un numéro de port non utilisé entre 1024 et 65535)
Port 1024

# Interdire l'accès direct à root
PermitRootLogin no

# Interdire l'accès à l'utilisateur par défaut (celui qui a été créé pendant l'installation)
DenyUsers nom-utilisateur

# Activer l'accès SFTP
Subsystem       sftp    internal-sftp

# digifab accès SFTP chrooté seulement
Match User digifab
  ChrootDirectory /data/digifab
  ForceCommand internal-sftp
  AllowTCPForwarding no
  X11Forwarding no
Match all
````

Redémarrer le service : `sudo systemctl restart sshd`

Pour se connecter : `ssh user@hostname -p 1024`(Remplacer par le nom de l'utilisateur et le hostname de la machine créé à l'installation. Penser également à indiquer le bon numéro de port)

#### Configuration de la box pour l'accès SSH à distance

Exemple avec une Freebox

Paramètres -> Mode avancé -> Gestion des ports -> ajouter une redirection

- IP destination : Adresse IP locale du RPI
- IP source : Toutes (remarque : on peut restreinte l'accès en indiquant une IP spécifique )
- Protocole : TCP
- Port début : 20
- Pour de fin : 20
- Port de destination : 20

Récupérer l'adresse IP externe grâce à un service comme [whatismyip.com](https://www.whatismyip.com)

Pour se connecter : `ssh user@ip -p 1024`

## Créer un partage de fichiers avec Samba

Installer Samba : `sudo apt-get install samba`  
Éditer le fichier de configuration : `sudo nano /etc/samba/smb.conf`  
Indiquer les informations suivantes

```
[share]
path = /data/digifab/home
public = yes
browseable = yes
guest only = yes
read only = no
force create mode = 0666
force directory mode = 0777
```

Taper cette commande pour relancer Samba : `sudo systemctl restart smbd`

Utiliser l'adresse `\\hostname\share `pour accéder au partage (remplacer *hostname* par le nom de la machine qui a été définie)

## Configuration d'un serveur web

### Installation Apache, MariaDB et PHP

 `sudo apt install apache2 php libapache2-mod-php mariadb-server php-mysql`

### Configurer MariaDB

Lancer le script pour sécuriser le gestionnaire de base de données : `sudo mysql_secure_installation`

Et valider les étapes

```
Enter current password for root (enter for none) : laisser vide et appuyer sur entrer 
Switch to unix_socket authentication [Y/n] :  n
Change the root password? [Y/n] n
Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] Y
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y
```

### Créer un virtualhost

Créer le fichier `/etc/apache2/sites-available/site.conf` avec les droits d'administration, et copiez-y le contenu suivant :

```
<VirtualHost *:80>
	DocumentRoot /var/www/html
	ServerName site.local
    <Directory /var/www/html>
    	Require all granted
    	AllowOverride All
    	Options FollowSymLinks MultiViews
    </Directory>
     Redirect permanent / https://www.digifab.local/
     ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


```

Puis activez ce nouvel hôte virtuel :

```
a2ensite site.conf
```

Finalement, redémarrez apache :

```
sudo systemctl restart apache2
```

### Activer SSL pour Apache

```
sudo a2enmod ssl
sudo systemctl restart apache2

```

Créer un certificat

````
sudo apt install certbot python3-certbot-apache
sudo certbot --apache --register-unsafely-without-email
````

Répondre aux questions

Redémarrer Apache : `sudo systemctl restart apache2`
