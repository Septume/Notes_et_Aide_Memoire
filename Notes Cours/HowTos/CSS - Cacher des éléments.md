# CSS - méthodes pour cacher des éléments

`display: none`

- La boite de l'élément n'est pas générée et n'occupe pas d'espace sur la page.
- Le contenu n'est pas actionnable (bouton, ancre,…)
- L'élément n'est pas lu par les lecteurs d'écran

`visibility: hidden`

- La boite de l'élément est générée et occupe un espace sur la page.
- Le contenu n'est pas actionnable
- L'élément n'est pas lu par les lecteurs d'écran

`opacity: 0`

- La boite de l'élément est générée et occupe un espace sur la page.
- Le contenu est actionnable
- L'élément est lu par les lecteurs d'écran
	

`position:absolute` : utiliser de manière à placer l'élément en dehors du viewport pour le rendre non visible

- La boite de l'élément est générée mais n'occupe pas d'espace sur la page car hors du flux normal
- Le contenu est actionnable
- L'élément est lu par les lecteurs d'écran
