---
layout: post
lang: en_GB
title:  "Quick Tip: Git, Mac OS X and German Umlauts (Umlaute)"
date:   2014-11-21 20:00:00
category: Git
tags: "Quick Tip, Git, Mac OS X, Umlauts, Umlaute, UTF-8, Unicode"
image: "/assets/img/git-logo.png"
excerpt: "Sure, using umlauts or other special characters within filenames is far from being called a best practice and should be forbidden by law (or at least by convention) for source code repositories. But sometimes you just have to deal with given files and might wonder why you find untracked files in a freshly cloned Git repository. If you’re on Mac OS X there is a great chance that this is caused by Umlauts or other Unicode characters."
---

## Update from September 22, 2015

In the current version of Mac OS X (10.10.5) with the latest version of Git (2.5.2) `precomposeunicode` has to be set to  `true` :persevere:

```bash
[core]
    # Git and the Umlaut problem on Mac OS X
    # Prevent showing files which filenames contains umlauts as untracked
    # Needs to be `false` since OS X 10.9.x
    precomposeunicode = true
```

---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          {{page.excerpt}}
        </p>
    </div>
</div>

In a Git client like SourceTree or Tower the filenames (of the suprisingly untracked files) look like your expect them to look:

![Screenshot: SourceTree](/assets/img/screenshot-sourcetree.png)

If you fire `git status` in your Terminal instead you see how Git handles Unicode characters:

![Screenshot: Terminal](/assets/img/screenshot-terminal.png)

That’s easy to fix … but in a different way depending on your OS X version :grin: (See: [stackoverflow.com](http://stackoverflow.com/questions/5581857/git-and-the-umlaut-problem-on-mac-os-x))

Since OS X 10.9.x `precomposeunicode` has to be set to `false`. This should be defined in your global `.gitconfig` and if needed within your repository as well.

## Global

You can choose whether to add the following to `~/.gitconfig` via your file system:

```bash
[core]
    # Git and the Umlaut problem on Mac OS X
    # Prevent showing files which filenames contains umlauts as untracked
    # Needs to be `false` since OS X 10.9.x
    precomposeunicode = false
```

See my [dotfiles](https://github.com/mischah/dotfiles/commit/f2ab1a8bb27a6dc944e2abd991f499e7928aef0d#diff-4723a3b40361325f6612c40749b696d9R80).

Or via your Terminal:

```bash
git config --global core.precomposeunicode false
```

## In your repository

This seems to be necessary depending on how the repository was created.

In addition to both ways described globally you can also edit the `.gitconfig` of your repository via the SourceTree user interface. Just click the following within the programs menu: »Repository« → »Repository Settings« → »Edit Config File …« and add `precomposeunicode = false` below `[core]` as described above.

Or via the Terminal just like before but without the global flag:

```bash
cd ~/my/path/to/repository
git config core.precomposeunicode false
```

---

**Please note:** 
There’s no need to trash the repository and clone it a second time. Just apply the settings and you’re good to go :ok_hand:
