# **Referrer policy**

Politique concernant le referrer envoyé lors d'une requête HTTP

## Fonctionnement

`Referer` : Entête HTTP de requête qui contient l'URL de la page précédente qui a permis à l'utilisateur d'accéder à la page courante en suivant un lien. (Remarque : Normalement le mot s'écrit avec deux "r". Il s'agit d'une faute d'orthographe qui a été faite lors de la standardisation et qui est restée)

`Referrer-Policy` : Entête HTTP de réponse qui permet de définir la politique concernant le referrer (Remarque : ici le nom doit être correctement orthographié avec deux "r")

- `no-referrer-when-downgrade` : Défaut. Le referrer n'est pas envoyé lorsque la destination est moins sécurisée. (C'est à dire, si la page de destination est en http alors que la page d'origine est en https)
- `no-referrer` : Le referrer n'est pas envoyé.
- `origin` : Envoie uniquement l'origine. ( Par exemple : `https://example.com/dir/` => envoi de l'URL `https://example.com`)
- `origin-when-cross-origin` : Envoie l'URL complète si la destination a la même origine ou seulement l'origine pour les autres cas.
- `same-origin`: le referrer sera envoyé uniquement si la destination est de la même origine
- `strict-origin-when-cross-origin` : Même chose que `origin-when-cross-origin` sauf que le referrer ne sera pas envoyé si la destination est moins sécurisée
- `strict-origin` : Même chose `same-origin` sauf que le referrer ne sera pas envoyé si la destination est moins sécurisée
- `unsafe-url` : L'URL complète sera envoyée dans tout les cas

Remarque : Deux URLs ont la même origine s'ils utilisent le même protocole, le même hôte et le même port

Afin d'éviter la divulgation d’informations sensibles, il est recommandé d'utiliser les valeurs :

- `no-referrer`
- `same-origin`
- `strict-origin`
- `strict-origin-when-cross-origin`

Exemple de pages sensibles : admin, réinitialisation de mot de passe, intranet

## Utilisation

### Avec apache

Dans la configuration générale

```
 Header always set Referrer-Policy "strict-origin-when-cross-origin"
```

Via un fichier .htaccess

```
 <IfModule headers_module.c>
 Header always set Referrer-Policy "strict-origin-when-cross-origin"
 </IfModule>
```

### Intégration avec HTML

Règle concernant le document entier : On utilise une balise `<meta>`

```html
 <meta name="referrer" content="origin">
```

Règle spécifique pour un élement `a`, `area`, `img`, `iframe`, `script` ou `link` : On utilise l'attribut `referrerpolicy`

```html
 <a href="http://example.com" referrerpolicy="origin">
```

Comme alternative, on peut également indiquer une relation `noreferrer` sur un élement `a`, `area` ou `link`

```html
 <a href="http://example.com" rel="noreferrer">
 
```