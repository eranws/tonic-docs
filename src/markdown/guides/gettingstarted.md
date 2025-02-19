# Getting Started

Building a component with Tonic starts by creating a function or a class.
The class should have at least one method named *render* which returns a template literal
of HTML.

```js
import Tonic from '@optoolco/tonic'

class MyGreeting extends Tonic {
  render () {
    return this.html`<div>Hello, World.</div>`
  }
}
```

or

```
function MyGreeting () {
  return this.html`
    <div>Hello, World.</div>
  `
}
```

---

The html tag for your component will match the class or function name.

> <i><b>Note</b>: Tonic is a thin wrapper around `web components`. Web
> components require a name with two or more parts. So your class name should
> be `CamelCased` (starting with an uppercase letter). For example, `MyGreeting`
> becomes `<my-greeting></my-greeting>`.</i>

---

Next, register your component with `Tonic.add(ClassName)`.

```js
Tonic.add(MyGreeting)
```

---

After adding your Javascript to your HTML, you can use your component anywhere.

```html
<html>
  <body>
    <my-greeting></my-greeting>

    <script src="index.js"></script>
  </body>
</html>
```

> <i><b>Note</b>: Custom tags (in all browsers) require a closing tag (even if
> they have no children). Tonic doesn't add any "magic" to change how this works.</i>

---

When the component is rendered by the browser, the result of your render
function will be inserted into the component tag.

```html
<html>
  <head>
    <script src="index.js"></script>
  </head>

  <body>
    <my-greeting>
      <div>Hello, World.</div>
    </my-greeting>
  </body>
</html>
```

A component (or its render function) may be `async` or an `async generator`.

```js
class GithubUrls extends Tonic {
  async * render () {
    yield this.html`<p>Loading...</p>`

    const res = await fetch('https://api.github.com/')
    const urls = await res.json()

    return this.html`
      <pre>
        ${JSON.stringify(urls, 2, 2)}
      </pre>
    `
  }
}
```

[0]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes
[1]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
[2]:https://caniuse.com/#search=domcontentloaded
