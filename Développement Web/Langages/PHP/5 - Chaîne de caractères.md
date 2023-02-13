# Chaîne de caractères

```php
$variable = "chaine de caractère";
echo $variable; 
```

Remarque : on peut aussi utiliser des guillemets simples

### Concaténation

```php
$variable= 20;
echo "Le visiteur a $variable ans"; 
```

Attention si on veut utiliser des guillemets simples il faut écrire :

```php
echo 'Le visiteur a ' . $variable . ' ans'; 
```

Remarque : il est préférable d’utiliser les guillemets simple pour écrire des chaines de caractères et d’utiliser la deuxième méthode de concaténation

### Fonctions sur les chaînes

- `strlen(chaine)` : retourne la longueur d’une chaine de caractère
- `str_replace('souschaine', 'nvSousChaine',chaine)`: remplacer des caractères par d’autre dans un chaine. Retourne la nouvelle chaine
- `strireplace()` : idem mais sans prendre en compte la case
- `strtolower(chaine)` : retourne la chaine en minuscule
- `strtoupper(chaine)` : retourne la chaine en majuscule
- `ucfirst(chaine)` : premier caractère de la chaine en majuscule
- `lcfirst(chaine)` : premier caractère de la chaine en minuscule
- `ucwords(chaine)` : premier caractère de chaque mot en majuscule
- `strpos(chaine, 'souschaine')` : retourne la position d’une sous-chaine ou false si non trouvé . Peut prendre en 3ème argument la position à partir de laquelle faire la recherche
- `stripos()` : similaire à `strpos()` mais ne prend pas en compte la case
- `strrpos()` : recherche de droite à gauche
- `strripos()` : recherche de droite à gauche et ne prend pas en compte la case
- `strspn($chaine, $masque)` : retourne la longueur de la première sous-chaine contenant les caractères spécifiés par le masque
- `strcpn(chaine, masque)` : retourne la longueur de la première sous-chaine ne contenant pas les caractères spécifiés par le masque
- `substr(chaine, index)` : soustrait une sous-chaine à partir de l’index indiqué. Si on indique un index négatif, on commence à partir de la fin de la chaine (-1 correspond au dernier caractère). On peut indiquer en 3ème argument un entier indiquant la longueur de la chaine à soustraire.
- `str_repeat(chaine, entier)` : permet de construire une chaine par répétition de caractères. prend en argument une chaine indiquant les caractères à répéter et un entier pour le nombre de répétition
- `strstr(chaine1, chaine2)` : recherche dans chaine1, la premier occurrence de chaine2. retourne une chaine contenant chaine2 et la suite de chaine1 ou false si non trouvé. Peut prendre en 3ème argument `true` pour indiquer que la fonction doit retourner la chaine qui se situe avant la chaine recherchée
- `stristr()` : idem mais sans prendre en compte la case
- `strrchr(chaine, caract)` : cherche dans une chaine la dernière occurrence d’un caractère et retourne la sous-chaine commençant à cette occurrence ou false si non trouvé. Sensible à la case
- `trim(chaine)` : supprime les caractères blancs avant et après la chaine
- `ltrim(chaine)` : supprime les caractères blancs avant la chaine
- `rtrim(chaine)` : supprime les caractères blancs après la chaine
- `strcmp(chaine1, chaine2)` : comparaison de deux chaines. Retourne un entier négatif si chaine1 < chaine2, un nombre positif si chaine1 > chaine2 ou 0 si elles sont égales
- `strcasecmp(chaine, chaine2)` : même chose mais en ne prenant pas en compte la case
- `str_word_count(chaine)` : retourne le nombre de mot d’une chaine. On peut indiquer comme deuxième argument `true`. Dans ce cas les mots sont retournés dans un tableau
