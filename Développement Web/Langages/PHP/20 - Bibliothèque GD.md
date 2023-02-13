# Bibliothèque gd

Permet de créer des images. Il faut activer `gd2` pour l’utiliser

### Renvoyer une image au navigateur

Il faut modifier le header pour que PHP renvoi une image à la place d’une page Web

On indique en début de fichier le header :

`header ("Content-type: image/png")` ou `header ("Content-type: image/jpeg")`

Il est possible d’afficher cette image sur une autre page avec `<img src="image.php" />`

### Créer une image

À partir d’une image vide : `imagecreate(largeur, hauteur)`

À partir d’une image JPEG : `imagecreatefromjpeg(nom_fichier)`

À partir d’une image PNG`imagecreatefrompng(nom_fichier)`

Ces fonctions retournent une nouvelle image

Exemple

```php
// image vide de 200x50 pixels
$image = imagecreate(200,50)

// a partir d'un jpeg 
$photo = imagecreatefromjpeg("photo.jpg");
```

### Afficher l’image

pour une image JPEG : `imagejpeg(image)`

Pour une image PNG : `imagepng(image)`

```php
header ("Content-type: image/jpeg");
$photo = imagecreatefromjpeg("photo.jpg");
imagejpeg($photo);
```

### Enregistrer l’image

Dans ce cas on n’a pas besoin de modifier le header pour renvoyer une image. On utilise les mêmes fonctions que pour l’affichage mais en indiquant en deuxième paramètre le dossier où sera stocké l’image

```php
$photo = imagecreatefromjpeg("photo.jpg");
imagejpeg($photo, 'gallerie/photo.jpg');
```

### Redimensionner une image

On utilise la fonction `imagecopyresampled()`

Prend en paramètre :

- l’image de destination
- l’image source
- l’abscisse de la destination. Pour une miniature on met 0
- l’ordonnée de la destination. Pour une miniature on met 0
- l’abscisse de la source. Pour une miniature on met 0
- l’ordonnée de la source. Pour une miniature on met 0
- largeur de la destination
- hauteur de la destination
- largeur de la source
- hauteur de la source

Pour obtenir les dimension d’une image :

- `imagesx(image)` : renvoie la largeur
- `imagey(image)` : renvoie la hauteur

### Texte, couleur et transparence

`imagecolorallocate(image, R,V,B)` : changer la couleur de fond. Prend en argument la référence vers une image et un code couleur R, V et B (entre 0 et 255) . On peut également utiliser cette fonction pour stocker une couleur dans une variable

`imagestring(image, taille, x, y, chaine, couleur)` : insère une chaine de caractère. Il faut indiquer :

- une taille de police entre 0 et 5
- les coordonnées x et y (0,0 correspond au coin supérieur gauche)
- la couleur de la chaine créée avec la fonction `imagecolorallocate()`

`imagecolortransparent(image, couleur)` : pour créer de la transparence. Pour les image PNG seulement

```php
header ("Content-type: image/png");
$image = imagecreate(200, 200);
$bg_color = imagecolorallocate($image,248,161,164);
$str_color = imagecolorallocate($image, 63,73,164);
imagestring($image, 5, 20, 100, 'Hello World !', $str_color);
imagecolortransparent($image, $bg_color);
imagepng($image);
```
