FrameWork pour styliser rapidement l'app de la même facon que BootStrap.

[Lien Site Officiel](https://tailwindcss.com/docs/guides/create-react-app)
```bash
npm install -D tailwindcss postcss autoprefixer @tailwindcss/typography
```

puis
```bash
npx tailwindcss init -p
```
 qui créer une fichier `tailwind.confif.js` dans lequel on doit ajouter la partie **content**
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
	content: [
		"./pages/**/*.{js,ts,jsx,tsx}",
		"./src/**/*.{js,ts,jsx,tsx}",
	],
	theme: {
		extend: {},
	},
	plugins: [require("@tailwindcss/typography")],
};
```


Remplacer le css de `index.css`  (`styles.globals.css` pour next) par ce qui suit.
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

* {
box-sizing: border-box;
}
```

Next: 
1. Supprimer `Home.module.css` et son `import` dans `api.index.tsx`
2. Dans `index.tsx` supprimer le `main` et coller à la suite du header
```tsx
<div className='p-12'>
	<p className='text-red-500'>Test tailwind</p>
</div>
```
pour tester tailwind *(relancer le server)*.

lancer avec 
```bash
npm run start
```

