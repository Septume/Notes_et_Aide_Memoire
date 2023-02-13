# URI

⇒ Uniform Resource Identifier
Permet d'identifier (de manière permanente) une ressource physique ou abstraite sur un réseau.

## Types d' URI

Un URI peut être de type *locator*, *name* ou les deux.

### URL (Uniform Ressource Locator)
En plus de l'identification, permet de localiser la ressource ainsi que les moyens d'accès

Exemple
```
<http://example.com>
ftp://ftp.example.com/pub/
mailto:admin@example.com
```


### URN (Uniform Ressource Name)
Identification d'une ressource par son nom dans un espace de noms

Exemple
```
urn:uuid:6d63842b-deb8-4093-9357-09deac3d0de6
urn:isbn:0-395-36341-1 //référence à un livre via son numéro ISBN
```

## Format d'une URI

`<nom du schéma> : <partie hiérarchique> [ ? <requête> ] [ # <fragment>]`

- **Nom du schéma**: Obligatoire. Indique le schéma d'URI sera utilisé. (Par exemple : http, urn, tel, dns, data)
- **Partie hiérarchique**: Obligatoire. Permet d'identifier la ressource
- **Requête**: Facultatif. Précédé d'un point d'interrogation. Permet d'indiquer des informations supplémentaires
- **Fragment**: Facultatif. Précédé d'un dièse. Informations permettant d'accéder à une sous-partie de la ressource