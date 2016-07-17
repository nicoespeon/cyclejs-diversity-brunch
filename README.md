# Cycle.js Diversity + Brunch + Babel/ES6

This repository illustrate the issue I'm facing to run [Cycle.js Diversity](https://github.com/cyclejs/core/releases/tag/v7.0.0) with latest version of Brunch + ES6.

## Witness the issue

1. Clone this repo
2. `npm install`
3. `npm start`
4. Go to http://localhost:3333/
5. Open your DevTools, a wild error message should appear

## Steps to reproduce this repo

1. Let's consider you have Node.js and Brunch installed.
2. Set up new repo from Brunch ES6 skeleton: `brunch new cyclejs-diversity-brunch -s es6`.
3. Install Cycle.js Diversity: `npm install xstream @cycle/xstream-run @cycle/dom`
4. Replace `app/index.js` with the following code:

```javascript
import {run} from '@cycle/xstream-run';
import {div, label, input, hr, h1, makeDOMDriver} from '@cycle/dom';

function main(sources) {
  const sinks = {
    DOM: sources.DOM.select('.field').events('input')
      .map(ev => ev.target.value)
      .startWith('')
      .map(name =>
        div([
          label('Name:'),
          input('.field', {attrs: {type: 'text'}}),
          hr(),
          h1('Hello ' + name),
        ])
      )
  };
  return sinks;
}

run(main, { DOM: makeDOMDriver('#app') });
```
