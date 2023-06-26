<h1>Node.js + TypeScript</h1>

## Setting up the TypeScript compiler
* Create a `tsconfig.json` file `npx tsc —init`
```json
{
  "compilerOptions": {
    "target": "ES2018",
    "lib": ["ES6"],
    "module": "NodeNext",
    "rootDir": "./src",
    "resolveJsonModule": true,
    "allowJs": true,
    "sourceMap": true,
    "outDir": "./build",
    "removeComments": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "noImplicitAny": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"],
  "lib": ["esnext"],
  "ts-node": {
    "esm": true
  }
}
```
* Adding module syntax support for Node.js to `package.json`
```json
{
  "type": "module"
}
```
* Create a `src` folder where all source code is stored `mkdir src`

## Setting for development mode
* Installing packages `npm install --save-dev ts-node nodemon`
* Adding a setting for nodemon in the `nodemon.json` file
```json
{
  "watch": ["src"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "npx ts-node ./src/main.ts"
}
```
* Adding a script to `package.json`
```json
{
  "dev": "npx nodemon"
}
```

## Setting for publishing mode
* Installing packages `npm install --save-dev rimraf`
* Add 2 scripts to `package.json`
```json
{
   "start": "npm run build && node build/main",
   "build": "rimraf ./build && npx tsc"
}
```

## Setting up ESlint
* Installing packages `npm i -D eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser`
* Create `.eslintrc` at the root
```json
{
  "parser": "@typescript-eslint/parser",
  "extends": ["plugin:@typescript-eslint/recommended"],
  "parserOptions": { "ecmaVersion": 2018, "sourceType": "module" },
  "rules": {}
}
```
* Add 2 scripts to `package.json`
```json
{
  "lint": "npx eslint ./src",
  "format": "npx eslint ./src --fix"
}
```

## Prettier setting
* Installing package `npm i -D prettier`
* Add `.prettierrc` file
```json
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 120,
  "tabWidth": 2
}
```

## Husky setting
* Installing package `npm i -D husky`
* Add setting to `package.json` root
```json
{
  "husky": {
    "hooks": {
      "pre-commit": "npm run lint"
    }
  }
}
```