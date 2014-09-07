---
layout: post
lang: en_GB
title:  "Setting up Jekyll (Part I) – including Flattr integration, comments etc."
date:   2014-09-07 18:50:00
category: jekyll
tags: "blogging, jekyll"
excerpt: "Part I of the »Jekyll Setup post« contains information about installing Jekyll, including Flattr, adding comments, tweaking the site navigation and improving syntax highlighting within your blog posts."
disqusIdentifier: 2014-09-07-jekyll-setup-github
---

As already announced in the first post I will explain a few key points on setting up Jekyll today. Pleaser refer to the »[technical aspects](/blogging/2014/09/01/welcome-first-post.html#technical-aspects)« of my blog if you have no clue what I’m talking about.

Part I of the »Jekyll Setup post« contains information about installing Jekyll, including Flattr, adding comments, tweaking the site navigation and improving syntax highlighting within your blog posts. Part II will take care of GitHub specific stuff (Hosting, Plugins, etc.).

## Install Jekyll

Jekyll is written in Ruby. So you need to have Ruby installed on your machine which is the case on Mac OS X by default. You just have to fire up your terminal and type the following to install Jekyll globally:

```bash
gem install jekyll
```

If your are using the default Ruby on OS X you will probably get the following  error message:

```bash
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.
```

You can easily fix that by executing the same command using superuser privileges via:

```bash
sudo gem install jekyll
```

## Local installation including default theme

The default theme is a clean and responsive one column layout which adapts nicely down to your smart phone. 

```bash
jekyll new my-awesome-site
cd my-awesome-site
```

This will create the directory `my-awesome-site` and install all files needed for your blog which is ready to run from that moment on. But we are going to inspect the content of `my-awesome-site` first.

```markup
.my-awesome-site
├── _config.yml                                   // The main config file
├── _includes                                     // Partials for your layouts
|   ├── footer.html
|   ├── head.html
|   └── header.html
├── _layouts                                      // Layouts for your pages
|   ├── default.html
|   ├── page.html
|   └── post.html
├── _posts                                        // Your posts
|   └── 2014-09-07-welcome-to-jekyll.markdown
├── _sass                                         // Sass includes 
|   ├── _base.scss                                // imported by main.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md                                      // A page 
├── css                                           // Main Sass file
|   └── main.scss
├── feed.xml                                      // Your feed
└── index.html                                    // The homepage

```

See »[Directory structure](http://jekyllrb.com/docs/structure/)« on the Jekyll docs for details.

### Checking the installation 

```bash
jekyll serve
```

Will build your sources into the directory `_site` and will start a server at `http://localhost:4000` running you blog. See »[Basic Usage](http://jekyllrb.com/docs/usage/)« on the Jekyll docs for a complete list of available commands.

**Important note**:  
Additional files in the root of your blog are copied o the root of `_site` when the site is built.

### Make use of *Drafts*

Create a directory called `_drafts` in the root of your site. This is the place for writing your post before *publishing* them via the `_posts` directory. Use the following command to build and *serve* your blog including the drafts.

```bash
jekyll serve --watch --drafts 
```

`--watch` watches for changes, and regenerates files automatically. This works for content as well as for Sass and JavaScript.

---

## Hide specific pages from the navigation

You may wish to exclude pages from the menu at the top righ corner of your page.
Especially if you live in Germany and have the need for all those annoying legal stuff.

**No problem**
Just extend the so called »[Front Matter](http://jekyllrb.com/docs/frontmatter/)« of pages you wish to include in the site navigation with an own custom variable.  

Let’s take the »about« page `about.md` for example and change the default front matter block from:

```markup
---
layout: page
title: About
permalink: /about/
---
```

to:

```markup
---
layout: page
title: About
permalink: /about/
menu: true
---
```

### Change the rendering of the navigation

Open `header.html` and replace 

<pre><code class="language-markup">&#123;% if page.title %&#125;  
  &lt;a class="page-link" href="&#123;&#123; page.url | prepend: site.baseurl &#125;&#125;">
      &#123;&#123; page.title &#125;&#125;
  &lt;/a>  
&#123;% endif %&#125;</code></pre>

with 

<pre><code class="language-markup">&#123;% if page.menu == true  %&#125;  
  &lt;a class="page-link" href="&#123;&#123; page.url | prepend: site.baseurl &#125;&#125;">
    &#123;&#123; page.title &#125;&#125;
  &lt;/a>  
&#123;% endif %&#125;</code></pre>

---

## Custom sorting of pages within the navigation

Jekyll sorts your menu items alphabetically without giving you a simple possibilty to change that. So we have to dig deep in our bag of tricks to accomplish such a basic desire.

**Rename pages within your file system**  
Just prefix your pages with a numeric index. For example

```markup
index.html    →     00-index.html
about.md      →     01-about.md
```

**Update the rendering of the navigation**
You have to change some code within `header.html` in addition to the renaming.

Before:

<pre><code class="language-markup">&#123;% if page.menu == true  %&#125;  
  &lt;a class="page-link" href="&#123;&#123; page.url | prepend: site.baseurl &#125;&#125;">
    &#123;&#123; page.title &#125;&#125;
  &lt;/a>  
&#123;% endif %&#125;</code></pre>

After:

<pre><code class="language-markup">&#123;% assign sorted_pages = site.pages | sort:"name" %&#125;
&#123;% for node in sorted_pages %&#125;
  &#123;% if node.menu == true  %&#125;  
    &lt;a class="page-link" href="&#123;&#123; node.url | prepend: site.baseurl &#125;&#125;">
      &#123;&#123; node.title &#125;&#125;
    &lt;/a>  
  &#123;% endif %&#125;
&#123;% endfor %&#125;</code></pre>

---

## Enhance syntax highlighting in your blog posts

First off all we like to use the so called *[GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)* to make use of *[Fenced code blocks](https://help.github.com/articles/github-flavored-markdown#fenced-code-blocks)* including the abbility to add languages to code blocks for language specific syntax highlighting. We need to add two lines to the build settings of `_config.yml` to accomplish this.

Before:

```markup
# Build settings
markdown: kramdown
```

After:

```markup
# Build settings
markdown: kramdown
kramdown:
  input: GFM
```

Now we can use:

``````markup
```javascript
var foo = 'foo';
```
``````

Instead of using these liquid tags

<pre><code class="language-markup">&#123;% highlight javascript %&#125;
var foo = 'foo';
&#123;% endhighlight %&#125;</code></pre>

### Using the beautiful **prism** syntax highligter 

1. Go to <http://prismjs.com/> and download Prism according to your needs
  (in terms of needed languages, plugins and a theme of your choice)
2. Place `prism.js` in the `/js` directory
3. Reference `/js/prism.js` from the bottom of `footer.html`:
  `<script src="/assets/js/prism.js"></script>`
4. Replace the content of `_syntax-highlighting.scss` with the content of `prism.css`

That’s it.

## Flattr Integration

Integrating Flattr on the pages containing your posts is pretty straight forward. First of all add a file called `flattr.js` to your `/js` directory. 

Copy the following content into that file:

```javascript
(function() {
    var s = document.createElement('script');
    var t = document.getElementsByTagName('script')[0];

    s.type = 'text/javascript';
    s.async = true;
    s.src = '//api.flattr.com/js/0.6/load.js?mode=auto' +
        '&uid=YourUserName' +
        '&button=compact' +
        '&html5-key-prefix=data-flattr';

    t.parentNode.insertBefore(s, t);
 })();
```

See [Embedded buttons](http://developers.flattr.net/button/) on the Flattr docs for further information.

### Add and configure Flattr buttons on your posts

Open `post.html` and add the following snippet wherever you like to place your Flattr button:

```markup
<a class="FlattrButton"
  title="{{ "{{page.title" }}}}"
  data-flattr-tags="{{ "{{page.tags" }}}}"
  data-flattr-category="text"
  data-flattr-language="{{ "{{page.lang" }}}}"
  href="{{ "{{site.url" }}}}{{ "{{page.url" }}}}">
    {{ "{{page.excerpt" }}}}
</a>
```

Make sure you’ve set `page.lang` and `page.excerpt` via »[Front Matter](http://jekyllrb.com/docs/frontmatter/)« on top of your posting. See the following example of my first post `2014-09-07-welcome-to-jekyll.markdown`

```markup
---
layout: post
lang: en_GB
title:  "„Welcome“ aka „This is the first post on my blog“"
date:   2014-09-01 21:53:08
category: blogging
tags: "blogging, jekyll"
excerpt: "Teaser text …"
---
```

Now you’ve got Flattr buttons automatically add to all your post with the page excerpt on the Flattr page of your »*thing*«.

---

##Adding comments

If you like to have comments on a *static* blog generated by Jekyll you have to depend on a third party tool which appends comments with heavy use of JavaScript. Yes, there are alternatives to [Disqus](https://disqus.com/) when it comes to comments. But I choose Disqus mainly because I already had an account and I had not time for checking out the other vendors.

**Here we go with short explanation of adding comments provided by Disqus:**  
First of all you need to [register](https://disqus.com/admin/create/) a site add Disqus and add the URL of your website within the [admin settings](https://michaelkuehnelde.disqus.com/admin/settings/). I left the other settings pretty much untouched but you can go really wild over there. 

Then you can add the following snippet to `post.html`:

```markup
<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
    var disqus_shortname = 'YourWebsitesShortname',
      disqus_identifier = '{{ "{{page.disqusIdentifier" }}}}',
      disqus_title = '{{ "{{page.title" }}}}',
      disqus_url = '{{ "{{site.url" }}}}{{ "{{page.url" }}}}';

    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script');
        dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0]
            || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the comments</noscript>
```

See [Setup Instructions](https://michaelkuehnelde.disqus.com/admin/settings/universalcode/) from Disqus.

Make sure you’ve set `page.disqusIdentifier` via »[Front Matter](http://jekyllrb.com/docs/frontmatter/)« on top of your posting. See the following example of my first post `2014-09-07-welcome-to-jekyll.markdown`

```markup
---
layout: post
lang: en_GB
title:  "„Welcome“ aka „This is the first post on my blog“"
date:   2014-09-01 21:53:08
category: blogging
tags: "blogging, jekyll"
excerpt: "Teaser text …"
disqusIdentifier: 2014-09-01welcome-first-post
---
```

You could omit the use of the `disqus_identifier` in the snippet as well as in the *Front Matter*. But I recommend using it, because you comments keep connected to the post when you decide to change your URL scheme. Or in the words of Disqus:

> You'll be able to reference the same thread regardless of the URL where it is loaded.

---

## Bottom line

Setting up a blog powered by Jekyll is pretty easy. Your blog will be up and running in a couple of hours if you’re happy with the default theme. As mentioned before, there will be a follow up post regarding GitHub specific stuff (Hosting, Plugins, etc.). So please return after you have adjust the default theme according to your needs :blush:
