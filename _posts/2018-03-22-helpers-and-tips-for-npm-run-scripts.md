---
layout: post
lang: en_GB
title:  "Helpers and tips for npm run scripts"
date:   2018-03-22 23:30:00
category: Tooling
tags: "Tooling, npm scripts, helpers, cli, tips, watch"
image: ""
excerpt: "The purpose of this blog post is not to introduce using npm as a build tool. There are lots of good articles about the »what« and »why«. I like to present some hidden gems to improve your setup instead."
disqusIdentifier: 2018-03-22-helpers-and-tips-for-npm-run-scripts
---

{{page.excerpt}}

I’d like to point to [Why npm Scripts?](https://css-tricks.com/why-npm-scripts/) if you want to read an introduction to the benefits of using CLI tools via npm scripts in favor of a task runner like Gulp and their plugin eco system.

## Introduction

You can easily [run scripts](https://docs.npmjs.com/cli/run-script) using npm by adding them to the `"scripts"` field in package.json and run them with `npm run <script-name>`. Run `npm run` to see available scripts. Binaries of locally install packages are made available in the `PATH`, so you can run them by name instead of pointing to `node_modules/.bin/name`.

```json
{
	"name": "my-package",
	"scripts": {
		"lint": "eslint ."
	},
	"devDependencies": {
		"eslint": "^4.19.0"
	}
}
```

```bash
$ npm run lint
```

----

## Lifecycle scripts

npm comes with predefined [lifecyle scripts](https://docs.npmjs.com/misc/scripts) which are excuted under specific conditions in case they are defined in your package.json.

```json
{
  "name": "my-package",
  "scripts": {
    "prepublishOnly": "nsp check"
  },
  "devDependencies": {
    "nsp": "^3.2.1"
  }
}
```

This will be executed automatically before your npm package is published to the registry via `npm publish` to check for known vulnerabilties in your dependencies.

__Note: *prepublishOnly* is available since npm v4.0.0. See [npm docs](https://docs.npmjs.com/misc/scripts#deprecation-note).__

### »npm start« and »npm test«

`npm start` are also lifecycle scripts but aren’t executed automatically. 

```json
{
  "name": "my-package",
  "scripts": {
    "start": "node server.js",
    "test": "jest"
  },
  "devDependencies": {
    "jest-cli": "^22.4.2"
  }
}
```

Therefore they can be executed simply with:

```bash
$ npm test
$ npm start
```

### »pre« and »post« scripts

»pre« and »post« scripts are special lifecycle scripts which can be used to run scripts automatically in sequence.

```json
{
  "name": "my-package",
  "scripts": {
    "pretest": "eslint .",
    "test": "jest"
  },
  "devDependencies": {
    "eslint": "^4.19.0",
    "jest-cli": "^22.4.2"
  }
}
```

```bash
$ npm test
```

This will lint your files before running your tests. The tests will not run if linting fails, or more generally: the following script won’t be executed if one of the scripts running in sequence exits with an exit code other than 0.

__Note: »pre« and »post« scripts can also be used for your custom npm scripts. So `npm run foo` will also run `prefoo` and `postfoo` if defined.__

----

## Options for npm scripts

#### Passing options to used commands
 
You can pass options to the command you are using in your npm script by adding `-- --flag` like in the example below.
 
```json
{
  "name": "my-package",
  "scripts": {
    "lint": "xo",
    "lint:fix": "npm run lint -- --fix",
  }
}
```
 
Adding the `-- --fix ` option is like executing `xo --fix`.

### Silent option
 
`npm run` has a `--silent` option which is especially useful when combining npm scripts in npm scripts.
 
Imagine you have a setup for linting your JavaScript files like the following:
 
```json
{
  "name": "my-package",
  "scripts": {
    "lint": "xo",
    "lint:fix": "npm run lint --silent -- --fix",
  }
}
```
 
Using the --silent option reduces the output in the Terminal. See this [comparison](https://twitter.com/mkuehnel/status/957965749473210369).

----

## Helper packages

### Watch tasks 

There are several packages which enable running scripts when files changed. In my opinion [onchange](https://github.com/Qard/onchange) offers the best combination of ease of use and flexibility. 

```json
{
	"name": "my-package",
	"scripts": {
		"lint": "eslint src",
    "lint:watch": "onchange \"src/**/*.js\" -- npm run lint --silent"
	}
}
```

So `npm run lint:watch` will watch for changes in the file system and will automatically run eslint when a file changes.

### Get notified in error cases

[cli-error-notifier](https://github.com/micromata/cli-error-notifier) sends native desktop notifications when npm scripts fail.

```json
{
  "scripts": {
    "lint": "onerror \"eslint src\"",
  }
}
```

This is especially useful for watching files while developing in conjunction with `onerror`.

```json
{
  "scripts": {
    "lint": "eslint src",
    "lint:fix": "npm run lint --silent -- --fix",
    "lint:watch": "onchange \"src/**/*.js\" -- onerror \"npm run lint --silent\""
  }
}
```

### Run multiple scripts in parallel or serial

Using [npm-run-all](https://github.com/mysticatea/npm-run-all) offers the following advantages:

- can increase readability of the scripts section in your package.json via glob-like patterns
  Before:

  ```json
  npm run clean && npm run build:css && npm run build:js && npm run build:html
  ```

  After:
  
  ```json
  npm-run-all clean build:*
  ```
- compared to using `npm run foo & npm run bar`
  - running scripts in parallel works on Windows
  - multiple scripts which are listening to file changes can run parallel 

```json
{
  "scripts": {
    "start": "npm-run-all clean --parallel webpack:server lint:watch",
    "build": "npm-run-all security test clean webpack",
  }
}
```

----

## Using npx with locally installed dependencies instead of npm run scripts

npm [comes bundled](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) with `npx` (since v5.2.0) — a tool to execute package binaries. Which is great to use packages globally without the need to install them globally.

But it’s also pretty useful for locally installed dependencies in your project.

Each command called with `npx` is executed either from the local `node_modules/.bin` directory, or from a central cache, installing any packages needed in order to run a command.
 
```json
{
	"name": "my-package",
	"scripts": {
		"lint": "xo"
	},
	"devDependencies": {
		"xo": "^0.20.0"
	}
}
```

```bash
npx xo --fix
```

This executes the locally installed version of XO from `node_modules/.bin`.
