# ESLint Angular Setup  

This is a quick eslint setup that will allow you to easily lint your Angular code within Visual Studio Code.


For a new Angular Project (Angular will automatically install eslint and create an eslintrc file with recommended settings for Angular). 
In addition to eslint, we will also integrate with prettier to allow for more lightweight formatting rules. 
Linters are powerful and check for code quality, while a formatter just cares about styling. 

Here's how we can install this

```
npm install -g @angular/cli //Install the Angular CLI if you don't have it
ng new my-app //This will autocreate an eslint file, ignore this if you already have an app
cd my-app
//Start here for existing apps
npm install --save-dev --save-exact prettier
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
//If using tailwind you can npm install --save-dev prettier-plugin-tailwindcss
```

Now in your .eslintrc.json

```
{
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

Then you need to add plugin:prettier/recommended as the last extension in your .eslintrc.json:
```
{
  "extends": ["plugin:prettier/recommended"]
}
```

Now make sure you have the Visual Studio Code Microsoft Eslint extension

Now put these into your user settings JSON 
```
  "editor.formatOnSave": true, //Make you format on every save
  //You can also use editor.formatOnType
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint":true
  },
  "eslint.validate": [
    "javascript",
    "typescript",
    //if using react
    "javascriptreact",
    "typescriptreact",
  ],
  //You can also set formatters for each individual language
  "editor.defaultFormatter": "dbaeumer.vscode-eslint",
```

Your .eslintrc file should look similar to this 
```
{
  "root": true,
  "ignorePatterns": ["projects/**/*"],
  "overrides": [
    {
      "files": ["*.ts"],
      "parserOptions": {
        "project": ["**/tsconfig.json"],
        "createDefaultProgram": true
      },
      "extends": [
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates",
        "plugin:prettier/recommended"
      ],
      "rules": {
        "@angular-eslint/component-class-suffix": [
          "error",
          {
            "suffixes": ["Page", "Component"]
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ],
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ]
      }
    },
    {
      "files": ["*.html"],
      "extends": ["plugin:@angular-eslint/template/recommended"]
    }
  ]
}
```
You can now edit your .prettierrc file if you'd like, when switching between OSs you may find that you
need to add end of line auto. You can also add the tailwind plugin (adds a consistent order for your styles) and point your tailwind config to help with additional styling if you use tailwind.
```
{
    "semi": true,
    "tabWidth": 2,
    "singleQuote": false,
    "plugins": ["prettier-plugin-tailwindcss"],
    "tailwindConfig" : "./tailwind.config.js",
    "endOfLine" : "auto"
}
```
Now you should get linting warnings, and Eslint and Prettier will fix any issues on file save.

### Common Problems
If you notice a change, and then then the file immedialty changes back, make sure your VSCode did not try to add their own default formatter.


