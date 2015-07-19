i18n-react
===
React (JS) text internationalization and externalizing.

##Quick example

```js
var React = require('react');
var T = require('i18n-react');

T.setTexts({
  greeting: "Hello, World! My name is *{myName}*! \n {{howAreYou}}",
  howAreYou:  "_How do you do?_"
});

React.render(
  <T text="greeting" myName="i18n-react"/>,
  document.getElementById('content')
);
```

Unsurprisingly renders:
********
Hello, World! My name is **i18n-react**!

_How do you do?_

********

###External yaml resource file
Usually texts are retrived from an extrenal source (I would recommend YAML format) but
loading of the external files is out of scope for the library.

```yaml
greetings:
  hello: Hi, {who}!
  howdy:
    formal: How do you do?
    normal: How are you, {who}?
    informal: "What's up?"
  bye: Bye

longTime:
  0: Not a day no see
  1: 1 day no see
  _: "[{context} days][Long time no see]"
```

Points of interest:
* {who} - variable interpolation
* formal/informal - context selectors
* longTime - pluralization
* [X days][...] - renders two paragraphs


## Usage
Npm compatible packager (browserify/webpack) is recommended, but ```Dist``` folder also contains UMD versions
(regular and minified) that can be used w/o commonJS packager.

```js
/* commonJS */
var T = require('i18n-react');
/* when using UMD version w/o modules */
var T = window['i18n-react'];
```


Initialize once - probably in an application entry point js:
```js
T.setTexts(require('../texts/texts-en.yml'));
/* or */
T.setTexts({
  greeting: "Hello, World! My name is *{myName}*! \n {{howAreYou}}",
  howAreYou:  "_How do you do?_"
});
```

Use it anywhere:
```xml
 <T text="path.to.string" context="context-if-any" var1="string" var2={int} var3={ReactElement}/>
 <T.p text="path.to.string" var1="string" var2={int} anyValidHtmlAttribute="p.will.have.it"/>
 <T.a text="path.to.string" href="a's href"/>
 <T tag='li' text="path.to.string" varInt={1} varReact={<span className="c">X</span>}/>
 <h1>{T.translate("path.to.string", { context: "context", var1: 2})}</h1>
```

As documentation is non-existent you are welcomed to consult unit tests for usage details and examples.

## Development
#### Global npm modules dependencies for required for development
- typescript
- react-tools

#### Commands
* Build commonJS version:  ```$ npm start```
* Watch commonJS folder:  ```$ npm run watch```
* Build UMD version:  ```$ npm run build```
* Start dev server for examples (http://localhost:1818/webpack-dev-server/examples/): ```$ npm run examples```
* Build examples: ```$ npm run build-examples```
* Watch tests (Chrome): ```$ npm test```


