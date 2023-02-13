# CSS - contexte d'empilement et z-index

### contexte d'empilement

Un nouveau contexte d'empilement est créé dans les cas suivants

- `position: relative` ou `position: absolute` et un `z-index` différent de `auto`  
- `position: fixed` ou `position: sticky`
- Un élément `flex item` ou `grid item` (c.a.d. un élément qui est enfant d'un container `flex` ou `grid`) avec un `z-index` différent de `auto`
- Élément qui a une propriété `opacity` inférieur à 1
- Élément pour lequel n'importe laquelle de ces propriétés est différent de `none`
	- `transform`
	- `filter`
	- `perspective`
	- `clip-path`
	- `mask`
	- `mix-blend-mode`

A noter que l'élément `html` créé un contexte d'empilement de base

### Fonctionnement du z-index

Pour qu'un élément puisse avoir un z-index

- Il doit avoir une position autre que `static`
- Ou il doit être un enfant d'un élément `flex` ou `grid`

Les valeurs les plus élevés sont au premier plan et les plus faibles au second plan. Ainsi un `z-index` de 2 sera placé au dessus d'un `z-index` de 1, et un `z-index` de -1 sera placé au dessus d'un `z-index` de -2.  

**Attention : La portée d'un z-index est limité à son contexte d'empilement = contexte  local**  

Cela signifie qu'un z-index situé en dehors du contexte n'aura aucun impact sur le positionnement des éléments enfants du contexte local
