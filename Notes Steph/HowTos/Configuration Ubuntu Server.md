# Ubuntu server

## Utilisation de sudo

Toutes les commandes exécutées avec `sudo` sont journalisées dans le fichier `/var/log/auth.log`

Ouvrir un terminal en mode root. Attention : Les commandes ne seront pas journalisées :

`sudo -i`

`exit` ou `Ctrl+D` pour quitter

## Configuration

### Configuration réseau

Éditer le fichier : `/etc/netplan/50-cloud-init.yaml`

**Attention : il faut bien respecter l’indentation et ne pas utiliser des tabulations mais des espaces car sinon cela ne fonctionnera pas**

Exemple de configuration :

```
network:
    ethernets:
        enp0s3:
            addresses: []
            dhcp4: true
            optional: true
        enp0s8:
            addresses: [192.168.1.200/24]
            gateway4: 192.168.1.1
            nameservers:
                addresses: [8.8.8.8, 8.8.4.4]
            dhcp4: false
            dhcp6: false
    version: 2
```

Dans cette exemple :

- **enp0s3** : adresse Ipv4 dynamique obtenir par DHCP
- **enp0s8** :
	- adresse IP fixe, indiquée avec la notation CIDR (`192.168.1.200/24`)
	- adresse Ipv4 de la passerelle (`192.168.1.1`)
	- Deux adresses DNS (primaire et secondaire). On peut laisser vide pour utiliser les DNS par défaut (`addresses: []`)

Application les changements : `netplan apply`

Relancer le service réseau : `systemctl restart systemd-networkd`

Pour afficher les adresses configurées : `ip a`

### Mettre en français

`sudo apt-get update`

`sudo apt-get install language-pack-fr language-pack-fr-base manpages-fr manpages-fr-extra`

`sudo update-locale LANG=fr_FR.UTF8`

### Réglage de l’heure

Lister les zones horaires : `timedatectl list-timezones`

Régler la zone horaire : `sudo timedatectl set-timezone Europe/Paris`

Activer la synchronisation avec un serveur de temps : `timedatectl set-ntp true`

Vérifier le statut : `timedatectl`

fichier de configuration : `etc/systemd/timesyncd.conf`

Relancer le service : `sudo systemctl restart systemd-timesyncd.service`

## Installation des paquets et mise à jour

### Gérer les dépôts

Éditer le fichier : `/etc/apt/sources.list`

`main` : paquets libres maintenus par les développeurs d’Ubuntu

`restricted` : paquets non libres maintenus par les développeurs d’Ubuntu

`universe` : paquets libres maintenus par la communauté

`multiverse` : paquets non libres maintenu par la communauté

`security` : mises à jour de sécurité

`updates` : mises à jour recommandées

### Gestions des paquets

### Apt-get

Installer un paquet : `sudo apt-get install [package]`

Supprimer un paquet : `sudo apt-get remove [package]`

Supprimer un paquet et purger ses fichiers de configuration : `sudo apt-get purge [package]`

Supprimer les dépendances inutiles : `sudo apt-get autoremove`

Mettre à jour l’index : `sudo apt-get update`

Mettre à jour les paquets : `sudo apt-get upgrade`

### Apt-cache

`apt-cache search [motif]` : pour faire une recherche de paquets

`apt-cache show [package]` : pour obtenir des infos sur un paquet

### Dpkg

lister tous les paquets installés : `dpkg -l`

Install un paquet local .deb : `sudo dpkg -i package.deb`

### Tasksel

Permet d’installer un groupe de paquets lié à un tâche : Serveur LAMP, serveur OpenSSH, etc. les paquets sont également configuré pour fourni un service près à l’emploi.

Pour afficher la liste des tâches disponibles : `tasksel --list-tasks`

Pour lister les paquets lié à une tâche : `tasksel --task-packages [nomTache]`

Pour installer une tâche : `sudo tasksel install [nomTache]`

### Mise à jour automatique

le paquet `unattended-upgrades` permet d’installer automatiquement les mises à jour de sécurité

Installation : `sudo apt-get install unattended-upgrades`

Configurer : Éditer le fichier `/etc/apt/apt.conf.d/50unattended-upgrades`

Pour effectuer automatiquement les autres types de mise à jour, il faut décommenter les lignes correspondantes. (Par exemple : `"Ubuntu trusty-updates";`)

Certains paquets peuvent être mis en liste noire et ne seront donc pas mis à jour automatiquement.

```
Unattended-Upgrade::Package-Blacklist {
//      "vim";
//      "libc6";
//      "libc6-dev";
//      "libc6-i686";
};
```

Pour activer la mise à jour automatique, il faut modifier le fichier `/etc/apt/apt.conf.d/10periodic`

```
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";
```

Avec cette configuration la mise à jour se fera quotidiennement et les archives locales seront nettoyées à chaque semaine.

Le résultat des mises à jour automatiques sera journalisé dans `/var/log/unattended-upgrades`

### Mise à niveau

Pour migrer vers une nouvelle version : `do-release-upgrade`

LAMP

Installation avec tasksel

`sudo tasksel install lamp-server`

Installation classique :

`sudo apt install apache2 php mysql-server php-mysql`
