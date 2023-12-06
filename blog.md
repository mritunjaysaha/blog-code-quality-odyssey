## Hi everyone! Let's dive into the powerful duo of ESLint and Prettier. If you've ever found yourself grappling with maintaining code quality or wrestling with consistent code formatting, this comprehensive guide is made for you.

In the fast-paced world of software development, ensuring clean and error-free code is paramount. ESLint and prettier, two industry-standard tools that provide the perfect solution. ESLint enables you to catch potential bugs, enforce coding conventions, and maintain consistent code quality. Meanwhile, Prettier takes care of code formatting, ensuring your code is beautiful and easy to read.

By using these two tools, you can supercharge your development workflow, saving precious time and effort from endless debates over code style and tedious manual formatting. With ESLint and Prettier, you have the tools to create code that is both elegant and maintainable.

This guide endeavors to lead you through the foundational aspects of ESLint and Prettier, delving into their functionalities, configuration options, plugins, and optimal methodologies. Whether you possess extensive experience as a developer or are embarking on your coding journey, our aim is to furnish you with the requisite knowledge and abilities to effectively harness the capabilities of these robust tools.

### How to implement ESLint and Prettier?

Cool, so now Let's see ESLint and Prettier in action. First, let's create our project by running **npx create-next-app@latest eslint-and-prettier** . Then vite will prompt you to enter the package name. Set the package name as you like. We'll name it **eslint-and-prettier**.

In the root directory of our react project we will find **.eslintrc.json** file with following contents

Now that our project's good to go, let's kick things off by adding some extra plugins for **ESLint**.

### How to install ESLint

To install ESLint and the necessary packages and plugins for configuring ESLint in your project, run the following command:

`npm i -D eslint-config-airbnb-base eslint-config-airbnb-typescript eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-prettier eslint-plugin-react eslint-plugin-simple-import-sort eslint-plugin-unused-imports eslint-plugin-spellcheck`

Each plugin is used for a specific purpose:

<ol>

<li>
<b>eslint-config-airbnb-base</b>: This is a preset configuration for ESLint provided by the Airbnb style guide. It includes a set of rules and recommended configurations that promote best practices for JavaScript development.
</li>

<li>
<b>eslint-config-airbnb-typescript</b>: Similar to eslint-config-airbnb-base, this preset configuration is specifically designed for projects using TypeScript. It extends the Airbnb base configuration and adds TypeScript-specific rules.
</li>

<li>
<b>eslint-config-prettier</b>: Prettier is a code formatter that helps enforce consistent code style. However, Prettier and ESLint have overlapping rules. eslint-config-prettier disables all ESLint rules that might conflict with Prettier's formatting rules, allowing them to work together seamlessly.
</li>

<li>
<b>eslint-plugin-import</b>: This plugin enhances ESLint's import/export rules. It provides additional validations for import statements, module resolution, and enforcing correct file extensions.
</li>

<li>
<b>eslint-plugin-jsx-a11y</b>: This plugin provides accessibility rules for JSX elements. It helps ensure that your React components are usable and accessible to users with disabilities.
</li>

<li>
<b>eslint-plugin-prettier</b>: This plugin integrates Prettier into ESLint. It formats code according to Prettier's rules by reporting any inconsistencies as ESLint errors.
</li>

<li>
<b>eslint-plugin-react-hooks</b>: This plugin provides rules and warnings specifically for React hooks, such as enforcing the correct usage of hooks like useState and useEffect.
</li>

<li>
<b>eslint-plugin-simple-import-sort</b>: This plugin offers an alternative approach to sorting imports. It provides rules for organizing and sorting import statements based on their category and prevents unused imports.
</li>

<li>
<b>eslint-plugin-unused-imports</b>: This plugin detects and reports unused import statements in your code. It helps keep your imports clean and free from unnecessary dependencies.
</li>

<li>
<b>eslint-plugin-spellcheck</b>: This plugin provides spell-checking capabilities for your JavaScript and TypeScript code. It helps catch misspelled words in comments, strings, and identifiers, allowing you to maintain code with accurate spelling.
</li>

</ol>

We're updating the `.eslintrc.cjs` file to include additional configurations for **JavaScript** and **TypeScript** development.

For **JavaScript**, we're extending it with **airbnb-base** to follow industry best practices.

