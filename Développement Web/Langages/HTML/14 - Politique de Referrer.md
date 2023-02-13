# Politique de referrer

Attribut `referrerpolicy` des éléments `link`, `img`, `area` , `iframe` et `script`

- `no-referrer-when-downgrade` : Le referrer est envoyé uniquement si la destination n’est pas moins sécurisée. (C’est à dire, si la page de destination est en http alors que la page d’origine est en https). Il s’agit du comportement par défaut du navigateur si aucune règle est indiquée.
- `no-referrer` : Le referrer n’est pas envoyé.
- `origin` : Envoie uniquement l’origine. ( Par exemple : `https://example.com/dir/` => envoi de l’URL `https://example.com`)
- `origin-when-cross-origin` : Envoie l’URL complète si la destination a la même origine ou seulement l’origine pour les autres cas.
- `same-origin`: le referrer sera envoyé uniquement si la destination est de la même origine
- `strict-origin-when-cross-origin` : Même chose que `origin-when-cross-origin` sauf que le referrer ne sera pas envoyé si la destination est moins sécurisée
- `strict-origin` : Même chose que `same-origin` sauf que le referrer ne sera pas envoyé si la destination est moins sécurisée
- `unsafe-url` : L’URL complète sera envoyée dans tout les cas
