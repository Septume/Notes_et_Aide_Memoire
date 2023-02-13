# Gestion des erreurs

### **Méthodes de la console**

`console.info()` : affiche une information

`console.warn()` : affiche un avertissement

`console.error()` : affiche une erreur

### **Structure try…catch…finally**

```jsx
try {
    // code a tester
    //  s’il n'y a pas d'erreur, le bloc est exécuté
} catch(e) {
    // ce bloc est exécuté si une erreur est detectée
    // la variable e est une référence vers l'erreur
    console.error(e); 
}finally{ //facultatif
    // ce bloc est exécuté dans tout les cas (erreur ou pas)
}
```

### **Throw**

Mot clé permettant de lever une exception

`throw "message à afficher"`

Exemple

```jsx
function division(a,b){
    if(isNaN(a) ||  isNaN(b)){
        throw 'Erreur de type';
    }
    if (b === 0){
        throw 'Division par zéro impossible';
    }
    return a/b;
}

try {
    console.log(division(3,0));
} catch(e) {
    console.error(e); // affiche 'Division par zéro impossible'
}
```
