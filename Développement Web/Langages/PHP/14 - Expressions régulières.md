# Expressions régulières

PHP utilise pour les regex l’extension PCRE (Perl Compatible Regular Expression). Cette extension utilise pratiquement la même syntaxe que les regex de PERL

Extension POSIX => dépréciée depuis la version 5.3. Supprimée dans la version 7

### Structure d’une regex

`/regex/options`

N’importe quel caractère à l’exception de l’antislash peut être utilisé comme délimiteur. En général on utilise le slash ou les caractères `() {} [] <>`

Options :

- `i` : la casse n’est pas pris en compte
- `s` : le symbole point qui permet de remplacer n’importe quel caractère, remplace également le caractère de retour à la ligne
- `m` : recherche multilignes
- `x` : permet d’ignorer les caractères d’espacement

### Fonctions

`preg_match(regex, chaine)` : retourne le nombre d’occurrence ou false. La fonction s’arrête dès la première occurrence trouvée

`preg_match_all(regex, chaine)` : même chose mais recherche toute les occurrences

`preg_replace(regex, chaine_remplacement, chaine_a_traiter )` : recherche et remplace une regex
