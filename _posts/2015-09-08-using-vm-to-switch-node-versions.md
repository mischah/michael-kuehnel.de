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

## Update from June 2, 2016

* Update versions numbers in examples
* Add info about [getting version infos](#so-many-versions-flushed)
* Add note about [potential problems with linking global packages](#potential-problems-with-linking-global-packages)
* Complete info about handling of [globally installed packages](#globally-installed-packages)

---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          {{page.excerpt}}
        </p>
    </div>
</div>



# Uninstall node via homebrew

First we could check which version of node we are using:

```bash
$ node -v
v5.5.0
```

Let’s get rid of this and older versions in the cellar of homebrew:

```bash
$ brew uninstall --force node
Uninstalling node...
```

## Potential problems with linking global packages 

Double check if there still is a `node_modules` directory in `/usr/local/lib` holding your globally installed packages. Do yourself a favor and remove that to prevent possible issues with linking globale packages via `npm link`.

# Installing the Node Version Manager (nvm) 

I prefer installing it via homebrew:

```bash
$ brew update
$ brew install nvm
```

Please have a look at <https://github.com/creationix/nvm> in case you would like to do a manual install.

Either way you have to add a few lines to your `~/.bash_profile`, `~/.zshrc` or `~/.profile`. In case of the homebrew installation it is:

```bash
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
```

# Using nvm

To download, compile, and install the (currently) latest v6.x.x release of node, do this:

```bash
nvm install 6
```

Let’s install the latest v5.x.x release in addition:

```bash
nvm install 5
```

You will use the latest installed version automatically after installation.
Switching version is easy as:

```bash
nvm use 6
```


In place of a version pointer like "6", you can use the special default aliases like "stable" and "unstable":

```bash
nvm install stable
nvm install unstable
nvm use stable
```

## Globally installed packages

Please note that you have to install global packages with every node version your are using with nvm.

>Another day, another Node.js release" 

This is something you want to automate since releases of Node.js are pretty frequent (for a good reason). Thankfully nvm offers to ways to accomplish that.

# Reinstall during install

The easiest one is to take care of that after during installation of a new node version with:

```bash
nvm install node --reinstall-packages-from=node
```

This will install the latest release and reinstall the globally installed packages from the predecessor.

You also can use more explicit versions like this:

```bash
nvm install 6.2 --reinstall-packages-from=6.0
```

# Reinstall later

You can »transfer« your global packages from one version to another at any given time. Just use:

```bash
nvm reinstall-packages <version>
```

This will reinstall global packages contained in `<version>`  to the current version in use.

## Setting a default version

You need to set a default version if you dont want to be surprised by switched versions with every opened Terminal window/tab. There are the two following ways to accomplish this.

### Via config file

You can place a `.nvmrc` file in your home directory to define your prefered version globally. For example:

```bash
5
```

This can be overidden by placing other `.nvmrc` files in your project root directories.

### Via nvm alias

Alternatively you can add an alias with `nvm alias <name> <version> `:

```bash
$ nvm alias default 5
default -> 5 (-> v5.11.1)
```

Enter `nvm --help` to see how to handle aliases.

## So many versions :flushed:

After a few releases it might come in handy to check which versions are installed and which you are currently using.

Just enter the following to see which versions are installed:

```bash
$ nvm ls
```

This will also highlight the version currently in use.

You could also fire `nvm current` to see what version your are using.

### Showing the current version in your prompt

There are zsh themes like [Bullet Train](https://github.com/caiogondim/bullet-train-oh-my-zsh-theme#nodejs-nvm) which offer to make the version visible with every prompt.

![Screenshot](/assets/img/nvm-screenshot.png)
Pretty nifty, huh?

I guess that’s all you need to know to start using nvm. 
Make sure to checked out the [project on Github](https://github.com/creationix/nvm) in case you like to dig deeper.



