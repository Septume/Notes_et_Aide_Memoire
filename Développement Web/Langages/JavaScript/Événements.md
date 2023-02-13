# Événements

| Événement          | **Correspondance**                                           | **Catégorie**     |
| ------------------ | ------------------------------------------------------------ | ----------------- |
| `click`            | L’utilisateur  a cliqué sur l’élément et a relâché le  bouton  de la souris ou a utilisé un autre dispositif  de  pointage qui émule cette action. | Souris,  pointage |
| `dblclick`         | L’utilisateur  a double-cliqué sur l’élément ou a  utilisé  un autre dispositif de pointage qui émule  cette  action. | Souris,  pointage |
| `mousedown`        | L’utilisateur  a pressé le bouton de la souris ou du  dispositif  de pointage sur l’élément. | Souris,  pointage |
| `mouseup`          | L’utilisateur  a relâché le bouton de la souris ou  du  dispositif de pointage sur l’élément. | Souris,  pointage |
| `mouseover`        | L’utilisateur  a déplacé le curseur de la souris ou  du  dispositif de pointage à l’intérieur des limites  de  l’élément ou d’un de ses descendants. | Souris,  pointage |
| `mouseout`         | L’utilisateur  a déplacé le curseur de la souris ou  du  dispositif de pointage hors des limites de  l’élément. | Souris,  pointage |
| `mousemove`        | L’utilisateur  a effectué un mouvement avec la  souris  ou le dispositif de pointage. | Souris,  pointage |
| `mousewheel`       | L’utilisateur  a actionné la molette de défilement  de  la souris ou du dispositif de pointage  équivalent. | Souris,  pointage |
| `scroll`           | L’élément  qui a fait l’objet d’un défilement.               | Souris,  pointage |
| `select`           | L’utilisateur  a sélectionné du texte.                       | Souris,  pointage |
| `keydown`          | L’utilisateur  a enfoncé une touche.                         | Clavier           |
| `keypress`         | L’utilisateur  a enfoncé une touche correspondant  à  un code caractère. | Clavier           |
| `keyup`            | L’utilisateur  a relâché une touche.                         | Clavier           |
| `dragstart`        | Début  de glisser-déposer.                                   | Drag  & drop      |
| `drag`             | L’utilisateur  est en train de déplacer l’élément.           | Drag  & drop      |
| `dragend`          | L’utilisateur  a fini de déplacer l’élément.                 | Drag  & drop      |
| `drop`             | Fin  de glisser-déposer, et dépôt.                           | Drag  & drop      |
| `dragenter`        | L’opération  de glisser-déposer initiée par  l’utilisateur  est entrée dans l’élément. | Drag  & drop      |
| `dragleave`        | L’opération  de glisser-déposer initiée par  l’utilisateur  a quitté l’élément. | Drag  & drop      |
| `dragover`         | L’opération  de glisser-déposer survole l’élément.           | Drag  & drop      |
| `focus`            | L’élément  a reçu le focus.                                  | Navigation        |
| `blur`             | Perte  du focus : l’élément détenait le focus et l’a  perdu,  car l’utilisateur a navigué vers un autre  élément,  au clavier ou grâce à son dispositif de  pointage. | Navigation        |
| `contextmenu`      | L’utilisateur  a déclenché le menu contextuel.               | Navigation        |
| `show`             | L’utilisateur  a requis l’affichage de l’élément  comme  menu contextuel. | Navigation        |
| `submit`           | Le  formulaire a été validé.                                 | Formulaires       |
| `reset`            | Le  formulaire a été remis à zéro.                           | Formulaires       |
| `change`           | L’utilisateur  a validé le changement de la valeur  d’un  élément (de formulaire). | Formulaires       |
| `input`            | L’utilisateur  a changé la valeur de l’élément de  formulaire. | Formulaires       |
| `formchange`       | L’utilisateur  a validé le changement de valeur  d’un  élément dans le formulaire dont cet élément  dépend. | Formulaires       |
| `forminput`        | L’utilisateur  a modifié la valeur d’un élément  dans  le formulaire dont cet élément dépend. | Formulaires       |
| `invalid`          | L’élément  de formulaire n’a pas respecté les  contraintes  de validation. | Formulaires       |
| `play`             | L’agent  utilisateur a débuté la lecture de  l’élément `<audio>` ou `<video>`. | Médias            |
| `pause`            | L’utilisateur  a mis en pause la lecture de  l’élément `<audio`> ou `<video>`. | Médias            |
| `playing`          | La lecture de l’élément `<audio>` ou` <video>`  a  débuté.   | Médias            |
| `timeupdate`       | La position de lecture de l’élément `<audio>`  ou  `<video>` a changé. | Médias            |
| `ended`            | La  fin de l’audio ou de la vidéo a été atteinte.            | Médias            |
| `emptied`          | L’élément `<audio>` ou `<video>`  est  retourné à son  état  initial. | Médias            |
| `volumechange`     | L’attribut DOM `volume` ou `muted` a été modifié  sur  un élément média. | Médias            |
| `durationchange`   | L’attribut DOM `duration` sur l’élément `<audio>`  ou` <video>` a été modifié. | Médias            |
| `ratechange`       | L’attribut DOM `defaultPlaybackRate` ou  `playbackRate` a été modifié sur l’élément ` <audio>` ou `<video>`. | Médias            |
| `loadedmetadata`   | L’agent  utilisateur a pu déterminer la durée et les  dimensions de l’élément `<audio>` ou` <video>`. | Médias            |
| `progress`         | L’agent  utilisateur télécharge les données médias  pour l’élément` <audio>` ou `<video>`. | Médias            |
| `loadstart`        | L’agent  utilisateur a commencé à charger des  données médias dans l’élément `<audio>`  ou  `<video>`. | Médias            |
| `readystatechange` | L’élément  et toutes ses ressources ont fini leur  chargement. | Médias            |
| `stalled`        | L’agent  utilisateur essaie de télécharger les  données  pour la lecture de l’élément média ` <audio>` ou `<video>`, mais celles-ci ne sont pas  reçues. | Médias            |
| `suspend`        | L’agent  utilisateur ne télécharge actuellement pas  le  contenu du média, mais ne dispose pas encore  de  l’entièreté des données. | Médias            |
| `waiting`        | La lecture de l’élément` <audio>` ou `<video>`  a  été  mise  en pause, car les données nécessaires pour  la  suite sont attendues. | Médias            |
| `canplay`        | L’agent  utilisateur peut reprendre la lecture de  l’audio  ou de la vidéo, mais estime que s’il  débute  à cet instant, la totalité du média ne  pourra  être lue au rythme de lecture actuel sans  avoir  à effectuer d’autre(s) pause(s) pour mettre  en  cache les données. | Médias            |
| `canplaythrough` | L’agent  utilisateur peut reprendre la lecture de  l’audio  ou de la vidéo en estimant qu’à cet  instant  la totalité du média pourra être lue au  rythme  de lecture actuel sans avoir à effectuer  d’autre(s)  pause(s) pour mettre en cache les  données. | Médias            |
| `loadeddata`     | L’agent  utilisateur peut rendre le contenu audio  ou  vidéo à la position de lecture courante, pour la  première  fois. | Médias            |
| `onseeking`        | La valeur de l’attribut `seeking` a été  modifiée à  `true` (l’opération de navigation temporelle sur  l’audio  ou la vidéo a eu lieu et est d’une durée  suffisamment  pertinente pour déclencher  l’événement). | Médias            |
| `seeked`         | La valeur de l’attribut `seeking` a été  modifiée à  `false` (l’opération de navigation temporelle sur  l’audio  ou la vidéo a pris fin). | Médias            |
| `load`           | L’élément  a fini son chargement.                            | Réseau            |
| `abort`          | Chargement  annulé par l’utilisateur.                        | Réseau            |
| `error`          | Le  chargement de l’élément a échoué.                        | Réseau            |

- `abort`
- `autocomplete`
- `autocompleteerror`
- `blur`
- `cancel`
- `canplay`
- `canplaythrough`
- `change`
- `click`
- `close`
- `ctextmenu`
- `cuechange`
- `dblclick`
- `drag`
- `dragend`
- `dragenter`
- `dragexit`
- `dragleave`
- `dragover`
- `dragstart`
- `drop`
- `duratichange`
- `emptied`
- `ended`
- `error`
- `focus`
- `input`
- `invalid`
- `keydown`
- `keypress`
- `keyup`
- `load`
- `loadeddata`
- `loadedmetadata`
- `loadstart`
- `mousedown`
- `mouseenter`
- `mouseleave`
- `mousemove`
- `mouseout`
- `mouseover`
- `mouseup`
- `mousewheel`
- `pause`
- `play`
- `playing`
- `progress`
- `ratechange`
- `reset`
- `resize`
- `scroll`
- `seeked`
- `seeking`
- `select`
- `show`
- `sort`
- `stalled`
- `submit`
- `suspend`
- `timeupdate`
- `toggle`
- `volumechange`
- `waiting`
