---
layout: post
lang: en_GB
title:  "Quick Tip: Update your Git client on Mac OS X"
date:   2014-12-19 12:00:00
category: Git
tags: "Quick Tip, Git, Mac OS X, Security"
image: "/assets/img/git-logo.png"
excerpt: "I like to assist you in case you wonder how to react on yesterdays announcement of that critical Git security vulnerability. As said within a post on Githubs Blog it’s strongly recommended to update your Git clients as soon as possible. Here we go with a short instruction how to update in case you are using OS X."
disqusIdentifier: 2014-12-19-update-your-git-client-on-mac-os-x
---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          I like to assist you In case you wonder how to react on yesterdays announcement of that critical Git security vulnerability. As said within this [post](https://github.com/blog/1938-vulnerability-announced-update-your-git-clients) on Githubs Blog it’s strongly recommended to update your Git clients as soon as possible. Here we go with a short instruction how to update in case you are using OS X.
        </p>
    </div>
</div>

## 1. If your already using Homebrew

```bash
brew update && brew upgrade git` bzw. `brew update && brew install git`
```

Entering `git --version` should echo → `git version 2.2.1` afterwards.

In case it’s saying something like `Git 1.9.x (Apple)` instead you have to add `export PATH=/usr/local/bin:$PATH` to your environment variables via `.bashrc` or however you handle that. See [my dotfiles](ttps://github.com/mischah/dotfiles/commit/44fae96e96b5721c0e349fafdc1172e78278979c).

After restarting your terminal  `git --version` should print → `git version 2.2.1`.

And you’re safe using Git via the command line.

## 2. If you dont use Homebrew

Get [Homebrew](Installieren → http://brew.sh/) and start reading at »1. If your already using Homebrew«.

## Update your Git Gui

In case your a using a Git client like Tower oder SourceTree you have to tell those apps which Git version they should use. You can set this via the Applications Preferences hitting `⌘ + ,` pn your Keyboard.

---

That’s it. Happy coding and merry christmas :christmas_tree:
