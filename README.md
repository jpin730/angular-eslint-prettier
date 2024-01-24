# Angular + Eslint + Prettier

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.1.1.

Selected options in interactive mode:

```bash
? Which stylesheet format would you like to use? CSS
? Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No
```

1. [Preparation](#preparation)
2. [Eslint](#eslint)

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
