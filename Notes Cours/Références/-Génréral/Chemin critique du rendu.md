# Chemin critique du rendu

_Critical Rendering Path_
Les étapes effectuées par le navigateur pour passer du code brut au rendu final de la page Web

![[CRP-Sequence.png]]

**Parsing du code** : 
-   **Construction de l’arborescence du DOM** (_Document Object Model_) à partir du code HTML. L'analyse ne bloque pas le rendu (Il n’est pas nécessaire que le document complet soit analysé pour que le contenu commence à apparaitre sur la page)
-   **Construction de l’arborescence du CSSOM** (_CSS Object Model_) à partir du code CSS. Contrairement à l'HTML, l'analyse du CSS bloque le rendu (Le code CSS doit d'abord être complètement analysé avant de pouvoir être exécuté)
-   **Exécution du code JavaScript**. Ce dernier ne peut pas être exécuté tant que la construction du CSSOM n'est pas terminé (Le CSS est bloquant pour le JS). Par défaut, l' exécution du code JS met en pause l'analyse du code HTML (le JS est bloquant pour l'HTML)
⇒ Construction de l'**arbre de rendu** (_render tree_ ou _layer tree_). Il s'agit d'une combinaison du DOM et du CSSOM

Ensuite le navigateur dessine les éléments en passant par 3 phases :
-   **Layout** _:_ Le navigateur détermine la taille et le positionnement des éléments
-   **Paint** _:_ Le navigateur transforme les éléments en pixels
-   **Composite** _:_ Le navigateur combine les différents calques créés par certaines propriétés CSS (transformations, opacité, etc.)