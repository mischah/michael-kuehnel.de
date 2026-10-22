---
layout: post
lang: en_GB
title: "Introducing »Relaxed« 1.0.0 for Zed"
date: 2026-10-22
category: Tooling
tags: "Zed, Theme, Relaxed, Editor"
image: "/assets/img/zed-relaxed-theme.png"
excerpt: "The Relaxed theme is now available for Zed. Version 1.0.0 brings the calm colors you might have enjoyed in your terminal and VSCode to the new and blaziingly fast Rust-powered editor."
---

{{page.excerpt}}

<figure>
  <img src="/assets/img/zed-relaxed-theme.png" alt="Screenshot of the Relaxed Theme in Zed showing a demo tsx file.">
  <figcaption>Zed now feels like home 🕶️</figcaption>
</figure>

## Backstory

Back in 2018 I released the »Relaxed Theme«, a color scheme I had fine-tuned for my terminal over quite a while. A [Visual Studio Code version](https://marketplace.visualstudio.com/items?itemName=mischah.relaxed-theme) followed shortly after and was used by myself and many others for almost a decade. 

Today I'm happy to announce that »Relaxed Theme« has arrived in [Zed](https://zed.dev) with version `1.0.0` 🎉

## How I ended up here

I stumbled upon Zed a while ago and got curious. I played around a bit an began configuring it to my needs (pretty much VSCode based style). After basic settings,  tosssing around side bars from one side to the other and installing just one additional extension I was quite taken with it.

After scrolling through `settings.json` and some addional minor tweaks here and there and using Zed as my primary work tool I became a fan.

The baked in »One Dark« theme is more than okay-ish. But of course I digged through third party themes I discovered that [Stefan Cosma](https://github.com/stefanbc) had already ported »Relaxed« to Zed. What a pleasant surprise.

So I invited Stefan to the [Relaxed-Theme](https://github.com/Relaxed-Theme) organization on GitHub, where the port now lives next to the terminal and VS Code versions, and started polishing. Now I'm really happy to use Zed exactly the way I want it to feel.

## What's new in 1.0.0

The goal was simple: if you know »Relaxed Theme« from VS Code, it should feel exactly the same in Zed. Stefan's port was a great starting point, but Zed highlights code a little differently, so here and there a color didn't match and the theme felt slightly off.

Version 1.0.0 closes that gap. Your code looks the way you know it from VS Code, diffs and merge conflicts are easy to read, and the UI got a bit calmer and easier on the eyes.

## Installation

1. Open **Extensions** in Zed (`cmd-shift-x` on macOS)
2. Search for `Relaxed`
3. Click **Install**
4. Open the theme picker (`cmd-k cmd-t`) and select **Relaxed**

That's it. Or check the [Zed extension page](https://zed.dev/extensions/relaxed-theme) and the [repository](https://github.com/Relaxed-Theme/zed-theme-relaxed) on GitHub.

## In action

**TypeScript / React:**

![Screenshot: Relaxed theme in Zed showing TypeScript / React](https://raw.githubusercontent.com/Relaxed-Theme/zed-theme-relaxed/main/screenshots/tsx.png)

**Sass:**

![Screenshot: Relaxed theme in Zed showing Sass](https://raw.githubusercontent.com/Relaxed-Theme/zed-theme-relaxed/main/screenshots/scss.png)

**Python:**

![Screenshot: Relaxed theme in Zed showing Python](https://raw.githubusercontent.com/Relaxed-Theme/zed-theme-relaxed/main/screenshots/py.png)

**Rust:**

![Screenshot: Relaxed theme in Zed showing Rust](https://raw.githubusercontent.com/Relaxed-Theme/zed-theme-relaxed/main/screenshots/rs.png)

You'll find more examples (JSON, HTML, Markdown, diffs and merge conflicts) in the [README](https://github.com/Relaxed-Theme/zed-theme-relaxed#language-examples).

## Make it yours

If you'd like to change a color without forking the theme, Zed lets you override single values in your `settings.json`:

```json
"theme_overrides": {
  "Relaxed": {
    "search.match_background": "#ebc17a40"
  }
}
```

The full list of available keys is in the [theme documentation](https://zed.dev/docs/themes).

---

That's it for now. Thanks again to Stefan for getting the ball rolling. If something looks funky, please [open an issue](https://github.com/Relaxed-Theme/zed-theme-relaxed/issues). Pull requests are welcome as well :octocat:
