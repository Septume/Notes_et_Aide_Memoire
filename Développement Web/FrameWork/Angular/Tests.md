# Tests

Voir [[Jasmine]]

Lancer la commande : `ng test --watch` 

## Karma

Fonctionnement : 
- Utilise un serveur 
- Ouvre le(s) navigateur(s) configuré(s) pour les tests qui se connectent sur le serveur de karma
- Suis les changements  du code des tests unitaires
- A chaque changement déclenche le build du code source modifié, puis émet un évènement pour que le navigateur exécute les tests
- Les tests sont exécutés sur le navigateur et les résultats sont transmis au serveur Karma,
- Karma produit les rapports en fonction des plugins activés : console, HTML, code coverage, etc...


## Fonction async() 

Fonction spécifique à Angular (à ne pas conforme avec le `async` de la spécification JS)


## TestBed 

Il s'agit d'une classe Angular qui permet de créer l'environnement de test en émulant le fonctionnement d'un module 

`TestBed.configureTestingModule()` : Méthode qui permet de déclarer les modules, composants, ou services à tester. La configuration est assez similaire à celle que l'on utilise dans un `@NgModule`
- `compileComponents()` : Méthode asynchrone de `configureTestingModule(()` qui s'occupe de la compilation des templates. Cette méthode n'est pas utile si on a déjà généré les templates avec le CLI 
`TestBed.inject()` : Méthode qui s'occupe de l'injection des services
`TestBed.createComponent()` :  permet d'instancier le composant donc le type est indiqué en argument. Retourne un objet `ComponentFixture`  avec les propriétés suivantes : 
- `componentInstance` : Instance du component
- `debugElement` : objet permettant d'inspecter et de manipuler le DOM.
- `detectChanges()` : déclenche la Change Detection.

```TS
describe('AppComponent', () => {
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [
        RouterTestingModule
      ],
      declarations: [
        AppComponent
      ],
    }).compileComponents();
  });

  it('should create the app', () => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.componentInstance;
    expect(app).toBeTruthy();
  });
});
```







