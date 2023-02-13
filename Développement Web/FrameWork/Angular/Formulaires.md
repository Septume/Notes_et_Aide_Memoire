# Formulaires

Les formulaires sont construit avec 4 briques de bases (classes) : 
- `FormControl` : permet de suivre la valeur, la validité et les interactions d'un contrôle de formulaire
- `FormGroup` : permet de créer un groupe de `FormControl` (Utilise un objet avec le nom du contrôle comme clé et sa valeur associée). La validité des données se fait sur l'ensemble du groupe. (Si un seule contrôle est invalide tout le groupe l'est aussi)
- `FormArray` : Permet de créer un tableau de `FormGroup`. On peut par la suite ajouter ou supprimer des `formGroup` pour créer des champs dynamiques. La validité des données se fait sur l'ensemble du tableau.
- `FormRecord` : Similaire à `FormGroup` . Peut être utilisé avec une clé dynamique et des contrôle ajouter et supprimer

 `[FormBuilder]` : fournit du sucre syntaxique qui raccourcit la création d'instances de `FormControl`, `FormGroup` et `FormArray`

Deux approches pour construire un formulaire :
- Template Driven Forms : logique gérée depuis le template => Utiliser pour les formulaires simples
- Reactive Forms : logique gérée depuis le component => Utiliser pour les formulaires complexes

[[Formulaires - Template Driven Forms]]
[[Formulaires - Reactive forms]]
[[Formulaires - Formulaires complexes]]











