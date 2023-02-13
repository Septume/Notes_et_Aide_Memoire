# Contexte de navigation

Chaque contexte de navigation possède son propre historique et son propre document actif

Valeurs à utiliser avec l'attribut `target` des éléments `link`, `a`, `area` et `form`

- `_self` : contexte courant (Défaut)
- `_blank` : nouveau contexte
- `_parent` : contexte parent (ou contexte courant s’il n’y a pas de parent).
- `_top` : contexte ancêtre de premier niveau (ou contexte courant s’il n’y a pas de parent).
- Contexte de navigation personnalisé : Il est possible d'utiliser un nom d'iframe (attribut `name` de l'élément `iframe`) comme valeur de l’attribut `target` d’un élément `a` ou `form` ou comme valeur de l’attribut `formtarget` d’un élément `input` ou `button`
