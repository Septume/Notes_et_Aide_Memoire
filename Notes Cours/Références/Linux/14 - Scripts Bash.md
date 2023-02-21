# Scripts bash

## **Variables**

`nomVariable = valeur`

`echo $nomVariable`

Initialiser une variable avec une valeur vide :

`nomVariable=""`

Supprimer une variable :

`unset nomVariable`

Le caractère `$` indique qu'il faut substituer le nom de la variable par sa valeur. Il s'agit d'une forme simplifiée. La forme complète (qui utilise des accolades) est :

`${nomVariable}`

La forme complète doit être utilisée si on souhaite ajouter des caractères à la valeur

Exemple

```
 $ number=10
 $ echo ${number}1
 101
```

On peut affecter comme valeur le résultat d'une commande

`rep=$(pwd)`

`echo $rep`
