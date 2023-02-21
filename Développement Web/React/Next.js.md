  ### Installation
```shell
npx create-next-app@latest nextjs-blog --use-npm
```
1. ok to proceed `yes`
2. Voulez-vous utiliser `Type Script`
3. Voulez-vous utiliser `ESLint`
4. Voulez-vous utiliser `src/directory` No
5. Voulez-vous utiliser `app/ directory` No

### Mise en place
Créer un ficher dans `pages` appelé `post/[slug].tsx` (post/ => devenant un dossier)


```shell
npm install --save mdx-bundler esbuild gray-matter
```
librery
gray-matter => récupérer meta-data
mdx-bundler => bundler le mdx en fichier html/ css