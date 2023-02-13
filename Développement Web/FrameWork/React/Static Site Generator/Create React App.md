Également créé par les équipes de Facebook, [Create React App](https://github.com/facebook/create-react-app) est un outil qui aide à créer et installer les bases essentielles au démarrage.

### Installez et lancez CRA
```bash
npx create-react-app la-maison-jungle
```

### Découvrir les fichiers
Vous trouverez trois dossiers 📁:

-   `node_modules`  : c’est là que sont installées toutes les **dépendances** de notre code. Ce dossier peut vite devenir très volumineux.
    
-   `public`  : dans ce dossier, vous trouverez votre **fichier `index.html`** et d’autres fichiers relatifs au référencement web de votre page.
    
-   `src`  : vous venez de rentrer dans le cœur de l’action. **L’essentiel des fichiers que vous créerez et modifierez seront là**.

Et faisons maintenant un petit tour des fichiers importants 👀 :

-   `package.json`  : situé à la racine de votre projet, il vous permet de **gérer vos dépendances** (tous les outils permettant de construire votre projet), vos scripts qui peuvent être exécutés avec `yarn`, etc. Si vous examinez son contenu, vous pouvez voir des dépendances que vous connaissez : React et ReactDOM :
    
    -   vous y trouverez `react-scripts`, créé par Facebook,  qui permet d’installer Webpack, Babel, ESLint et d’autres pour vous faciliter la vie ;
        
-   dans `/public`, vous trouvez `index.html`. Il s'agit du **template de votre application**. Il y a plein de lignes de code, mais vous remarquez `<div id="root"></div>` ? Comme dans les chapitres précédents, nous allons y ancrer notre app React ;
    
-   dans  `/src`, il y a  `index.js`  qui permet d’**initialiser notre app React** ;
    
-   et enfin, dans  `/src`, vous trouvez  `App.js`  qui est **notre premier composant React**.
    

Je vois  `dependencies`  et  `devDependencies`. Mais c'est quoi la différence entre les deux ?  
En fait, les  `dependencies`  sont des dépendances qui sont nécessaires à notre code pour fonctionner, aussi bien en local qu'en production. En revanche, les  `devDependencies`   sont uniquement nécessaires pour la phase de développement. Les deux sont installées depuis votre _package manager,_ pour nous `yarn`, en précisant une option différente : `yarn add`  pour les `dependencies`, et  `yarn add --dev`   pour les  `devDependencies`.

Deux fichiers que nous n'utiliserons pas directement mais qui ne font pas de mal à garder :

-   le `README.md`   qui permet d’afficher une page d’explication si vous mettez votre code sur GitHub, par exemple ;
    
-   et le fichier `.gitignore`   qui précise ce qui ne doit pas être mis sur GitHub, typiquement le volumineux dossier des `node_modules`.
    

La base de code qui a été initialisée avec Create React App contient du code et des outils qui ne seront pas exploités dans ce cours, notamment tout ce qui concerne la partie de tests. Les fichiers que je n’ai pas mentionnés au-dessus, vous pouvez les supprimer. Ça vous permettra de garder ce qui est essentiel.

#### Prenez en main votre app avec les commandes

Lorsque vous vous trouvez à la racine de votre projet, vous pouvez exécuter `yarn start`   qui va **démarrer votre application en mode développement**.

Cela vous donne quelque chose comme ça (même si votre adresse IP sera très probablement différente) :

![La console montre que l'application a bien compilé (Compiled successfully!), c'est-à-dire que l'application a démarré.](https://user.oc-static.com/upload/2021/01/14/16105925124955_image16.png)

Un onglet a dû s'ouvrir dans votre navigateur à l'URL[`http://localhost:3000/`](http://localhost:3000/). Si ce n'est pas le cas, ouvrez-le vous-même.

Et tadaa ! 🎉🎉🎉  
Vous avez le magnifique logo de React qui tourne dans votre navigateur !

```
Il existe d'autres commandes :

-   `yarn run build`   vous permettra de créer un `build`  avec votre code transformé et minifié, si vous devez déployer votre application en production (la mettre en ligne, par exemple) ;
    
-   `yarn test`  pour exécuter les tests.
    

Vous pouvez d'ailleurs créer vos propres commandes si vous les ajoutez dans la partie `scripts`.
```

### Organisez votre code

Nous allons maintenant **modifier notre base de code** pour qu'elle soit plus à l'image de notre projet. Il existe plusieurs manières d'organiser son code, et il est important de réfléchir à comment l'organiser. Ici, nous allons séparer les fichiers selon leur type : composants/style/images, etc.

On va commencer par créer un dossier  `/components`   dans `/src`, où nous mettrons tous nos composants. On y glisse  `App.js`   et on en profite pour changer le chemin d'import dans  `index.js`. Pour ce qui est des autres fichiers, le plus important est `index.js` que vous devez garder. Vous pouvez également garder`index.css`,  mais vous pouvez supprimer les autres fichiers.

Maintenant, **créons notre `Banner`**  du chapitre précédent dans un fichier JavaScript à part dans  `/composants` que nous pouvons appeler  `Banner.js`.

```jsx
function Banner() {
    return <h1>La maison jungle</h1>
}

export default Banner
```

```
Vous remarquez la notation  `export default`   ? Il s'agit d'une syntaxe prévue dans l'ES6, qui vous épargnera d'utiliser les accolades au moment de l'import. 
```

On peut maintenant adapter le code de  `App.js`   en supprimant le code de base, et **y importer notre `Banner`**.

```jsx
import Banner from './Banner'

function App() {
    return <Banner />
}

export default App
```

Ce qui nous donne :

![Notre Banner La maison jungle s'affiche dans le navigateur](https://user.oc-static.com/upload/2021/01/14/16105928894712_image12.png)

Notre Banner s'affiche dans le navigateur

Félicitations ! Vous avez réutilisé votre code du chapitre précédent !

![Logo de Webpack](https://user.oc-static.com/upload/2021/01/18/16109914276811_P2C1-2.png)

Import vos composants grâce à Webpack

Je l’ai déjà mentionné, mais ici, c’est [Webpack](https://webpack.js.org/) qui nous permet d’importer notre composant aussi facilement, avec `import`. Cet outil particulièrement utile est essentiel pour lier les fichiers entre eux, afin qu’ils soient interprétés par le navigateur. Et dire que Create React App nous a permis de l’installer sans faire aucune configuration. Si ça c’est pas de la chance ! 🍀