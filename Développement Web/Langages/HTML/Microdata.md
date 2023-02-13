# Microdata

Attributs supplémentaires HTML5 permettant de rajouter du contenu sémantique basé un document de référence => Schema.org

Les principaux attributs :

- `itemscope` : pour créer un nouveau élément sémantique. Les propriétés de l’élément seront définis dans les balises enfants (la balise parente avec l’attribut `itemscope` étant une sorte de container)
- `itemtype` : permet de définir le type d’élément sémantique grâce à une URL vers un document de référence
- `itemprop` : pour indiquer les propriétés de l’élément sémantique. Il est possible d’utiliser plusieurs propriétés de même nom mais avec une valeur différente. il est possible également de définir plus d’une propriété à la fois, avec la même valeur
- `itemid`

Remarque : il est possible de définir son propre vocabulaire

Exemple 1

```html
<!-- description d'une personne
Le container <section> défini une personne en utilisant le vocabulaire du schéma Person 
chaque propriétés définie dans cette section sont identifiées par la valeur de l'attribut itemprop des éléments enfants-->

<section itemscope itemtype="http://schema.org/Person">

	<p>
		<!-- name est une propriété de Person et a pour valeur : Jean Michu -->
		<span itemprop="name">Jean Michu </span><br>
		<!-- jobTitle est une propriété de Person et a pour valeur : Developpeur Web -->
		<span itemprop="jobTitle">Developpeur Web</span>
	</p>
	
	<!--adress est une propriété de Person et se réfère à un autre vocabulaire
	permettant de décrire une adresse postale : PostalAddress 
	Il faut donc créé un nouveau itemscope 
	et indiquer l'URL du schéma PostalAddress avec itemtype -->
	
	<p itemprop="address" itemscope itemtype="http://schema.org/PostalAddress">
		<span itemprop="streetAddress">1, rue de la paix </span><br>
		<span itemprop="postalCode">75000</span>
		<span itemprop="addressLocality">Paris</span>
	</p>
	<!-- fin du sous container PostalAdress -->
	
	<p itemprop="telephone">06.666.666</p>
	
	<p>
		<a href="mailto:jeanmichu@trucmail.fr" itemprop="email"> Mon adresse mail</a>
		<!--Deux propriétés de même nom mais avec valeurs différentes -->
		<a href="http://www.jeanmichu.fr" itemprop="url">Mon site Web</a>
		<a href="http://www.twitter.com/jeanmichu" itemprop="url">Mon Twitter</a>
	</p>

</section>
<!-- fin du container Person -->
```

Exemple 2

```html
<div itemscope itemtype="http://schema.org/MusicRecording">
	<h2>The song I just published</h2>
	<ul>
		<li>Name: <span itemprop="name">Please buy me on itunes, I need money!</span></li>
		<!-- ici on a défini deux propriétés qui ont la même valeur -->
		<li>Band: <span itemprop="genre keywords">Punk, Ska</span></li>
	</ul>
</div>
```

Les valeurs possibles :

- `a`, `area`, `audio`, `embed`, `iframe`, `img`, `link`, `object`, `source`, `video` : la valeur est l’URL indiquée par les attributs `href`, `src` ou `data`
- `time` : la valeur est la date ou/et heure indiquée dans l’attribut `datetime` et qui doit respecter le format ISO 8601
- `meta` : les valeurs sont indiqués dans l’attribut `content`. Cela permet d’inclure des micro-données qui n’’apparaissent pas dans le texte de la page
- toutes les autres balises : la valeur correspond au texte qui se trouve entre les balises d’ouverture et de fermeture
