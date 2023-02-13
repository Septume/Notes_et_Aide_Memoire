# PostgreSQL - Introduction

## Présentation

Caractéristiques : 
- Open Source
- Très utilisé en entreprise
- supporte à la fois les requêtes SQL (relationnelles) et JSON (non relationnelles).
-  extensible => on peut définir ses propres types de données, types d'index, langages fonctionnels, etc.

Fonctionnalités avancées
- Types définis par l'utilisateur
- Héritage des tables
- mécanisme de verrouillage sophistiqué
- Intégrité du référentiel des clés étrangères
- Vues, règles, sous-requête
- Transactions imbriquées (points de sauvegarde)
- Contrôle de simultanéité multi-version (MVCC)
- Réplication asynchrone


Limites de PostgreSQL
- La taille d’un champ est limitée à 1 gigaoctet. En pratique, cette taille est limitée par la quantité de mémoire vive disponible pour lire ce champ.
- La taille d’une ligne est limitée à 1,6 téraoctet.
- La taille d’une table est limitée à 32 téraoctets.
- Le nombre maximal de colonnes dans une table peut aller de 250 à 1600, selon la taille d’un bloc de données et la taille des types de données utilisés pour les colonnes.


## Installation sous Windows

Après l'installation ajouter `C:\Program Files\PostgreSQL\<numero_version>\bin` au PATH


## Se connecter au serveur 

Deux méthodes pour se connecter au serveur : 
- La commande `psql` 
- Application graphique `pgAdmin` 

`psql -U postgres` : Se connecter avec l'utilisateur par défaut (*postgres*)

connaitre la version de postgreSQL : `SELECT version();` 

Pour quitter : `exit`

## Créer une base de données 

`CREATE DATABASE database_name;`

Pour restaurer une base de données (créer d'abord la base) : 
`pg_restore -U <user> -d <database_name> <path>
Ex : `pg_restore -U postgres -d dvdrental C:\sampledb\dvdrental.tar` 

## SQL 

Les mots-clés SQL sont insensibles à la casse.
Par exemple `SELECT` est équivalent à `select` ou `Select`. 
Par convention, on utilise les mot clés SQL en majuscules pour faciliter la lecture des requêtes.

Les instructions SQL doivent être terminées par un point-virgule 

