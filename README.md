# babel-plugin-yo-yoify

Like [yo-yoify][], but as a Babel plugin. Transform [yo-yo][] or [bel][]
template strings into raw document calls.

## Example

**In**

```js
import bel from 'bel'

const title = 'yo-yoify'
const header = bel`
  <header id="page-header">
    <h1>${title}</h1>
    <button onclick=${event => alert('Hello world!')}>Click here</button>
  </header>
`
```

**Out**

```js
const title = 'yo-yoify';
const header = function () {
  var _h = document.createElement('h1');
  _appendChild(_h, [title]);

  var _button = document.createElement('button');
  _button.onclick = event => alert('Hello world!');
  _button.textContent = 'Click here';

  var _pageHeader = document.createElement('header');
  _pageHeader.setAttribute('id', 'page-header');
  _appendChild(_pageHeader, ['\n    ', _h, '\n    ', _button, '\n  ']);
  return _pageHeader;
}();

```

## Installation

```bash
npm install --save-dev babel-plugin-yo-yoify
```

## Usage

Without options:

```js
// .babelrc
{
  "plugins": [
    "yo-yoify"
  ]
}
```

With options:

```js
// .babelrc
{
  "plugins": [
    ["yo-yoify", {
      "appendChildModule": "yo-yoify/lib/appendChild"
    }]
  ]
}
```

## Options

 - `appendChildModule` - Import path to a module that contains a function that
   appends different types of children to an element. By default, the function
   included with [yo-yoify][] is used. Signature: `appendChild(el, array)`,
   where the `array` can contain any JavaScript value.

## License

[ISC][]

[yo-yoify]: https://github.com/shama/yo-yoify
[yo-yo]: https://github.com/maxogden/yo-yo
[bel]: https://github.com/shama/bel
[ISC]: ./LICENSE
