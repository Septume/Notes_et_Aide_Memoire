### Qu'est ce que Next.js
Next.js est un framework React qui vous permet de créer des sites web statiques et des applications web. Il dispose d’un rendu hybride statique et serveur, d’une prise en charge de TypeScript.

### Pourquoi utiliser Next.js
**"Pourquoi l'équipe de React préfère Next.js"**

Avec React, le navigateur va demander la page au serveur. Le serveur va renvoyer du HTML avec du JS (beaucoup de JS). Le navigateur execute le JS et fait le rendu en HTML.

Next va lire l'application directement sur le serveur et va faire le rendu en HTML directement sur le serveur. Et fournit ce HTML rendu au client pour etre plus rapide.
[Kodaps](https://www.youtube.com/watch?v=_ITJN_dqtEs)

- [`Optimisation d'image`](https://kinsta.com/fr/base-de-connaissances/next-js/#optimisations-dimage)
- [`Internationalisation`](https://kinsta.com/fr/base-de-connaissances/next-js/#internationalisation)
- [`Next.js Analytics` ](https://kinsta.com/fr/base-de-connaissances/next-js/#nextjs-analytics)
- [`Zero Config`](https://kinsta.com/fr/base-de-connaissances/next-js/#zero-config)
- [`Pise en charge intégrée de SSR, SSG et CSR`](https://kinsta.com/fr/base-de-connaissances/next-js/#prise-en-charge-intgre-de-ssr-ssg-et-csr)

### Création d'une application Next.js
Saisir la commande suivante dans le bon dossier où vous voulez placer votre projet Next.js :

En remplaçant le **< project-name >** par le nom réel de votre projet.

```bash
npx create-next-app
// Follow the instructions to create your first Next.js project.
cd <project-name>
npm run dev
```


### Elements Next.js
A la création un nouveau projet Next.js, différents éléments on également été livrés, pages et structures de dossiers. 

##### Structure des dossiers

Après avoir créé un nouveau projet Next.js à partir d’une CLI (Command-line interface), il y a une application Next.js avec une arborescence de dossiers allégée. Cette structure de dossiers par défaut est le strict minimum pour faire fonctionner une application Next.js.

Les seuls dossiers spécifiques à Next.js sont les dossiers **pages**, **public** et **styles**. <span style="color: red"><u>Ceux-ci ne doivent pas être renommés</u></span>, sauf si vous êtes prêt à ajuster des configurations supplémentaires.

Voici la structure de dossiers par défaut pour un nouveau projet Next.js :

```jsx 
# other files and folders, .gitignore, package.json...
- pages
  - api
    - hello.js
  - _app.js
  - index.js
- public
  - favicon.ico
  - vercel.svg
- styles
  - globals.css
  - Home.module.css
```


##### Pages

Les pages sont l’un des dossiers spécifiques à Next.js. Ce sont des composants React, et chacun des fichiers du dossier Pages est une page web. 
Chaque page web est un composant React. Par exemple, nous avons un composant React dans le dossier **Pages**, ce qui donne une URL de page web.

```jsx
// Location: /pages/index.js
//  is just a basic React component
export default Index() {
  return <h1>Welcome to Home</h1>
}
```

Next.js est livré avec des pages personnalisées pré-créées, préfixées par des underscores, telles que `_app.js` et `_document.js`. 
Next.js utilise le composant de page personnalisée `_app.js` pour initialiser les pages. Il réside dans le dossier `pages`, tandis que le composant de page personnalisée `_document.js` complète les balises `<html>` et `<body>` de votre application.

Le framework utilise également un système de routage basé sur les pages, dans lequel chaque page devient automatiquement une route en fonction de son nom de fichier. Par exemple, une page à `pages/user` sera située à `/user`, et `pages/index.js` à `/`.