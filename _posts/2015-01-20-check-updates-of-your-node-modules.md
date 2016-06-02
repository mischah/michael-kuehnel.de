---
layout: post
lang: en_GB
title:  "Quick Tip: Updating your node modules is easy as »1, 2, 3«"
date:   2015-01-20 14:00:00
category: npm
tags: "Quick Tip, npm, Node.js, update"
image: "/assets/img/npm-logo.svg"
excerpt: "It might be a »no-brainer« in case you are working within the Node.js environment for a while. But I used to ask myself how to figure out if there are updates to my dependencies / devDependencies which are beyond the patch-level updates which are »automatically« installed via the definition within my `package.json`. Because I don’t like to check possible updates separately for every module I’m using in my project."
disqusIdentifier: 2015-01-20-check-updates-of-your-node-modules
---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          {{page.excerpt}}
        </p>
    </div>
</div>

Fortunately there is a node module which can handle that for all dependencies within your project and even all your globale modules. It’s called [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) and will also update your `package.json` file if you like to. So updating becomes »fun« again :smile:

Using this is pretty straight forward. First you need to install the package globally with:

```bash
npm install -g npm-check-updates
```

Then use the modules cli without any option to check available updates within your projects root directory:

```bash
npm-check-updates
```

This will show you all possible updates without changing anything:

```bash
"superb" can be updated from ^1.0.5 to ^1.1.1 (Installed: 1.0.5, Latest: 1.1.1)
"mocha" can be updated from ^2.0.1 to ^2.1.0 (Installed: 2.0.1, Latest: 2.1.0)
"should" can be updated from ^4.4.2 to ^4.6.1 (Installed: 4.4.2, Latest: 4.6.1)

Run 'npm-check-updates -u' to upgrade your package.json automatically
```

If you like to upgrade your projects `package.json` file just make use of the `-u` option as mentioned in the output above and fire:

```bash
npm install
```

afterwards. And :boom: … all updates will land on your machine and you’re done.

See the [README](https://www.npmjs.com/package/npm-check-updates) for more options.
