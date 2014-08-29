---
layout: post
title:  "Welcome to Jekyll!"
date:   2014-05-25 21:53:08
categories: jekyll update
tags: jekyll blogging
excerpt: First post is about checking out jekyll.
---

You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

Jekyll also offers powerful support for code snippets:

{% highlight javascript %}
/**
 * Bind custom event `overflowed`.
 * Fired when a element within the ribbon is overflowed.
 */
$(document).on('overflowed.kira.ribbon', function() {
	console.warn('overflowed!');
	$('#mm_mainTabContent').find('.mm_ribbonCloneOpener').show();
	//$ribbonCloneWrapper.attr('data-visible', 'true');
});
{% endhighlight %}

```javascript
/**
 * Bind custom event `overflowed`.
 * Fired when a element within the ribbon is overflowed.
 */
$(document).on('overflowed.kira.ribbon', function() {
	console.warn('overflowed!');
	$('#mm_mainTabContent').find('.mm_ribbonCloneOpener').show();
	//$ribbonCloneWrapper.attr('data-visible', 'true');
});
```

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll]:    http://jekyllrb.com
