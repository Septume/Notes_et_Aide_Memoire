# JSON

Javascript object notation

Format pour l'échange de données sur le Web qui se présente sous forme de chaine de caractères

Avantages :

- Simple
- Très lisible

Inconvénients :

- limité dans les types de données possibles  (pas extensible comme le XML)
- pas de possiblité d'utiliser de commentaire

## Syntaxe

Utilisation de paires de clé/valeur séparées par une virgule  
Les noms de clés sont représentés sous la forme de chaine de caractères et doivent obligatoirement être entourés de guillemets doubles (Contairement aux objets JS)

Les valeurs possibles sont :

- nombre (entier ou décimal)
- chaine de caractères (indiquée avec des guillemets doubles)
- booléen (true ou false)
- tableau (indiqué avec des crochets [])
- objet (indiqué avec des accolades {})
- null (Valeur vide)
	

Attention :

- On doit toujours utilisés des guillemets doubles (et non pas des apostrophes)
- Il n'est pas possible d'utiliser des commentaires JS (Les parsers JSON stricts généreront une exception)

Exemple

```json
{
	"squadName": "Super hero squad",
	"formed": 2016,
	"active": true,
	"members": [
		{
			"name": "Molecule Man",
			"age": 29
		},
		{
			"name": "Madame Uppercut",
			"age": 39
		}
	]
}
```

On peut également utiliser un tableau comme objet JSON valide

```json
[
	{
		"name": "Molecule Man",
		"age": 29,
		"secretIdentity": "Dan Jukes",
		"powers": [
			"Radiation resistance",
			"Turning tiny",
			"Radiation blast"
		]
	},
	{
	"name": "Madame Uppercut",
	"age": 39,
	"secretIdentity": "Jane Wilson",
		"powers": [
		"Million tonne punch",
		"Damage resistance",
		"Superhuman reflexes"
		]
	}
]
```

### Utilisation

Les données JSON doivent être converties en objet JS natif pour être exploitées

  

Notes :

- Convertir une chaîne de caractères en un objet natif =>  analyse syntaxique (parsage)
- Convertir un un objet natif  en chaîne de caractères =>  linéarisation (stringification)
