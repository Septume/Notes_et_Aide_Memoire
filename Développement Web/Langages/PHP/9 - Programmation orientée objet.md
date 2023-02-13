# Programmation orientée objet

### Créer et instancier une classe

```php
class NomClasse {
	private $propriete1; 
	private $propriete2;
	….
	public function methode(parm){}

}
```

Par convention le nom de la classe doit commencer par une majuscule

Il est recommandé de mettre une classe par fichier dont le nom doit être celui de la classe. On peut également utiliser extension *.class.php*

Instancier un objet : `$objet = new NomClasse();`

Appel de méthode`$objet->methode(arg)`

Accéder à une propriété : `$objet->propriete`(Remarque : on ne doit pas mettre le $)

mot clé `$this` : fait référence à la classe en cours

```php
lass Personne {

    private $nom = 'Dupont';
    private $prenom = 'Jean';
    private $age = 40;

    public function decrirePersonne(){
        return 'nom: ' . $this->nom . ', prénom: '. $this->prenom . ', age: ' . $this->age; 
    }
}

$personne = new Personne();
echo $personne->decrirePersonne();
```

### Droits d’accès

`private` : l’ élément est accessible uniquement dans la classe

`public` : l’élément est accessible à l’extérieur de la classe

`rpotected` : l’élément est accessible dans les classes enfants

En général les propriétés sont en `private` et les méthodes en `public`

Il faut toujours indiquer les droits d’accès pour les propriétés. Pour les méthodes, si le droit d’accès n’est pas spécifié, celui ci est par défaut `public`

### Constructeur

un constructeur par défaut est appelé lorsqu’on créé un objet avec `new`

Il est possible de créer son propre constructeur afin de passer en argument les valeurs des propriétés de l’objet

Le constructeur est toujours nommé `__construct` et ne possède pas de return

```php
class Personne {
    private $nom;
    private $prenom;
    private $age;

    public function __construct($nom, $prenom, $age){
        $this->nom = $nom;
        $this->prenom = $prenom; 
        $this->age = $age;
    }

    public function decrirePersonne(){
        return 'nom: ' . $this->nom . ', prénom: '. $this->prenom . ', age: ' . $this->age; 
    }
}

$personne = new Personne('Dupont', 'Jean', 40);
echo $personne->decrirePersonne();
```

### Méthodes et propriétés statiques

Pour appeler une propriété ou une méthode sans avoir besoin d’instancier un objet on utilise le mot clé `static`

```
class NomClasse {
    private static $propriete; 
    public  static function methode(parm){}

}

NomClasse::propriete
NomClasse::methode(args)

```

Remarque : on peut utiliser une propriété ou une méthode statiques au sein de la même classe. Dans ce cas on utilise le mot clé `self` qui fait référence au nom de la classe

```
self::propriete
self::methode(args)
```

### Héritage

`class NomSousClasse extends NomSuperClasse {}`

la sous classe

- hérite des propriétés et des méthodes de son parent
- peut redéfinir ces propriétés et méthodes
- peut définir ses propres propriétés et méthodes

### Namespace

Permet d’éviter les conflits de nom de classe en cas d’utilisation de bibliothèque tierces. Deux classes peuvent avoir le même nom si elle sont dans un namespace différent

On indique le namespace avant la déclaration d’une classe :

`namespace NomNameSpace\Section\SousSection`

Le namespace doit être ajouté en préfixe du constructeur

`$objet = new \NomNameSpace\Section\SousSection\NomClasse()`

Pour un classe qui appartient au namespace global (racine) :

`$objet = new \NomClasse()`

Pour ne pas avoir besoin d’indiquer le préfixe on peut utiliser le mot clé `use` en début de fichier pour indiquer les namespaces à utiliser

`use \NomNameSpace\Section\SousSection\NomClasse`

**Attention : cette technique ne fonctionne pas si on utilise deux classes pourtant le même nom** . Il faut aussi créer un alias avec un nom unique en utilisant le mot clé `as`

`use \NomNameSpace\Section\SousSection\NomClasse as NomAlias`

`$objet = new NomAlias()`

La constante `__NAMESPACE__` permet d’obtenir l’espace de nom courant

Remarque :

- plusieurs espaces de nom peuvent être définies dans le même fichier mais ce n’est pas une bonne pratique
- on peut aussi utiliser les namespaces avec les fonctions et les constantes

### Classe et méthode abstraite

Classe abstraite : classe ne pouvant pas être instanciée. sert de base à la définition de classe fille.

Méthode abstraite : définie obligatoirement dans une classe abstraite. Il s’agit d’une méthode non implémentée c’est-à-dire que le code n’est pas présent. la méthode sera implémentée dans la classe fille. Une classe fille qui n’implémente pas toutes les méthodes abstraites de la classe mère est implicitement abstraite

```php
abstract class NomClasse {
    abstract public function nomMethode(); 
}
```

### Classe et méthode finale

Classe finale : classe dont on ne peut hériter.

Méthode finale : ne peut pas être redéfini dans une classe fille

```php
final class NomClasse {}
```

### Interface

Classe qui ne contient que des méthodes sans implémentation et pas d’attributs

les méthodes sont obligatoirement `public` (le mot clé peut être omis)

```php
interface nomInterface {
    public function nomMethode()
}
```

On peut ensuite définir une nouvelle classe qui implémente une interface

`class NomClasse implements NomInterface {}`

=> si une seule méthode de l’interface n’est pas implémentée, la classe sera abstraite

### Trait

sorte de classe qui regroupe un ensemble d’attribut et e méthode pouvant ensuite être utilisée dans une autre classe sans héritage

```php
trait nomTrait {
    private static $propriete; 
    public  static function methode(parm){}

}
```

utilisation des traits dans une classe

`class NomClasse { use nomTrait1, nomTrait2, …` `}`
