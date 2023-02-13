# Jasmine

Installation : `npm install --save-dev jasmine`  
Initialiser un projet Jasmine : `npx jasmine init` => créer un dossier `spec` qui contient un fichier de configuration `jasmine.json`  
Pour lancer les tests : `npx jasmine`  
Pour lancer un spec spécifique : `npx jasmine spec/appSpec.js`

## Fichier de configuration

```JSON
{
  "spec_dir": "spec", // répertoire des fichiers de tests
  "spec_files": [
    "**/*[sS]pec.?(m)js" // nom des fichiers de tests (.spec.js)
  ],
  "helpers": [
    "helpers/**/*.?(m)js" // configuration à exécuter lors des tests. Se trouve dans un dossier `helpers` 
  ],
  "env": {
    "stopSpecOnExpectationFailure": false,
    "random": true
  }
}
```

## Script de test

Dans `package.json`

```JSON
"scripts": {
    "test": "jasmine"
  },
```

Puis lancer `npm test` pour lancer jasmine

### Exemple de code

```JS
// suite 
describe("suite de spec", function() {
  let a;
  //  Spécification
  it("spec", function() {
    a = true;
    // assertion
    expect(a).toBe(true);
  });
  // sous-suite
  describe("suite de spec", function() {/*code */});
  
});
```

  `describe`  : pour Indiquer ce qui vas être tester  
  `it` : pour indiquer une spécification => ce qui  doit normalement se passer.  
  `expect` : correspond à une assertion (ou *expection* en anglais) => consiste à tester une valeur réelle pour vérifier qu'elle correspond bien à une valeur attendu. Utilise un matcher qui permet d'effectuer un type de comparaison.  

## Matchers

```JS
expect(mixed).toBeUndefined(); // undefined
expect(mixed).toBeDefined(); // defined
expect(mixed).toBeNull(); // null
expect(mixed).toBeTruthy(); // true
expect(mixed).toBeFalsy(); // false
expect(mixed).toEqual(mixed); // égal
expect(mixed).toMatch(pattern); // correspond à la regex
expect(mixed).toBeNaN() // n'est pas un nombre
expect(number).toBeGreaterThan(number); // plus grand que 
expect(number).oBeGreaterThanOrEqual(number); // plus grand ou egal
expect(number).toBeLessThan(number); // plus petit que
expect(object).toContain(value); // doit contenir (valeur de tableaun, sous chaine)
expect(fn).toThrow(e); // levée d'erreur
expect(object).toBe(object); // comparaison ===
expect(object).toBeInstanceOf(className)

// chaque assertions à une variante négative
// exemple
expect(number).not.toBeLessThan(number)
```

Remarque : Il est possible de créer des matchers personnalisés

## Méthodes globales 

`beforeEach()` : Permet d'indiquer une fonction setup qui sera appelée avant l'exécution de chaque specs. Permet de préparer un environnement sain pour chaque spec
`afterEach()` : Permet d'indiquer une fonction de "tear down"  qui sera appelée après l'exécution de chaque specs. Permet de nettoyer l' environnement 

Exemple 

```JS
describe('Calculator', () => {
  const calculator
  beforeEach(() => {
    calculator = new Calculator();
  });
  it('should evaluate 2 + 3 + 4 to 9', () => {
    expect(calculator.evaluate('2 + 3 + 4')).toEqual(9);​
  });
});
```

## Code Asynchrone 

La fonction de spec peut retourner une promesse dont la  résolution signale la fin du test 

```JS

it('should not affect arithmetic rules', async () => {
  await new Promise(resolve => {
    setTimeout(() => {
      expect(1).not.toEqual(2);
      resolve();
    });
  });
});
```


