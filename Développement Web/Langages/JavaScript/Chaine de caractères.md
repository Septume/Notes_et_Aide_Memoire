# Chaine de caractères

## Créer une chaine de caractères

Les chaines doivent être délimitées par des apostrophes ou des guillemets

```jsx
let chaine1 = "chaine de caractères"
let chaine2 = 'une autre chaine';
```

Caractères d'échappement :

- `\`
- `\n` (nouvelle ligne)
- `\t` (tabulation)
- `\r` (retour chariot)

Pour comparer deux chaînes on utilise l'opérateur de comparaison `===`

```jsx
let chaine1 = "bonjour";
let chaine2 = "Bonjour";

console.log (chaine1 === chaine2); // false
```

L'opérateur `+` permet de concaténer des chaines entre elles ou avec un nombre

La propriété `length` permet de retournée la longueur d'une chaine

```jsx
let chaine = "bonjour"
console.log("Il y a " + chaine.length + " lettres dans le mot " + chaine);
// "Il y a 7 lettres dans le mot bonjour"
```

Pour parcourir une chaine on utilise une boucle for classique

```jsx
var chaine = "bonjour"
for (let i = 0; i < chaine.length; i++){
  console.log(chaine[i]);
}
```

## Template literals (spécification es6)

Ou "*template strings*"

Permettent d’insérer du code JavaScript dans n’importe quelle chaine de caractères. Pour cela on utilise :

- des accents graves pour délimiter lac chaine de caractères
- Un bloc `${}` pour y intégrer le code JS

Les tremplates strings permettent également de conserver les retour à la ligne ce qui permet d'utliser des chaines de caractères multiligne. Cela peut être utile lorsqu'on doit utiliser des chaines de caractères contenant du code HTML à injecter.

```jsx
let username = "toto"; 
console.log(`Bonjour ${username}`);
```

## **Méthodes pour les chaines**

`toUpperCase()` : Retourne la chaine en majuscule

`toLowerCase()`: Retourne la chaine en minuscule

`charAt(indice)` : Retourne le caractère situé à l'indice indiquée

`trim()` : Retourne la chaine où les blancs (espaces, tabulation et caractères de fin de ligne) avant et après la chaine sont supprimés

`indexOf(sousChaine, indice)` : Retourne l'indice du premier caractère de la première occurrence de la sous chaîne trouvée. Retourne -1 si la sous-chaîne n'existe pas. le second argument est facultatif et permet de faire une recherche uniquement à partir de l'indice donnée.

`lastIndexOf(sousChaine, indice)` : Retourne l'indice du premier caractère de la dernière occurrence de la sous chaîne trouvée

`substring(indiceA, indiceB`) : Retourne une sous-chaîne de l'indice A (inclus) à l'indice B (exclus). Si on n'indique pas l'indice B, la recherche se fera jusqu'à la fin de la chaîne

`slice(indiceA, indiceB)` : Retourne une sous-chaîne de l'indice A (inclus) à l'indice B (exclus). Accepte les indice négatifs en paramètres. Dans ce cas le comptage commence à la fin. (-1 correspondant au dernier caractère)

`substr(indice, longueur)` : Retourne une sous-chaîne de x caractères. Le premier paramètre correspond à l'indice de début et le deuxième au nombre de caractère à extraire.

`split(séparateur, nombreMax)` : Permet de couper une chaîne de caractère selon un séparateur et retourne les sous-chaînes résultantes dans un tableau. Le séparateur étant un caractère ou une série de caractères. Si le séparateur est une chaine vide (`""`) c'est un tableau de caractères qui est retourné. Le deuxième argument est facultatif et permet de retourner dans un tableau qu'un nombre max de chaînes.

`replace(sousChaine, nouvelleSousChaine)` : Remplace une sous chaîne par une autre

`includes(sousChaine, indice)` : Recherche si la sous- chaîne est présente et renvoie true si c'est le cas, sinon false. le deuxième paramètre est facultatif et permet de faire une recherche uniquement à partir de l'indice donné.

```jsx
let chaine = " BONJOUR   ";
chaine = chaine.trim().toLowerCase();
console.log(chaine); // "bonjour"
```

## Encodage des caractères spéciaux

Deux fonctions permet de gérer les caractères spéciaux dans les chaines

`encodeURIComponent()` : Prend comme argument une chaine et la retourne encodée

`decodeURIComponent()` : Réalise l'opération inverse

L'encodage doit être utilisé notament lors de l'envoie de données au serveur

```jsx
console.log(encodeURIComponent("Hello World")); // "Hello%20World"
```
