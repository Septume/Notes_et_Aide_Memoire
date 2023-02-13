# Constantes

Les constantes sont accessibles dans tout le script, y compris les fonctions. Par convention, le nom est en majuscule

### Créer une constante

`define(NOM_CONST, valeur_const)`

ou

`const NOM_CONST = valeur`

```php
define('HELLO', 'Hello World !');
echo HELLO;
```

- fonction `define()` : la constante peut être définie via des valeurs littérales, des expressions, des variables ou des appels de fonctions. La fonction retourne un booléen pour indiquer le succès ou l’échec de la création de la constante.
- instruction `const` : on ne peut pas utiliser des variables ou des appels de fonctions pour définir la constante. Par contre cette instruction peut être utilisée dans les classes

Conseilcréer un fichier contenant que des constantes pour gérer les paramètres de configuration du site de manière centralisée

### Fonctions pour les constantes

`defined(NOM_CONST)` : teste si la constante indiquée en argument est définie

`constant(NOM_CONST)` : retourne la valeur de la constante indiquée en argument

### Constantes magiques

- `__FILE__` : chemin complet du fichier
- `__DIR__` : nom du dossier dans lequel est le fichier
- `__LINE__` : le numéro de la ligne actuellement utilisée dans le fichier
- `__FUNCTION__` : le nom de la fonction actuellement définie
- `__CLASS__` : le nom de la classe actuellement définie
- `__METHOD__` : le nom de la méthode actuellement utilisée
- `__NAMESPACE__` : le nom de l’espace de noms ( namespace) courant
- `__TRAIT__` : le nom du trait (incluant le nom de l’espace de noms dans lequel il a été déclaré)
