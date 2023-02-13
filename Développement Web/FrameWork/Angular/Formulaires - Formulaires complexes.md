# Formulaires complexes

Exemple d'approche : 
  1. créer des FormControls indépendants afin de pouvoir les manipuler plus facilement
  2. créer des FormGroups à partir de FormControls indépendants pour les regrouper et pouvoir les valider ensemble 
  3. Réunir le tout dans un FormGroup final afin de pouvoir récupérer toutes les valeurs en même temps, et de réagir aux événements de validation.  ce FormGroup héritera des validations de tous ses enfants.




