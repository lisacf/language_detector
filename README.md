*Use of this software is subject to important terms and conditions as set forth in the License file*

# App Scaffold

## Description
This repo contains a scaffold to help developers build [apps for Zendesk](https://developer.zendesk.com/apps/docs/apps-v2/getting_started) products. The App Scaffold includes many features to help you maintain and scale your app. Some of the features provided by the App Scaffold are listed below, however you don't need prior experience in any of these to be able to use the scaffold successfully.

- [ES6 (ES2015)](https://babeljs.io/docs/learn-es2015/)

_ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and the first update to the language since ES5 was standardized in 2009. Implementation of these features in major JavaScript engines is [underway now](http://kangax.github.io/compat-table/es6/)._

- [Handlebars](http://handlebarsjs.com/) templates

_Handlebars.js is an extension to the Mustache templating language created by Chris Wanstrath. Handlebars.js and Mustache are both logicless templating languages that keep the view and the code separated like we all know they should be._

- [SASS](http://sass-lang.com/) stylesheets

_Sass is an extension of CSS that adds power and elegance to the basic language. It allows you to use variables, nested rules, mixins, inline imports, and more, all with a fully CSS-compatible syntax._

- [Webpack](https://webpack.github.io/) module bundler

_Webpack is a module bundler. It packs CommonJs/AMD modules i. e. for the browser. Allows to split your codebase into multiple bundles, which can be loaded on demand._

- [Karma](http://karma-runner.github.io/) test runner

_The main goal for Karma is to bring a productive testing environment to developers. The environment being one where they don't have to set up loads of configurations, but rather a place where developers can just write the code and get instant feedback from their tests. Because getting quick feedback is what makes you productive and creative._

- [Jasmine](https://jasmine.github.io/) testing framework

_Jasmine is a behavior-driven development framework for testing JavaScript code. It does not depend on any other JavaScript frameworks. It does not require a DOM. And it has a clean, obvious syntax so that you can easily write tests._

## Getting Started

### Folder structure

The folder and file structure of the App Scaffold is as follows:

Name             | Description
---------------- | -----------
[`dist/`](#dist) | The folder in which webpack packages the built version of your app
[`lib/`](#lib)   | The folder in which the shims and files that make the scaffold work live
[`spec/`](#spec) | The folder in which all of your test files live
[`src/`](#src)   | The folder in which all of your source JavaScript, CSS, templates and translation files live
[`.eslintrc`](#eslintrc) | Configuration file for JavaScript linting
[`karma.conf.js`](#karmaconfjs) | Configuration file for the test runner
[`package.json`](#packagejson) | Configuration file for build dependencies
[`webpack.config.js`](#webpackconfigjs) | Configuration file that webpack uses to build your app

#### dist
The dist directory is the folder you will need to package when submitting your app to the marketplace. It is also the folder you will have to serve when using ZAT. It includes your app's manifest.json file, an assets folder with all your compiled JavaScript and CSS as well as HTML and images.

#### lib
The lib directory is where the source code for the app shims and compatibility methods live. While you may modify or remove this code as required for your app, doing so is not recommended for beginners.

#### spec
The spec directory is where all your tests and test helpers live. Tests are not required to submit/upload your app to Zendesk and your test files are not included in your app's package, however it is good practice to write tests to document functionality and prevent bugs.

#### src
The src directory is where your raw source code lives. The App Scaffold includes different directories for JavaScript, stylesheets, templates and translations.

#### .eslintrc
eslintrc is a configuration file for [ESLint](http://eslint.org). ESLint is a linting utility for JavaScript. For more information on how to configure ESLint see [Configuring ESLint](http://eslint.org/docs/user-guide/configuring).

#### karma.conf.js
karma.conf.js is a configuration file for [Karma](http://karma-runner.github.io). Karma is a JavaScript test runner. This file defines where your source and test files live. For more information on how to configure this file see [Karma - Configuration File](http://karma-runner.github.io/1.0/config/configuration-file.html).

#### package.json
package.json is a configuration file for [NPM](https://www.npmjs.com). NPM is a package manager for JavaScript. This file includes information about your project and its dependencies. For more information on how to configure this file see [package.json](https://docs.npmjs.com/files/package.json).

#### webpack.config.js
webpack.config.js is a configuration file for [webpack](https://webpack.github.io/). Webpack is a JavaScript module bundler. For more information about webpack and how to configure it see [What is webpack](http://webpack.github.io/docs/what-is-webpack.html).

### Setup
1. Clone or fork this repo
2. Run `npm install`

To run your app locally in Zendesk, you need the [Zendesk Apps Tools (ZAT)](https://github.com/zendesk/zendesk_apps_tools).

You'll also need to run a couple of command-line Node.js-based tools that are installed using `npm`. For a node module to be available from the command-line, it must be installed globally.

To setup these and other dependencies, run these commands:

```
gem install zendesk_apps_tools
npm install --global webpack foreman karma-cli
```

Note: Foreman was originally created as a Ruby tool. If you prefer, you can install it by `gem install foreman` instead.

### Migrating from v1
The master branch of this repo contains modules and sample code to help you migrate from a v1 app. For detailed documentation on how to migrate from a v1 app see our [Migrating to v2](https://developer.zendesk.com/apps/docs/apps-v2/migrating) guide on the Zendesk Developer Portal.

### Starting from scratch
If you're starting a v2 app from scratch you will need to check out the [from-scratch](https://github.com/zendesk/app_scaffold/tree/from-scratch) branch:

```
git checkout from-scratch && npm install
```

The from-scratch branch uses up-to-date versions of the libraries included with the App Scaffold and also removes the shims needed when migrating from v1. It also includes sample code to help you get started on v2. If you want to see the exact differences between the master and from-scratch branches click [here](https://github.com/zendesk/app_scaffold/compare/from-scratch).

### Running locally

_Note: the App Scaffold currently depends on zat v1.35.12 or greater._

Foreman allows you to easily run multiple processes in one tab. One process is `zat server`, which serves the app in a way that can be consumed by the host (eg Zendesk). The second is `webpack --watch` to rebuild the project whenever you save changes to a source file.

To run these processes, run

```
nf start
```

or run the individual commands from the Procfile in separate terminals.

Note: if you installed the Ruby version of foreman, you'll need to use `foreman start`.

#### Parameters and Settings

If you need to test your app with a `parameters` section in `dist/manifest.json`, foreman might crash with a message like:

> Would have prompted for a value interactively, but zat is not listening to keyboard input.

To resolve this problem, set default values for parameters or create a `settings.yml` file in the root directory of your app scaffold-based project, and populate it with your parameter names and test values. For example, using a parameters section like:

```json
{
  "parameters": [
    {
      "name": "myParameter"
    }
  ]
}
```

create a `settings.yml` containing:

```yaml
myParameter: 'some value!'
```

If you prefer to manually input settings every time you run foreman, edit the Procfile to remove the `--unattended` option from the server command.

## Testing

The App Scaffold is currently setup for testing with [Jasmine](http://jasmine.github.io/) (testing framework) and [Karma](https://karma-runner.github.io) (test runner). To run specs, run

```
karma start
```

Specs live under the `spec` directory and can be configured by editing the `karma.conf.js` file.

## Deploying

To check that your app will pass the server-side validation check, run

```
zat validate --path=./dist
```

If validation is successful, you can upload the app into your Zendesk account by running

```
zat create --path=dist
```

To update your app after it has been created in your account, run

```
zat update --path=dist
```

Or, to create a zip archive for manual upload, run

```
zat package --path=dist
```

taking note of the created filename.

For more information on the Zendesk Apps Tools please see the [documentation](https://developer.zendesk.com/apps/docs/apps-v2/getting_started#zendesk-app-tools).

## External Dependencies
External dependencies are defined in the  [`webpack.config.js`](https://github.com/zendesk/app_scaffold/blob/master/webpack.config.js) as `externalAssets`. This ensures these dependencies are included on your app's `index.html` as well as in the test suite.

## Owners
The project is maintained by the Quokka / Vegemite team, ping us with [@zendesk/vegemite on GitHub](https://github.com/orgs/zendesk/teams/vegemite).

## Contribute
* Put up a PR into the master branch.
* CC and get a +1 from @zendesk/vegemite.

## Bugs
Submit Issues via [GitHub](https://github.com/zendesk/app_scaffold/issues/new) or email support@zendesk.com.

## Useful Links
Links to maintaining team, confluence pages, Datadog dashboard, Kibana logs, etc
- https://developer.zendesk.com/
- https://github.com/zendesk/zendesk_apps_tools
- https://webpack.github.io

## Copyright and license
Copyright 2016 Zendesk

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License.

You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
