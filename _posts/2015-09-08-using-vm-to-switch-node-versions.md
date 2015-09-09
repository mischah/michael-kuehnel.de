---
layout: post
lang: en_GB
title:  "Switch Node.js versions with the Node Version Manager (nvm)"
date:   2015-09-08 23:00:00
category: Node.js
tags: "Quick Tip, Node.js, Versions, homebrew, npm"
image: "/assets/img/nodejs-logo.svg"
excerpt: "Sure you can just use homebrew to update your Node.js installation when there are new releases. It’s in fact very handy to do so. But beside the quirk when it comes to updating npm there is a method which makes switching Node.js version even easier. This became more important since the stable release of Node 4.0 which I like to use. But I have to be able to use a different Node version just in case thinks break with Node 4.0."
disqusIdentifier: 2015-09-08-using-vm-to-switch-node-versions
---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          {{page.excerpt}}
        </p>
    </div>
</div>



# uninstall node via homebrew

First we could check which version of node we are using:

```bash
$ node --version
v0.12.1
```

Let’s get rid of this version:

```bash
$ brew uninstall node
Uninstalling /usr/local/Cellar/node/0.12.1...
node 0.10.26, 0.10.28, 0.10.35, 0.10.35_2, 0.12.0 are still installed.
Remove them all with `brew uninstall --force node`.
```

… and old versions we still have in the cellar:

```bash
$ brew uninstall --force node
Uninstalling node...
```



# Installing the Node Version Manager (nvm) 

I prefer installing it via homebrew:

```bash
$ brew update && brew upgrade
$ brew install nvm
```

Please have a look at <https://github.com/creationix/nvm> in case you would like to do a manual install.

Either way you have to add a few lines to your `~/.bash_profile`, `~/.zshrc` or `~/.profile`. In case of the homebre installation it is:

```bash
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
```

# Using nvm

To download, compile, and install the latest v0.12.x release of node, do this:

```bash
nvm install 4.0
```

Let’s install the latest v.0.12.x release in addition:

```bash
nvm install 0.12
```

You will use the latest installed version automatically after installation.
Switching version is easy as:

```bash
nvm use 0.4
```


In place of a version pointer like "4.0", you can use the special default aliases like "stable" and "unstable":

```bash
nvm install stable
nvm install unstable
nvm use stable
```

## Version settings via config file

You could place a `.nvmrc` file in your home directory to define your prefered version globally. For example:

```bash
0.40
```

This can be overidden by placing other `.nvmrc` files in project root directories.

---

I guess that’s all you need to know to start using nvm. 
Make sure to checked out the [project on Github](https://github.com/creationix/nvm) in case you like to dig deeper.



