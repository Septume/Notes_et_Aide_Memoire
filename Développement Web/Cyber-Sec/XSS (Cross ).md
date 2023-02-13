https://korben.info/articles/comment-ecrire-un-bouncer-crowdsec
## Comment une attaque XSS peut-elle se produire?

L'un des types d'attaques XSS les plus courants est une attaque **XSS basée sur DOM**. Lorsque vous mutez directement DOM, il devient facile pour un attaquant de lui injecter des données contenant du JavaScript malveillant. 

Le code HTML suivant rend simplement un balisage de base avec une **< div >** vide.

``` html
<html>
   <body>
       <div id="validation">
       </div>
       <input placeholder="Enter your referral code below" />
       <button>Submit</button>
   </body>
</html>
```

En appuyant sur le bouton de Soumission, on déclenche une fonction. À l'intérieur de la fonction, on évalue ce que l'utilisateur a entré. On fourni ensuite un message de rétroaction à l'utilisateur en fonction du résultat à l'intérieur de la **< div >** vide.

```jsx
const validationElement = document.getElementById('validation');
const validationMessage = `Oops! This seems like an invalid referral code.`
validationElement.append(validationMessage);
```

L'utilisation de la méthode **"append"** rend un message à l'intérieur de notre **< div >** vide. Cependant, cela expose une vulnérabilité dans notre application. 

```jsx
Oops! This seems like an invalid referral code.
<script>
  ...
  alert('Congrats! You've won a prize');
  ...
</script>
```

L'attaquant rend essentiellement le message de validation accompagné d'un **< script >** malveillant. Cela était possible car l'application modifie le DOM directement à l'aide de la méthode **append ( )** sur la **< div >**. À l'intérieur du **< script >**, l'attaquant peut écrire du code qui vole nos informations confidentielles et sensibles. Pour des motifs similaires, si nous utilisons **innerHTML** pour muter le DOM directement, on expose notre application à une attaque XSS potentielle. 

Ainsi, une attaque XSS peut être un spectacle alarmant pour vos utilisateurs. Cependant, les cadres frontaux ont parcouru un long chemin et offrent une certaine protection contre de telles attaques. Voyons comment React gère ces situations pour vous et jusqu'où il sécurise votre application contre une attaque XSS.