Moving on to **TypeScript**, we're setting up configurations to enhance code quality specifically for TypeScript projects.

Additionally, we're incorporating **plugin:prettier/recommended**. This integration combines ESLint's rules with Prettier's formatting capabilities to detect code inconsistencies and ensure consistent formatting.

Below is the updated structure of your `.eslintrc.cjs` file after extending the configurations.

```js
// .eslintrc.json
{
  extends: [
    "airbnb-base",
    "next/core-web-vitals", // Needed to avoid warning in next.js build: 'The Next.js plugin was not detected in your ESLint configuration'
    "plugin:prettier/recommended",
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react-hooks/recommended"
    ],
  parser: '@typescript-eslint/parser',
  parserOptions: { ecmaVersion: 'latest', sourceType: 'module' },
  plugins: ['react-refresh'],
  rules: {
    'react-refresh/only-export-components': 'warn',
  },
};
```

Prepare yourself for the next step of our adventurous journey, brave explorer! We shall now update the rules property in your **.eslintrc.json** file to enforce code style and uphold the highest standards of quality.

Behold the magnificent transformation of your **.eslintrc.json** file, infused with the wisdom of countless battles fought by seasoned developers:

```js
// .eslintrc.json
module.exports = {
  env: { browser: true, es2020: true },
  extends: [
    'airbnb-base',
    'plugin:prettier/recommended',
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react-hooks/recommended',
  ],
  parser: '@typescript-eslint/parser',
  parserOptions: { ecmaVersion: 'latest', sourceType: 'module' },
  plugins: ['react-refresh'],
  rules: {
    'react-refresh/only-export-components': 'warn',
    'no-param-reassign': 1,
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        endOfLine: 'auto',
      },
    ],
    'react/react-in-jsx-scope': 0,
    '@typescript-eslint/no-empty-function': 1,
    'spaced-comment': 'error',
    quotes: ['error', 'single'],
    '@typescript-eslint/restrict-template-expressions': 1,
  },
};
```

Armed with these mighty rules and settings, your code shall be fortified against errors and imbued with unparalleled style. Brace yourself for their power:

<ol>
<li>
<b>no-param-reassign : 1</b>: Enables the rule that prohibits reassigning function parameters. With this setting, any attempts to modify function parameters will trigger an error. Reassigning function parameters is considered a bad practice as it can lead to confusion and unintended side effects.
</li>

<li>
<b>prettier/prettier: [...]</b>: Configures the Prettier code formatter integration with ESLint. The provided settings specify that single quotes should be used for strings (singleQuote: true), and the line endings should be automatically detected based on the file (endOfLine: "auto").
</li>

<li>
<b>react/react-in-jsx-scope: 0</b>: Disables the rule that enforces importing the React object in every JSX file. This rule is specific to React projects and ensures that the React object is always in scope when using JSX syntax.
</li>

<li>
<b>@typescript-eslint/no-empty-function: 1</b>: Enables the rule that disallows empty function implementations. With this setting, empty function definitions will trigger an error. It is generally considered good practice to provide meaningful implementation for functions to avoid potential issues.
</li>

<li>
<b>spaced-comment: error</b>: Enforces a space after the start of a comment. This rule helps improve code readability by ensuring consistent spacing in comments.
</li>

<li>
<b>quotes: ["error", "single"]</b>: Enforces the use of single quotes for string literals. This rule ensures consistent quotation style throughout the codebase.
</li>

<li>
<b>@typescript-eslint/restrict-template-expressions: 1</b>: Enables the rule that checks for potentially unsafe expressions in template literals. With this setting, if a potentially unsafe expression is detected within a template literal, it will trigger an error. This rule helps prevent potential bugs and security vulnerabilities.
</li>
</ol>

Get ready to supercharge your **TypeScript** project! We're about to unleash a set of powerful configurations designed exclusively for TypeScript files. Brace yourself as we set specific rules and wield cutting-edge plugins tailored to TypeScript's unique requirements. But we won't stop there. We'll boldly extend various ESLint configurations, going above and beyond to ensure pristine code quality. And just to push the boundaries even further, we'll enforce additional custom rules, leaving no room for mediocre code. Embrace the boldness and elevate your TypeScript development to new heights!

```js
// eslintrc.json
{
  // Configuration for JavaScript files
  "extends": [
    "airbnb-base",
    "next/core-web-vitals", // Needed to avoid warning in next.js build: 'The Next.js plugin was not detected in your ESLint configuration'
    "plugin:prettier/recommended"
  ],
  "rules": {
    "no-param-reassign": 1,
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true,
        "endOfLine": "auto"
      }
    ],
    "react/react-in-jsx-scope": 0,
    "@typescript-eslint/no-empty-function": 1,
    "spaced-comment": "error",
    "quotes": ["error", "single"],
    "@typescript-eslint/restrict-template-expressions": 1
  },
  "overrides": [
    // Configuration for TypeScript files
    {
      "files": ["**/*.ts", "**/*.tsx"],
      "plugins": ["@typescript-eslint", "unused-imports", "simple-import-sort"],
      "extends": [
        "airbnb-typescript",
        "next/core-web-vitals",
        "plugin:prettier/recommended"
      ],
      "parserOptions": {
        "project": "./tsconfig.json"
      },
      "rules": {
        "prettier/prettier": [
          "error",
          {
            "singleQuote": true,
            "endOfLine": "auto"
          }
        ],
        "react/destructuring-assignment": "off", // Vscode doesn't support automatically destructuring, it's a pain to add a new variable
        "react/require-default-props": "off", // Allow non-defined react props as undefined
        "react/jsx-props-no-spreading": "off", // _app.tsx uses spread operator and also, react-hook-form
        "react-hooks/exhaustive-deps": "off", // Incorrectly report needed dependency with Next.js router
        "@next/next/no-img-element": "off", // We currently not using next/image because it isn't supported with SSG mode
        "@typescript-eslint/comma-dangle": "off", // Avoid conflict rule between Eslint and Prettier
        "@typescript-eslint/consistent-type-imports": "error", // Ensure `import type` is used when it's necessary
        "no-restricted-syntax": [
          "error",
          "ForInStatement",
          "LabeledStatement",
          "WithStatement"
        ], // Overrides Airbnb configuration and enable no-restricted-syntax
        "import/prefer-default-export": "off", // Named export is easier to refactor automatically
        "simple-import-sort/imports": "error", // Import configuration for `eslint-plugin-simple-import-sort`
        "simple-import-sort/exports": "error", // Export configuration for `eslint-plugin-simple-import-sort`
        "@typescript-eslint/no-unused-vars": "off",
        "unused-imports/no-unused-imports": "error",
        "unused-imports/no-unused-vars": [
          "error",
          { "argsIgnorePattern": "^_" }
        ]
      }
    }
  ]
}
```

Let's breakdown down the configuration:

<ol>
<li>
<b>files: ["**/*.ts", "**/*.tsx"]:</b> Specifies that the configuration applies to TypeScript files with the .ts and .tsx extensions.
</li>

<li>
<b>plugins: [...]</b>: Specifies the list of plugins used in this configuration. These plugins include @typescript-eslint, unused-imports, tailwindcss, and simple-import-sort.

</li>

<li>
<b>extends: [...]</b>: Extends the ESLint configurations for TypeScript and related frameworks. It includes plugin:tailwindcss/recommended, airbnb-typescript, next/core-web-vitals, and plugin:prettier/recommended. These configurations provide a set of predefined rules and settings tailored for specific environments.
</li>

<li>
<b>parserOptions: { "project": "./tsconfig.json" }</b>: Configures the parser options for TypeScript files, specifying the location of the tsconfig.json file. This helps ESLint understand TypeScript-specific syntax and type information.
</li>

<li>
<b>rules: { [...] }</b>: Defines specific rules and their configurations for TypeScript files. Here are some notable rules and their settings:

<ul>
<li>
<b>react/destructuring-assignment: "off"</b>: Turns off the rule that enforces destructuring assignment for React components.
</li>

<li>
<b>react/require-default-props: "off"</b>: Allows non-defined React props to be undefined.
</li>

<li>
<b>react/jsx-props-no-spreading: "off"</b>: Allows spreading props in JSX components.
</li>

<li>
<b>react-hooks/exhaustive-deps: "off"</b>: Disables exhaustive dependency checking for React hooks.
</li>

<li>
<b>@typescript-eslint/comma-dangle: "off"</b>: Disables the rule related to trailing commas in TypeScript.
</li>

<li>
<b>@typescript-eslint/consistent-type-imports: "error"</b>: Enforces consistent usage of import type in TypeScript when necessary.
</li>

