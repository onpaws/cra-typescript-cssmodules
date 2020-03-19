### TypeScript + CSS Modules + React
##### aka error TS2614: CSS Module has no named exported members

My goal is to use [TypeScript](https://reactjs.org/docs/static-type-checking.html#adding-typescript-to-a-project) + [CSS Modules](https://reactjs.org/blog/2018/10/01/create-react-app-v2.html#whats-new) in my React app.

In JavaScript, both named and default CSS modules import work OK.
```
import React from 'react';
import { header } from './App.module.css';

const Component = () =>
  <div className={header}>
    Hello, world.
  </div>

export default Component
```

However with TypeScript, the compiler chokes on the named import `header`:
```
import React from 'react';
import { header } from './App.module.css';

const App: React.FC = () => 
  <div className={header}>
    Hello, world.
  </div>

export default App;
```
I guess the types are provided via webpack+babel, not sure.

Error message:
```
Failed to compile.

cra-typescript-cssmodules/src/App.tsx
TypeScript error in cra-typescript-cssmodules/src/App.tsx(2,10):
Module '"*.module.css"' has no exported member 'header'. Did you mean to use 'import header from "*.module.css"' instead?  TS2614

    1 | import React from 'react';
  > 2 | import { header } from './App.module.css';
      |          ^
    3 | 
    4 | const App: React.FC = () => 
    5 |   <div className={header}>

```


I found this [issue](https://github.com/facebook/create-react-app/issues/5677) but it's been closed and can't seem to find anything newer on this.

[Download minimal repro](https://github.com/onpaws/cra-typescript-cssmodules)


### Manual repro steps

 - npx create-react-app myapp --typescript
 - To `App.module.css` add the following:
```
.header {
  composes: background from './colors.module.css';
}
```
- To `colors.module.css` add the following:
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