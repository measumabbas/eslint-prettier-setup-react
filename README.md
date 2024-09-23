# Step-by-Step Guide: Adding ESLint and Prettier to a React Vite Project
In this guide, we will walk through setting up ESLint and Prettier for a React Vite project to enforce consistent coding standards and automatically format your code. Additionally, we’ll use the eslint-plugin-sort-imports-es6-autofix plugin to automatically sort imports, which improves readability and helps maintain a clean code structure.

By the end of this guide, your React Vite project will be set up with ESLint and Prettier, ensuring your code is clean, consistent, and follows best practices.

## Step 1: Initialize a React Vite Project
If you haven't already created a Vite project, start by setting up a new one
```bash
npm create vite@latest my-vite-app --template react
```
Open your project directory 
```bash
cd my-vite-app
```
Then install the dependencies

```bash
npm install
```
## Step 2: Install ESLint and Prettier
```bash
npm install --save-dev eslint prettier eslint-config-prettier eslint-plugin-prettier eslint-plugin-react eslint-plugin-unused-imports @eslint/js eslint-plugin-sort-imports-es6-autofix
```
## Step 3: Configure Eslint by adding rules
In the root of your project, there will be a file named eslint.config.mjs, if not then create a eslint.config.mjs file and add the following configuration:
```javascript
import autoPrefix from 'eslint-plugin-sort-imports-es6-autofix';
import globals from 'globals';
import pluginJs from '@eslint/js';
import pluginReact from 'eslint-plugin-react';
import prettier from 'eslint-plugin-prettier';
import tseslint from 'typescript-eslint';
import unusedImports from 'eslint-plugin-unused-imports';
export default [
  { files: ['**/*.{js,mjs,cjs,ts,jsx,tsx}'] },
  { files: ['**/*.js'], languageOptions: { sourceType: 'commonjs' } },
  { languageOptions: { globals: globals.browser } },
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
  pluginReact.configs.flat.recommended,

  {
    plugins: {
      'unused-imports': unusedImports,
      'sort-imports-es6-autofix': autoPrefix,
      prettier: prettier,
    },
    rules: {
      'react/react-in-jsx-scope': 'off',
      'no-console': ['error', { allow: ['warn', 'error'] }],
      '@typescript-eslint/no-unused-vars': 'error',
      'unused-imports/no-unused-imports': 'error',
      'unused-imports/no-unused-vars': [
        'warn',
        {
          vars: 'all',
          varsIgnorePattern: '^_',
          args: 'after-used',
          argsIgnorePattern: '^_',
        },
      ],
      'sort-imports-es6-autofix/sort-imports-es6': [
        2,
        {
          ignoreCase: false,
          ignoreMemberSort: false,
          memberSyntaxSortOrder: ['none', 'all', 'multiple', 'single'],
        },
      ],
      'prettier/prettier': [
        'error',
        {
          singleQuote: true,
          jsxSingleQuote: true,
          tabWidth: 2,
          endOfLine: 'auto',
        },
      ],
      curly: 'error',
    },
  },
];

```

## Step 5: Update package.json Scripts, add the following script if its not in the scripts
```json
"scripts": {
  "lint": "eslint ."
}
```

## step 6: Install eslint and prettier
You can install eslint and prettier extensions from vscode extensions

## step 7 : VsCode Settings

If you can't see eslint as a formatter then create a .vscode folder inside this folder create a file named settings.json add the following settings 
```json
{
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true,
    "[javascript]": {
    "editor.formatOnSave": false
    },
    "[javascriptreact]": {
    "editor.formatOnSave": false
    },
    "eslint.alwaysShowStatus": true,
    "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
    ],
    "prettier.useTabs": true,
    "prettier.jsxSingleQuote": false,
    "prettier.tabWidth": 2,
    "prettier.arrowParens": "avoid",
    "prettier.singleQuote": true
    }
```
