# vtex-react-checkout

This is a WIP boilerplate for using React (and more!) within [VTEX Checkout UI Custom](https://vtex.io/docs/components/functional/vtex.checkout-ui-custom@0.0.9/), created by [Enzo Spagnolli](https://github.com/Enzo3322), [Gabriel Nobrega](https://github.com/ganobrega), and [Gustavo Amemiya](https://github.com/gustavokei)

## Preview

![app image](https://i.imgur.com/UDLqxW1.gif)

## Features:

- ReactJS support and all its benefits (plugins, hooks, context api, etc)
- Typescript support
- SCSS support
- Easy SVG importing
- Support for legacy code (your old `checkout6-custom.js` scripts should work without any issues)
- Integrity Hash for files check-up
- A much more organized files structure

## Installation

Download this repository into your `checkout-ui-custom` folder to  and run

```js
yarn
```

* PS: If you don't have the folder `checkout-ui-custom` in your project folder, rename the folder `vtex-react-checkout` that you downloaded to `checkout-ui-custom`

Then, compile `checkout6-custom.js` and `checkout6-custom.css` by running

```js
yarn dev
```

Finally, link your app

```js
vtex link
```

Saving your work will automatically recompile the main files

Your old `checkout6-custom.js` scripts should be reimplemented into `src/scripts/main.jsx`, no changes required

## Folder Structure

    .
    ├── src                       # Source
    │   ├── icons                 # SVG Icons
    │   ├── scripts               # JS
    │   ├── styles                # SCSS
    │   ├── checkout6-custom.scss # SCSS importer
    │   └── checkout6-custom.tsx  # TSX importer
    ├── checkout6-custom.css      # Compiled CSS
    ├── checkout6-custom.js       # Compiled JS
    └── ...

## Implementing a React Component

### Step 1 - Creating a render method

Inside the `scripts` folder, create a `renderComponent.tsx` file

    .
    ├── scripts
    │   ├── components
    │   ├── main.jsx
    │   └── renderComponent.tsx <<
    └── ...

```js
import React from "react";
import ReactDOM from "react-dom";
import ExampleComponent from "./components/ExampleComponent";

window.addEventListener("DOMContentLoaded", () => {
  const div = document.createElement("div");
  div.setAttribute("class", "example-preact-component");
  document.querySelector(".cart-template")?.prepend(div);
  ReactDOM.render(<ExampleComponent />, div);
});
```

This will render a react component before the first child of the `.cart-template` element as soon as the page loads

In order to timely render a component, you'll need to create your own methods:

```js
import React from "react";
import ReactDOM from "react-dom";
import AnotherExampleComponent from "./components/AnotherExampleComponent";

window.addEventListener("DOMContentLoaded", () => {
  const checkHash = () => {
    if (location.hash === "#/payment") {
      const div = document.createElement("div");
      div.setAttribute("class", "another-example-component");
      document.querySelector(".cart-template")?.prepend(div);
      ReactDOM.render(<AnotherExampleComponent />, div);
    }
  };
  checkHash();

  window.addEventListener("hashchange", () => {
    checkHash();
  });
});
```

In the example above, the component will render everytime `#/payment` loads

You can go even deeper into the complexity layers. To illustrate, by using `MutationObserver` and/or listening to VTEX's methods like `orderFormUpdated.vtex`, be creative 😉

### Step 2 - Creating your React Component

Just put your component inside the `components` folder. There is no catch!

    .
    ├── components/ExampleComponent
    │   ├── context
    │   ├── ExampleContent.tsx
    │   └── index.tsx
    └── ...

Feel free to take a look at this repo's example component. I have implemented React's Context API + [Swiper](https://github.com/nolimits4web/swiper) slider. Installing plugins is also easy, you should get away with it by following their instructions
