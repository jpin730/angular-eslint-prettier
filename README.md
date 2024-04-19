# Angular + ESLint + Prettier

## Introduction

This is a simple Angular project with Eslint and Prettier configured. The main goal is to have an Angular project with a good code style and format, and to achieve this, I use Eslint and Prettier together. I try to resume in simple steps how to configure it in a new Angular project. There are one branch for the result of each step, so you can see the changes in each one.

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.3.5 through the following command:

```bash
ng new --minimal --ssr=false --style=css --skip-git --skip-install angular-eslint-prettier
```

## Table of contents

1. [Preparation](#preparation)
2. [Eslint](#eslint)
3. [Prettier](#prettier)
4. [Git hooks](#git-hooks)
5. [Recommended VSCode extensions](#recommended-vscode-extensions)

## Preparation

Generate .nvmrc file with the Node version used in the project

```bash
node -v > .nvmrc
```

Use [Node Version Manager](https://github.com/nvm-sh/nvm) for set Node version specified in .nvmrc file

```bash
nvm use
```

Install dependencies

```bash
npm install
```

## Eslint

Add [Angular Eslint Schematics](https://github.com/angular-eslint/angular-eslint) to project

```bash
ng add @angular-eslint/schematics
```

For execute linting on all files you can use

```bash
npm run lint
```

## Prettier

Add [Prettier](https://prettier.io/docs/en/install) to project

```bash
npm install --save-dev --save-exact prettier
```

Add `.prettierrc` file to project root and the [basic configuration suggested by Prettier](https://prettier.io/docs/en/configuration) is

```json
{
  "trailingComma": "es5",
  "tabWidth": 4,
  "semi": false,
  "singleQuote": true
}
```

But, my personal preference is to use 2 spaces for indentation and trailing commas in all cases, so my `.prettierrc` file is

```json
{
  "trailingComma": "all", // changed
  "tabWidth": 2, // changed
  "semi": false,
  "singleQuote": true
}
```

Install [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier) to make ESLint and Prettier play nice with each other

```bash
npm install --save-dev eslint-config-prettier
```

Add eslint-config-prettier at the end of the extends array in your `.eslintrc.json` file

```json
{
  "extends": ["...", "prettier"]
}
```

You can add a script to your package.json to run Prettier on all files ignoring unknown ones

```json
{
  "scripts": {
    "format": "prettier --write --ignore-unknown ."
  }
}
```

And then run it with

```bash
npm run format
```

## Git hooks

For check linting and formatting before commit you can use [husky](https://github.com/typicode/husky) and [lint-staged](https://github.com/lint-staged/lint-staged)

```bash
npm install --save-dev husky lint-staged
npx husky install
npm pkg set scripts.prepare="husky install"
npx husky add .husky/pre-commit "npx lint-staged"
```

For husky 9 or later, `npx husky install` and `npx husky add` are deprecated, so you can use the following commands

```bash
npx husky init
```

In file `.husky/pre-commit` replace the content with

```bash
npx lint-staged
```

> Note: For CI environments, when install dependencies use `npm ci --ignore-scripts` to avoid prepare script execution

Add the following to your `package.json` file

```json
{
  "lint-staged": {
    "**/*.{ts,html}": "npx eslint --fix",
    "**/*": "npx prettier --write --ignore-unknown"
  }
}
```

> Note: It's important to run Prettier after ESLint

## Recommended VSCode extensions

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
