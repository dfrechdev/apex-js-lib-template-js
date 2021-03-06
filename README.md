# apexjs-template-js-lib

[![npm](https://img.shields.io/npm/v/apexjs-template-js-lib.svg?style=flat-square)](https://www.npmjs.com/package/apexjs-template-js-lib) [![Travis (.org) branch](https://img.shields.io/travis/dfrechdev/apexjs-template-js-lib/master.svg?style=flat-square)](https://travis-ci.org/dfrechdev/apexjs-template-js-lib) [![David](https://img.shields.io/david/dfrechdev/apexjs-template-js-lib.svg?style=flat-square)](https://github.com/dfrechdev/apexjs-template-js-lib/blob/master/package.json) [![NpmLicense](https://img.shields.io/npm/l/apexjs-template-js-lib.svg?style=flat-square)](https://github.com/dfrechdev/apexjs-template-js-lib/blob/master/LICENSE)

This is the default JavaScript template for [create-apex-js-app][mainproject] and is used to bootstrap a project that creates a JavaScript library for use in Oracle Apex. By using a standardized way to build your JavaScript code for APEX, your source code is transformed during the build process in the following ways:

-   all JavaScript code is bundled into one file
-   all JavaScript code is transpiled to ES5 syntax
-   language features that are not part of ES5 and cannot be transpiled (eg. Promise, Map, Set, ...) and are use in the code are polyfilled
-   the target environment (supported browsers) of your build can be set in one place and define the result of the transpilation and polyfills
-   in development mode, source maps are created inline within the bundle file to ease debugging in the browsers development console
-   ESLint statically checks the source code with the `eslint:recommended` rule set
-   CSS files that are imported into the JavaScript source files are extracted with vendor prefixes added into a separate CSS file
-   all transformed code is minimized and shortened
-   ability to write unit tests with [ava][ava] that run during a build

The result of the build process is a JavaScript bundle file, that contains the transpiled source code with the dependencies and required polyfills, as well as a CSS file that includes the code of all imported CSS files. The bundled JavaScript file exposes your source code in one library variable to your APEX application.

All default settings can be easily changed according to your needs, after you have created your app.

## How to use this template

To create your JavaScript app for APEX, run the following command in your shell with the app name replaced (the app name may only include letters, numbers, underscores and hashes):

```bash
npx create-apex-js-app <app-name>
```

Please check the documentation of the package [create-apex-js-app][mainproject] for more details. This template is the default template for the generator package, therefore it does not need to be specified during the creation.

## Questions during the creation of your library

-   **Library code**: This will be the code that is exposed on your APEX page and contains all of your source code. As with the library name, the library code may only include letters, numbers, underscores and hashes. By default, your library name is used for the library code as well.

-   **Initial version**: Define the initial version of your library. The version needs to follow the [semantic versioning][semver] rules. The default is version 1.0.0.

-   **output format**: The output format defines the module you want to create. By default, the library is created as an IIFE (Immediately Invoked Function Execution), which is s good fit for browsers. If you want to use your library in other modules/libraries however, you might want to choose another format.

## How to write your library

The generated library contains a `src` folder with a file called `main.js`. This is the default entry point for the bundle generation and the place where your JavaScript code should go. You can import any node package that you have installed or local modules that you have created in separate files. All exported variables, objects or functions within the main.js file will be accessible in your library. Check the `examples` folder in your library to see how you can add your code.

## How to build your library

The build process transforms your code and stores the result in the `dist` folder of your library.To start the build process, issue one of the following commands from the root of your library:

### Create production bundle

```bash
npm run bundle
```

This will bundled your JavaScript code and CSS files for production. This includes transpilation, polyfilling, static code checking, as well as minifying and shortening (uglifying) of your code. By default, no source maps are created for your transformed code.

### Create development bundle

```bash
npm run bundle-dev
```

This will create bundle your Javascript code and CSS files as above, but without minifying and uglifying. But, for development source maps are added inline of your JS file.

### Run tests

```bash
npm run test
```
This will run all tests defined in the `tests` folder.

### Run script every change

All above scripts can also be run to watch and re-execute on every change:

```bash
npm run watch:bundle
npm run watch:bundle-dev
npm run watch:test
```

### Create documentation

```bash
npm run doc
```

This will create the documentation from the JSDoc comments in your source code.

### Run build

```bash
npm run build
```

This will run the tests, the production build and create the JSDoc documentation.

## Configuration

You can change your build to your needs by changing the following configuration files:

-   [package.json][packagejson]: Root configuration file of your project. Includes the name of your app, the exposed library code, the version of your app and many more.
-   [rollup.config.js][rollupconf]: Configuration file for the bundle process of your library
-   [.eslintrc.json][eslintconf]: Settings file for ESLint. By default the predefined [eslint:recommended][eslintrecommend] rules are used for ESlint. If you want to use another set, you can change it in this configuration file. The .eslintignore file in addition includes all the files that should be ignored by ESLint
-   [.prettierrc][prettierconf]: Rules for the Prettier extension in VSCode
-   [jsdoc.conf][jsdocconf]: Configuration file for documentation creation with JSDoc
-   [.babelrc][babelconf]

### Externals

Externals are parts of your app, that should not be included in your bundle, as they are already loaded on your page. With this template, the following libraries are set as externals:

#### apex

The apex JavaScript API is passed to your app as an argument when it is loaded. You therefore need to ensure, that your library is loaded after the apex library.

#### jQuery

The jQuery library is included in the apex library and can be referenced with `apex.jQuery`. Additionally, you can map `apex.jQuery` to the `$` variable in your files if you wish such as:

```javascript
const $ = apex.jQuery;
```

As you are working in your own namespace, it is safe to override the `$` variable. This way you can make sure that you always access the jQuery library from the apex library while being able to continue to use the `$` shortcut.

## Contribute

Found a bug? Have an idea? See [how to contribute][contributing].

## Author

Daniel Frech, 2018

## License

[MIT](LICENSE)

[contributing]: /CONTRIBUTING.md
[semver]: https://semver.org/
[mainproject]: https://github.com/dfrechdev/create-apex-js-app
[ava]: https://github.com/avajs/ava
[packagejson]: https://docs.npmjs.com/files/package.json
[babelconf]: https://babeljs.io/docs/en/config-files
[jsdocconf]: http://usejsdoc.org/about-configuring-jsdoc.html
[prettierconf]: https://github.com/prettier/prettier
[eslintconf]: https://eslint.org/docs/user-guide/configuring
[rollupconf]: https://rollupjs.org/guide/en
[eslintrecommend]: https://eslint.org/docs/rules/