<li>
<b>no-restricted-syntax: [...]</b>: Overrides Airbnb configuration and enables the rule that restricts certain types of syntax, such as ForInStatement, LabeledStatement, and WithStatement.
</li>

<li>
<b>import/prefer-default-export: "off"</b>: Allows named exports instead of preferring default exports.
</li>

<li>
<b>simple-import-sort/imports: "error"</b> and <b>simple-import-sort/exports: "error"</b>: Enforce a specific import and export order using eslint-plugin-simple-import-sort.
</li>

<li><b>@typescript-eslint/no-unused-vars: "off"</b> and <b>unused-imports/no-unused-imports: "error"</b>: Turn off the default TypeScript rule for unused variables and use the unused-imports plugin to enforce unused import detection.</li>

<li>
<b>unused-imports/no-unused-vars: [...]</b>: Configures the unused-imports plugin to ignore variables that start with an underscore (\_).
</li>

<li>
<b>spellcheck/spell-checker</b>: This is the name of the rule provided by the <b>eslint-plugin-spellcheck</b> plugin. It is configured to check the spelling of words in <b>comments</b>, <b>strings</b>, and <b>identifiers</b>.

<ul>
    <li>
        <b>error</b>: This indicates that if a misspelled word is found, it will be reported as an error.
    </li>
    <li>
    <b>Configuration object</b>: The configuration object within the array provides additional settings for the spell-checker rule:
        <ul>
            <li>
                <b>"comments": true</b>: Enables spell-checking in comments.
            </li>
            <li>
                <b>"strings": true</b>: Enables spell-checking in strings.
            </li>
            <li>
                <b>"identifiers": true</b>: Enables spell-checking in identifiers.
            </li>
            <li>
                <b>"lang": "en_US"</b>: Specifies the language for spell-checking. In this case, it is set to American English.
            </li>
            <li>
                <b>"skipWords": ["some", "specific", "words"]</b>: An array of words to skip from spell-checking. You can add specific words that you want to exclude from being checked.
            </li>
            <li>
                <b>"skipIfMatch": ["regex"]</b>: An array of regex patterns to skip from spell-checking. You can specify regular expressions to match words that should be skipped.
            </li>
            <li>
                <b>"minLength": 3</b>: Sets the minimum word length to check. Words shorter than this length will not be checked for spelling.
            </li>
        </ul>
    </li>
</ul>

</li>

</ul>

</li>
</ol>

As per the new [**React** documentation](https://react.dev/learn/start-a-new-react-project), react recommends using **Next.js** as one of the frameworks for react applications. If we are using **Next.js** then we'll have to add **next/core-web-vitals**. It is needed to avoid warning in next.js build: **'The Next.js plugin was not detected in your ESLint configuration'**. For this plugin we need **eslint-config-next** package.

### Setting up Prettier

Prettier is a code formatter that helps maintain consistent code style and formatting in projects. We will add a **.prettierrc** which will have the configuration for prettier code formatter.

```json
{
  "semi": true,
  "tabWidth": 2,
  "printWidth": 80,
  "singleQuote": true,
  "trailingComma": "all",
  "jsxSingleQuote": true,
  "bracketSpacing": true
}
```

This configuration enforces the following formatting rules:

<ol>
<li><b>semi</b>: Adds semicolons at the end of statements.</li>
<li>
<b>printWidth</b>: Wraps lines that exceed 80 characters.
</li>
<li><b>singleQuote</b>: Uses single quotes for string literals.</li>
<li><b>trailingComma</b>: Adds trailing commas in arrays and objects. The value "all" enforces trailing commas wherever possible.</li>
<li><b>jsxSingleQuote</b>: Uses single quotes for JSX attributes.</li>
<li><b>bracketSpacing</b>: Adds spaces inside object literals.</li>
</ol>

Let's add some scripts in the package.json file to run prettier on all the files in the project.

```json
"format": "prettier --write \"src/**/*.+(js|jsx|ts|tsx)\"",
```

The final scripts in the package.json will look as follows

```json
"scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
    "format": "prettier --write \"src/**/*.+(js|jsx|ts|tsx)\""
}
```

Here is the GitHub [repo](https://github.com/mritunjaysaha/blog-code-quality-odyssey) for you to try it out!!!
