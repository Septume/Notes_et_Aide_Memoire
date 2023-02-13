# Structure de contrôle

### Opérateurs

### Opérateurs de comparaison

`==`

`===`

`>`

`>=`

`<`

`<=`

`!=`

`!==`

### Opérateurs logique

- `AND` ou `&&`
- `OR` ou `||`
- ``!`

### Conditions

### Structure if…else

```php
if (CONDITION) {
    instructions;
} elseif (CONDITION) {
    instruction; 
} else {
    instruction; 
} 
```

Syntaxe avec code HTML inclus

```php
<?php if (CONDITION): ?>
    CODE HTML
<?php elseif (CONDITION): ?>
    CODE HTML 
<?php else: ?>
    CODE HTML
<?php endif; ?>
```

### Switch

```php
switch ($variable){
case valeur1: 
    instructions; 
    break;
case valeur2: 
    instructions;
    break;
default:
    instructions; 
}
```

Syntaxe avec code HTML inclus

```php
<?php switch ($variable): 
    case valeur1: ?>
        CODE HTML
    <?php case valeur2: ?>
        CODE HTML
    <?php default: ?>
        CODE HTML
<?php endswitch; ?>
```

### Ternaire

`$variable = (condition) ? valeur : valeur`

Si la condition est vrai : la valeur se trouvant après le " ?" est affectée

Si elle est fausse : la valeur se trouvant après le " : " est affectée

### Test null

`$variable = valeur1 ?? valeur2 ?? valeur3 ?? …`

Retourne la première valeur qui est non `NULL`

### Comparaison combinée

`$variable = valeur1 <=> valeur2`

Retourne :

- `1` si valeur1 < valeur2
- `0` si valeur1 = valeur2
- `1` si valeur1 > valeur2

### Boucle

### While

```php
while (CONDITION)  {
    instructions; 
}
```

Syntaxe avec code HTML inclus

```php
<?php while (CONDITION): ?>
    CODE HTML
<?php endwhile; ?>
```

### Do…while

une seule syntaxe est disponible

```php
do {
    // instructions;
} while (CONDITION);

```

### For

```php
for ( INITIALISATION; CONDITION; INCREMENTATION) {
    // instructions; 
}
```

Syntaxe avec code HTML

```php
<?php for ( INITIALISATION; CONDITION; INCREMENTATION): ?>
    CODE HTML
<?php endfor; ?>
```

### Instructions d’arrêt

`break` : sortir d’une structure de contrôle

`continue` : ne pas exécuter les instructions suivantes de l’itération courante et pas à itération suivante
