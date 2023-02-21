```tsx
<Routers>
	<Route path='/login' element={ <LoginForm/>}/>
	<Route path='/Profile/:id' element={ <Profile/>}/>
	<Route path='/Service/*' element={ <Service/>}/>
</Routers>
```
# /:id
est une route dynamique mais restrictive à un seul enfant.

# /*
`/api/Profile/jahn/caracteristique` => redirige vers `/service`
est une route dynamique pouvant découler sur plusieurs enfants.
*Pratique pour rediriger un petit malin cherchant une page inexistante.*

# Imbriquer des routes

Supprimer le `/` à la fin de la ligne, pour rajouter une fin de balise `</Route>` qui englobe les routes imbriquées.
```tsx
<Route path='/Profile' element={ <Profile/>}>
	<Route path='/Profile/caracteristique' element=
		{<Caracteristique/>} />
	<Route path='/Profile/adresse' element=
		{<Adresse/>} />
</Route>

```

aller dans `Profile.tsx` et importer `Outlet` *(sortie)* dans le `from "react-router-dom"`.

Et imbriquer `<outlet/>` dans le html ou doit apparetre les components imbriquer