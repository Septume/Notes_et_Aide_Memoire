# Tableaux

`<table>` : Pour construire le tableau. Cette balise doit contenir tous les éléments du tableau

`<caption>` : Légende du tableau. Se place avant les autres éléments. (La position de la légende peut être personnalisées avec du CSS). Un seul élément par tableau.

`<tr>` : Table row. Ligne de tableau

`<td>` : Table data. Cellule de tableau

- `colspan` : Pour fusionner des colonnes. La valeur est un entier indiquant le nombre de cellules à fusionner.
- `rowspan` : Pour fusionner des lignes
- `headers` : Pour indiquer la ou les cellules d’ entête `<th>` qui sont liées à l’élément. La valeur est une liste des `id` correspondants, séparés par des espaces.

`<th>` : Cellules d’entête

- `scope` : Pour préciser les cellules auxquelles s’applique l’entête
	- `row` : l’entête s’applique sur toutes les cellules situées sur la même ligne (entête de ligne)
	- `col` : l’entête s’applique sur toutes les cellules situées sur la même colonne (entête de colonne)
	- `rowgroup` : l’entête s’applique sur un groupe de lignes
	- `colgroup` : l’entête s’applique sur un groupe de colonnes
- `abbr` : Contient une description courte et abrégée du contenu à destination des lecteur d’écran
- `colspan`
- `rowspan`

`<thead>` Contient les lignes appartenant à l’entête du tableau. Un seul élément par tableau

`<tbody>` : Contient les lignes appartenant au corps du tableau. Il est possible d’indiquer plusieurs éléments `<tbody>` au sein du même tableau.

`<tfoot>` : Contient les lignes appartenant au pied de tableau. Un seul élément par tableau

`<colgroup>` : Pour indiquer des groupes de colonne. (division structurelle au sein du tableau). Les éléments `<colgoup>` doivent être placés au début avant les éléments `<thead>`, `<tbody>`, `<tfoot>` et `<tr>` et après l’élément `<caption>`s’il est présent.

- `span` : pour indiquer le nombre de colonnes appartenant au groupe. Par défaut `1`. Cet attribut est ignoré si le `<colgroup>` contient des éléments `<col>`

`<col>` : Pour spécifier des attributs communs à l’ensemble des cellules d’une colonne. Utile pour appliquer un ensemble de style à une colonne entière sans devoir répéter l’information sur chaque ligne. Les éléments `<col>` sont en général placés dans un élément `<colgroup>` servant de containeur.

- `span` : pour indiquer le nombre de colonnes consécutives sur lesquelles sont appliqués les attributs communs.

```html
<table>

	<colgroup>
		<!--la première colonne en vert et les 2 suivantes en bleu -->
		<col style="background-color: lightgreen">
		<col span="2" style="background-color: lightblue">
	</colgroup>

	<tr>
		<td>&nbsp;</td>
		<th scope="col">A</th>
		<th scope="col">B</th>
	</tr>

	<tr>
		<th scope="row">1</th>
		<td>A1</td>
		<td>A2</td>
	</tr>

	<tr>
		<th scope="row">2</th>
		<td>B1</td>
		<td>B2</td>
	</tr>

</table>
```
