![Happy DOM Logo](https://github.com/capricorn86/happy-dom/raw/master/docs/happy-dom-logo.jpg)


# About

A [JSDOM](https://github.com/jsdom/jsdom) alternative with support for server side rendering of web components.

[Happy DOM](https://github.com/capricorn86/happy-dom) aims to support all common functionality of a web browser.

This package makes it easier to setup servering side rendering of web components by handling the setup of the Node [VM Context](https://nodejs.org/api/vm.html#vm_vm_createcontext_sandbox_options) for you.



### DOM Features

- Custom Elements (Web Components)

- Shadow Root (Shadow DOM)

- Mutation Observer

- Tree Walker

- Fetch

And much more..



### Works With

- [Google LitHTML](https://lit-html.polymer-project.org)

- [Google LitElement](https://lit-element.polymer-project.org)

- [React](https://reactjs.org)

- [Angular](https://angular.io/)

- [Vue](https://vuejs.org/)

  

# Installation

```bash
npm install @happy-dom/server-rendering
```



# Usage


```javascript
import { HappyDOMContext } from '@happy-dom/server-rendering';
import { Script } from 'vm';

const context = new HappyDOMContext();
const result = context.render({
    url: 'http://localhost:8080',
    html: `
        <html>
            <head>
                <title>Test page</title>
            </head>
            <body>
                <div class="myContainer">
                    <!–– Content will be added here -->
                </div>
            </body>
        </html>
    `,
    scripts: [
        new Script(`
            const element = document.createElement('div');
            const myContainer = document.querySelector('.myContainer');
            element.innerHTML = 'Test';
            myContainer.appendChild(element);
        `)
    ],
    customElements: {
        openShadowRoots: true,
        extractCSS: true,
        scopeCSS: true,
        addCSSToHead: true
    }
});

// Outputs: <html><head><title>Test page</title></head><body><div class="myContainer">Test</div></body></html>
console.log(result);
```