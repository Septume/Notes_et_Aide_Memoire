# Envoyer un mail

`mail(destinataires, objet, message)` : permet d’envoyer un mail. Retourne un booléen pour indiquer le succès ou l’échec.

- destinataires : chaine contenant l’adresse mail. On peut en indiquer plusieurs en les séparant par une virgule
- objet et message : chaine
- (facultatif) entête : chaine indiquant des entêtes supplémentaires

Le message est envoyé à un serveur de messagerie indiquer dans le fichier de configuration

- `SMTP` : adresse d’un serveur SMTP
- `sendmail_from` : adresse mail de l’émetteur
- `sendmail_path` : chemin d’accès vers l’exécutable d’un serveur de messagerie.
