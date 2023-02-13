## `Button.module.css`[​](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/#buttonmodulecss "Lien direct vers le titre")

```
.error {  background-color: red;}
```

Copier

## `another-stylesheet.css`[​](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/#another-stylesheetcss "Lien direct vers le titre")

```
.error {  color: red;}
```

Copier

## `Button.js`[​](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/#buttonjs "Lien direct vers le titre")

```
import React, { Component } from 'react';import styles from './Button.module.css'; // Import css modules stylesheet as stylesimport './another-stylesheet.css'; // Import regular stylesheetclass Button extends Component {  render() {    // reference as a js object    return <button className={styles.error}>Error Button</button>;  }}
```

Copier

## Résultat[](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/#result "Lien direct vers le titre")

Aucun affrontement d'autres `.error` noms de classe

```
<!-- This button has red background but not red text --><button class="Button_error_ax7yz">Error Button</button>
```

Copier