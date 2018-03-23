# React Fiber renderer for PIXI

![](https://img.shields.io/badge/tested_with-jest-green.svg)
[![CircleCI](https://circleci.com/gh/inlet/react-pixi-fiber.svg?style=shield&circle-token=d485cdd81a76e041173d51205e62ac1e5dce3f9b)](https://circleci.com/gh/inlet/react-pixi-fiber)
![](https://img.shields.io/badge/license-MIT-green.svg) 
![](https://img.shields.io/badge/code_style-prettier-blue.svg)
![](https://img.shields.io/badge/react-fiber-ff69b4.svg)
![](https://img.shields.io/badge/pixi-v4+-ff69b4.svg)

A custom React 16 (Fiber) renderer. Write [PIXI](http://www.pixijs.com/) applications using React declarative style.

![](https://user-images.githubusercontent.com/232559/37669267-b46a8f8e-2c66-11e8-96e7-cae2ae6bdd7d.png)

## Install

```
yarn add @inlet/react-pixi
```

## Usage 

```jsx
import { Stage, Sprite } from '@inlet/react-pixi'

const App = () => (
  <Stage>
    <Sprite image="./bunny.png" x={100} y={100} />
  </Stage>
)
```

## Custom Components

```jsx
// ./components/Rectangle.js

import * as PIXI from 'pixi.js'
import { PixiComponent } from '@inlet/react-pixi'

export default new PixiComponent('Rectangle', {
  create: props => {
    return new PIXI.Graphics()
  },
  didMount: parent => {
    // apply custom logic on mount
  },
  willUnmount: parent => {
    // clean up before removal
  },
  applyProps: (instance, oldProps, newProps) => {
    const { fill, x, y, width, height } = newProps
    instance.clear()
    instance.beginFill(fill)
    instance.drawRect(x, y, width, height)
    instance.endFill()
  }
})

// App.js

import { Stage } from '@inlet/react-pixi'
import Rectangle from './components/Rectangle'
export default () => (
  <Stage>
    <Rectangle x={100} y={100} width={500} heigth={300} fill={0xff0000}/>
  </Stage>
)
```

## Scripts

```bash
# compile umd & es builds
yarn build

# compile dev builds
yarn build:dev

# compile production builds
yarn build:prod

# watch development builds
yarn build:watch

# lint code
yarn eslint

# fix linting issues
yarn eslint --fix

# test
yarn test

# watch tests
yarn test:watch
```

## Resources

- [github.com/acdlite/react-fiber-architecture](https://github.com/acdlite/react-fiber-architecture)
- [github.com/nitin42/Making-a-custom-React-renderer](https://github.com/nitin42/Making-a-custom-React-renderer)
- [github.com/facebook/react/tree/master/packages/react-art](https://github.com/facebook/react/tree/master/packages/react-art)
- [github.com/facebook/react](https://github.com/facebook/react)
- [github.com/michalochman/react-pixi-fiber](https://github.com/michalochman/react-pixi-fiber)
