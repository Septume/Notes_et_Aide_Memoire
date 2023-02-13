# Vs code - shortcuts

## Interface

### Général

- `CTRL + MAJ + P`ou `F1` : Palette de commande
- `CTRL + P` : Accès rapide
  - Par défaut : Rechercher des fichiers. Pour ouvrir d'autre fichiers sans fermer la liste appuyer sur la flèche droite plutôt que entrée
  - `?` Liste des commandes globales
  - `>` Accéder aux commandes (ou faire`CTRL + MAJ + P`)
  - `@` Accéder à un symbole dans le fichier (par ex: variable, classe) (ou faire `CTRL + MAJ + O`)
	  - `@:` trier les symboles par type
  - `#` Accéder à un symbole dans l'espace de travail (ou `CTRL + T`)
  - `:` Accéder à un numéro de ligne (ou `CTRL + G`)

### Fenêtre

- `CTRL ° MAJ + N` : Nouvelle fenêtre/instance
- `CTRL + MAJ + W` : Fermer fenêtre / instance

### Barre latérale / panneau

- `CTRL + B` : Afficher/cacher la barre latérale
- `CTRL + MAJ + E` : Explorateur de fichiers
- `CTRL + MAJ + F` : Recherche globale
- `CTRL + MAJ + H` : Recherche globale avec remplacer
- `CTRL + J`: Afficher/cacher le panneau
- `CTRL + MAJ + M`: messages d'erreurs et d'avertissements (problèmes)
- `CTRL + ù` : terminal

### Zoom

- `CTRL + NumPad +` : Zoom avant
- `CTRL + NumPad +` : Zoom arrière
- `CTRL + NumPad 0` : Zoom initial

### Explorateur

- `Entrée` : Ouvrir le fichier
- `CTRL + Entrée`: ouvrir sur le coté
- `droite`: déplier le
- `gauche`plier le dossier
- `CTRL gauche`: plier tout les dossiers

### Editeurs

- `CTRL + *` : fractionner éditeur (Par défaut le fractionnement se fait sur la droite)
- `MAJ + ALT + 0` : Passer à une disposition des éditeurs vertical et vice-versa
- `CTRL + W` ou `CTRL + F4` fermer un éditeur (Ne fonctionne pas sur un éditeur épinglé)
- `CTRL + MAJ + T` : ré-ouvrir l'éditeur fermé
- `CTRL + K MAJ + Entrée` : épingler /dé-épingler un éditeur
- `CTRL + MAJ + pagPre pageSuiv` : déplacer un éditeur sur la gauche/droite
- `CTRL + K gauche/droite` : déplacer un groupe d'éditeur

### Autres

- `CTRL + K Z`: Mode zen (`ECHAP ECHAP` pour quitter)
- `CTRL + MAJ + V`: aperçu fichier mardown
- `CTRL + K V`: Aperçu fichier markdown (sur le coté)

## Navigation

- `CTRL + TAB` : Naviguer dans les fichiers ouverts ( `CTRL + MAJ + TAB` pour naviguer en sens inverse)
- `CTRL + 1`, `CTRL + 2`, etc : Naviguer des les groupes d' éditeurs
- `CTRL + 0` : Aller dans la barre latérale
- `CTRL + R` : Naviguer entre les dossiers et espaces de travail récement ouvert
- `Début\fin` : Aller au début/à la fin de la ligne
- `ALT + flèche gauche` : Aller à l'emplacement où le curseur se trouvait précédemment.
- `ALT + flèche droite` : Revenir à l'emplacement suivant
- `CTRL + début/fin` : naviguer au début/ à la fin du fichier
- `CTRL + G`: Aller à un numéro de ligne
- `F2` ou `CTRL + clic`: Aller à la définition d'un symbole
- `Ctrl + clic` : Suivre un lien
- `ALT + Scroll` : défilement rapide
- `CTRL + M`: permet de basculer dans un mode ou la touche `TAB` permet de changer le focus dans l'interface (refaire le raccourci pour quitter)

## Edition

`CTRL + ESPACE` : Afficher le menu IntelliSense. Faire une deuxième fois le raccourci permet d'afficher l'aide sur les entrés ou d'autres infos rapides. Echap pour quitter.

### Lignes

- `CTRL + x`: Couper la ligne sur laquelle se trouve le curseur
- `MAJ + ALT + flèche hau/bas` : copier la ligne courante ou les lignes sélectionnées vers le haut/bas
- `ALT haut/bas` : déplace la ligne courante ou les lignes sélectionnées vers le haut/bas
- `CTRL + Entrée`: Insérer une ligne en bas
- `CTRL + MAJ + Entrée`: Insérer une ligne en haut

### Commentaires

- `CTRL + :` commentaire de ligne
- `CTRL + MAJ + :` : Commentaire de bloc

### Pliage

- `CTRL + MAJ + )` : Plier la ligne
- `CTRL + MAJ + ^`: Déplier la ligne
- `CTRL + K CTRL + 0` : tout plier
- `CTRL + K CTRL + J` : tout déplier

### Peek editor

- `ALT + F2`: Afficher la définition du symbole dans le peek editor
- `MAJ + F2` Afficher les occurrences du symboles dans le peek editor

### Formatage

- `CTRL + K Ctrl + F` : formater la sélection
- `MAJ + ALT + F` : Formater tous le fichier

## Curseur et sélection

- `ALT + clic` : Insérer un curseur
- `CTRL + ALT + flèche haut/bas`: Placer des curseur au dessus/dessous de la position actuelle
- `Ctrl + Maj + L`: placer un curseur à la fin de chaque occurrence de la sélection
- `CTRL + F2` : placer un curseur sur chaque occurrence du mot courant
- `CTRL + D` : placer un curseur à la fin de occurrence suivante. (Refaire pour une sélection une à une)
- `CTRL + K CTRL + D :` Sauter occurrence suivante
- `CTRL + U` : Annuler la dernière action de curseur
- `Maj + Alt + glissement souris` : permet de faire une selection de colonne de texte
- `CTRL + L` : sélectionner la ligne actuelle

## Recherche

- `CTRL + F`: Rechercher dans le fichier
- `CTRL + H` ! Rechercher et remplacer
- `F3` `MAJ F3` : chercher occurrence suivante/précédente
- `ALT + Entrée` : Sélectionner toutes les occurrences trouvées
