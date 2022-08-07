# React Native EsLint Prettier for Expo.
Enforcing Consistent and Error Free Code in an Expo React Native Project with TypeScript. 
Tutorial Resume in this [link](https://justinnoel.dev/2020/07/20/enforcing-consistent-and-error-free-code-in-an-expo-react-native-project-with-typescript/).


> Improve your team's code quality and efficiency by using ESLint, Prettier to automate formatting and consistency checks.

## Configure ESLint for TypeScript
First, we need to get ESLint configured to support TypeScript:

```sh

npm add --dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin

```

Now, let's add an .eslintrc file in our project's root directory so that it looks like this:
```
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ]
}
```

Next, we'll need to add an .eslintignore file to ensure our linter doesn't go to crazy and start linting every directory in our project:
```
node_modules
dist
.expo
.expo-shared
web-build
```

Now, we'll need to add a lint script to our package.json:
```
{
...,
"lint": "eslint . --ext .ts,.tsx,.js,.jsx,.json",
"lint-and-fix": "eslint . --ext .ts,.tsx,.js,.jsx,.json --fix",
...
}
```
The two script above will let you npm run lint or ```npm run lint-and-fix``` to see/fix all the linting errors in your project.

## Installing and Configuring Prettier
To install Prettier, run this command

```
yarn add --dev prettier
```

Now, we need to add the magic sauce to keep all your files formatted just the way your team likes (after arguing for a few days).

Add a .prettierrc file to look something like this:
```
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": false,
  "printWidth": 80
}
```

We also need to keep Prettier and ESLint from whacking each other over the head. Modify your .eslintrc file to look like this:
```
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": ["react", "@typescript-eslint", "prettier"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ]
}
```

Finally, add a script to package.json to run prettier on all your existing files:

```
"prettier-format": "prettier --config --write \"src/**/*.{js,jsx,tsx,ts}\""
```


Now, run ```npm run prettier-format``` and watch it automagically format many of the files in our project. Just like that, we've updated the formatting for every file in the project. Now, if a team member modifies one of those files days or weeks later, their PR won't be polluted with tons of formatting changes that hide their real changes.

## VSCode Configs 
All settings for VSCode are in ```.vscode/settings.json``` file.

> OBS: Add comment ```// eslint-disable-next-line no-undef``` for lines ignore validation in code.
