# Éléments interactifs

`<details>` : Permet d’indiquer un contenu ayant pour rôle d’apporter des informations ou détails supplémentaires (Mais non obligatoire pour la compréhension du document ou le fonctionnement de l’application) Par défaut ce contenu est masqué (Il faut cliquer sur une flèche pour l’afficher). Doit avoir pour premier enfant un élément `<summary>` qui permet d’afficher en permanence un résumé du contenu.

- `open` : Attribut booléen. Indique si le contenu est affiché lors du chargement de la page. (Par défaut le contenu est caché)

Remarque : L’évènement `toogle` est déclenché quand l’état de l’élément `<details` change entre ouvert et fermé.

```html
<details>
	<summary>Informations complémentaires</summary>
	<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nemo iste natus veritatis ipsam culpa et consectetur corporis quasi laudantium, atque, iusto amet voluptates. </p>
</details>
```

`<dialog>` : Permet de créer une boite de dialogue

- `open` : Attribut booléen. Permet d'activer la boite de dialogue

Remarque :

- La boite de dialogue doit être associée à du code JavaScript. Les méthodes `showModal()` et `close()` permettent de contrôler l'attribut `open`
- Le pseudo-élément CSS `::backdrop` peut être utilisé pour mettre en forme l'arrière plan du dialogue
- Il est possible de placer un élément `form` dans une boite de dialogue en indiquant l'attribut `method="dialog"`
