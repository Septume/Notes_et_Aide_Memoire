# Display

Classes :

`d-{value}` , `d-sm-{value}` , etc.

Les valeurs :

- `none`
- `inline`
- `inline-block`
- `block`
- `table`
- `table-cell`
- `table-row`
- `flex`
- `inline-flex`

```html
 <div class="container-fluid">
     <div class="row">
     
         <!-- toute la largeur sur écran mobile et 10 colonnes sur écran desktop -->
         <div class="col-12 col-lg-10">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Soluta dolor ut consequatur enim, animi fugit, ducimus laborum aperiam porro doloremque.</div>
         
         <!-- non affiché sur écran mobile et afficher sur 2 colonnes sur écran desktop -->
         <div class="col-md-2 d-none d-lg-block ">Ad alias repellendus, cum labore consectetur minima omnis quos nulla non voluptatem dolore asperiores quia. Accusantium architecto, alias sint. Aliquid!
         </div>
     </div>
 </div>
```
