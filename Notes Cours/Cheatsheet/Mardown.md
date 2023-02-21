# Markdown

Remarque : Pour utiliser dans le texte des caractères réservés au markdown, il faut d'abord les échapper en utilisant le caractère `\` (Qui lui même doit être échappé)

## Titres

### Syntaxe setext

```md
Titre de niveau 1
=================

Titre de niveau 2
-----------------
```

### Syntaxe atx

```md
# Titre de niveau 1
## Titre de niveau 2
###	Titre de niveau 3
#### Titre de niveau 4
##### Titre de niveau 5
###### Titre de niveau 6
```

## Styles de texte

### Gras

```md
**Texte en gras** 
ou 
__Texte en gras__
```

### Italique

```md
*Texte en italique* 
ou 
_Texte en italique_
```

### Gras et italique

```md
***Texte en gras et italique*** 
ou 
___Texte en gras et italique___
```

### Barré

```md
~~Texte barré~~
```

### Code en ligne

```md
`code`
```

## Blocs de contenu

### Citation

```md
> Lorem ipsum dolor sit amet, consectetuer adipiscing elit 
```

Remarque : on peut imbriquer des citations et utiliser à l'intérieur les autres styles de markdown

### Listes

#### Liste non ordonnée

```md
- item
    - sous item
    - sous item
- item
- item
```

Remarque : On peut également utiliser des `*` ou des `+`

#### Liste ordonnée

```md
1. item 1
   1. sous item 1
   2. sous item 2
2. item 2
3. item 3
```

Remarque : L'ordre des nombres n’a pas d'importante. La sortie HTML produira toujours une liste correctement ordonnée

#### Liste de taches

```md
- [x] terminé
- [ ] non terminé

```

### Bloc de code

<pre><code>
​```javascript
	var link = document.getElementById("link");
​```
</code></pre>

Remarque : on peur également créer un bloc de code avec une indentation de 4 espaces ou une tabulation (Markdown standard)

## Liens

### Liens automatiques

```md
http://exemple.tld
contact@mail.tld
```

### Liens hypertextes

```md
[Texte du lien](http://exemple.tld)
[Texte du lien](path/file.txt)
```

### Liens de référence

```md
[Texte du lien][1]
[Texte du lien][2]

[1]:http://exemple.tld
[2]:http://exemple.tld
```

### Images intégrées

#### Affichage taille réelle

```md
![Texte alternatif](image.png)

```

#### Taille redimensionnée

On précise la largeur (la hauteur est automatiquement calculée pour garder les proportions)

```md
![Texte alternatif|100](image.png)

```

### Échappement des espaces

Pour échapper les espaces :

- Utiliser le code `%20`
- Entourer le nom de la cible avec des `<>`

```md
[Texte du lien](nom%20avec%20espaces)
[Texte du lien](<nom avec espaces>)
```

## Tableaux

```md
| entête                 | entête               | entête               |
| :--------------------- | -------------------: | :------------------: |
| alignement à gauche    | alignement à droite  | alignement au centre |
| ligne 2			     | ligne 2              | ligne 2              |
| ligne 3			     | ligne 3              | ligne 3              |
```

On peut mettre des liens et des images incorporées dans les cellules.

## Autres

### Barre de séparation

```md
-------------------
ou
*******************
```

### Retour à la ligne

Créer deux espaces ou plus à la fin de la ligne  
Ou utiliser la balise `<br>`

### Notes de bas de page (footnotes)

```md
Le HTML ^[HyperText Markup Language] permet de créer des pages Web
```

Un numéro sera automatiquement affiché avec un lien vers la note.Le texte entre crochet sera ajouté en bas de page avec le numéro et un lien de retour

Pour Créer une note de bas de page de plussieurs ligne utiliser plutôt cette syntaxe

```md
Le HTML permet de créer des pages Web [^Note]
```

Et indiquer en fin de page la note (en indentant les lignes à inclure dans la note)

```md
[^Note]: Note de ba de page
	Sur plusieurs ligne
```
