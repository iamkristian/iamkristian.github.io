---
layout: post
title:  "Learn me some react"
date:   2023-01-10 09:00:00
image: IMG_6049.png
image_thumb: IMG_6049_thumb.png
subtitle: The one about learning react
categories: react
---
How to start out with react? [reactjs.org](https://reactjs.org/) is a good
place to start out.

Do I code React in
[javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) or
[typescript](https://www.typescriptlang.org/)? It's optional. However in this
example I'm going with typescript, since I'm a fan of type checks and a modern
frameworks.

So how to get started? A bit confusing actually - the react website gives me
quite a few options to chose from.

Being an avid macuser I want the ability to switch between node versions, this
becomes obvious when getting more practical experience.

So I need [node.js](https://nodejs.org/en/) - this can be accomplished with the
node version manager tool.
```
brew install nvm
```
Be sure to copy/paste the additional installation steps from brew into your .bashrc or .zshrc.

Now you're ready to run

```
nvm install --lts
```

And from here you can generate your first react app - following the [react guide](https://beta.reactjs.org/learn/start-a-new-react-project)

## Yarn and corepack

To use react with typescript we need [yarn](https://yarnpkg.com/getting-started/install)

```
npm install -g corepack
```

Activate yarn at a stable version

```
corepack prepare yarn@stable --activate
```

## Typescript

Now it will be possible to add typescript with

```
yarn add typescript --dev
```

It is possible to create the project from scratch with

```
npx create-react-app my-app --template typescript
```

More on the [Typescript Language for JS programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html).

## Finding your way around



