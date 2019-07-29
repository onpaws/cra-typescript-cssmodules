### TypeScript & CSS Modules?

Goal is to use CRA to write React components using the official [TypeScript](https://reactjs.org/docs/static-type-checking.html#adding-typescript-to-a-project) support, incorporating [CSS Modules](https://reactjs.org/blog/2018/10/01/create-react-app-v2.html#whats-new).

Despite following the [documentation](https://facebook.github.io/create-react-app/docs/adding-a-css-modules-stylesheet) as much as possible, there appears to be a gap in CRA's TypeScript support for CSS Modules, which is a shame. 

I found this [issue](https://github.com/facebook/create-react-app/issues/5677) but I can't seem to find anything newer on this.

[Download minimal repro](https://github.com/onpaws/cra-typescript-cssmodules)


Manual steps:
 - npx create-react-app myapp --typescript
 - add to `App.module.css`
```
.header {
  composes: background from './colors.module.css';
}

```
- add to `colors.module.css`
```
.background {
  background-color: #447;
}
```
- change App.tsx to:
```
import React from 'react';
import { header } from './App.module.css';

const App: React.FC = () => 
  <div className={header}>
    Hello, world.
  </div>

export default App;
```