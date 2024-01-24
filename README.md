# Angular + Eslint + Prettier

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.1.1.

Selected options in interactive mode:

```bash
? Which stylesheet format would you like to use? CSS
? Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No
```

1. [Preparation](#preparation)
2. [Eslint](#eslint)
3. [Prettier](#prettier)
4. [Git hooks](#git-hooks)

## Preparation

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

But, my personal preference is to use double quotes, so I change the configuration to

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
