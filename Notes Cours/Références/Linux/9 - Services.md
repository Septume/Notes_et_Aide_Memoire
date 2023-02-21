# Services

La gestion des services se fait via la commande :

`systemctl [action] <Nom_du_service>.service`

Les actions :

- `enable` : Activer le lancement automatique du service
- `disable` : Désactiver le lancement automatique
- `start` : Démarrer le service
- `stop` : Arrêter le service
- `restart` : Redémarrer le service
- `reload`: Recharger le fichier de configuration du service
- `status`: Voir le statut du service

Pour afficher la liste des services actifs : `systemctl list-units --type=service`

Pour afficher les logs : `journalctl`

Pour filtrer les logs d'un service particulier : `journalctl -u [nom_du_service]`
