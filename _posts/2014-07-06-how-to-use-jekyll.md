---
categories: 
layout: post
date: 2014-07-06
tags:
- instructions
- code
---

## Understand the Liquid Templating Language

[The GitHub site hosts the docs](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers). Start there.

## Adding the Patterns Pages and Links

If `_config.yml` contains `relative_permalinks: false`...

And we have a top level folder called 'patterns' and place in it **markdown files** containing something like:

{% highlight yaml %}
---
layout: patterns
title: Revealing Module
permalink: /patterns/revealing-module/
---
{% endhighlight %}

The markdown / html content of the page.

And we have a _layouts/patterns.html file looking something like:

{% highlight html %}
{% raw %}
---
layout: default
---
<section class="docs">
<div class="grid">
<div class="unit four-fifths">
  <article>
    <h1>{{ page.title }}</h1>
    {{ content }}
  </article>
</div>
{% include patterns_contents.html %}
<div class="clear"></div>
</div>
</section>
{% endraw %}
{% endhighlight %}


#### patterns_contents.html

{% highlight html %}
{% raw %}
<div class="unit one-fifth hide-on-mobiles">
  <aside>
    {% for section in site.data.patterns %}
    <h4>{{ section.title }}</h4>
    {% include patterns_ul.html items=section.docs %}
    {% endfor %}
  </aside>
</div>
{% endraw %}
{% endhighlight %}

When patterns_ul.html is included, `section.docs` is passed along, and will be available in patterns_ul.html as the `include.items` variable.

#### patterns_ul.html

{% highlight html %}
{% raw %}
{% assign items = include.items %}
<ul>
{% for item in items %}
  {% assign item_url = item | prepend:"/patterns/" | append:"/" %}
  {% if item_url == page.url %}
    {% assign c = "current" %}
  {% else %}
    {% assign c = "" %}
  {% endif %}
  {% for p in site.pages %}
    {% if p.url == item_url %}
      <li class="{{ c }}"><a href="{{ site.baseurl }}{{ p.url }}">{{ p.title }}</a></li>
    {% endif %}
  {% endfor %}
{% endfor %}
</ul>
{% endraw %}
{% endhighlight %}

## Bug with Pygments Highlighting

[This issue explains the problem](https://github.com/jekyll/jekyll/issues/1181). The solution is to use Python 2.7.

Ensure the following:

* Uninstall any version of Pygments that may not work: `gem uninstall pygments.rb --version "=5.2"`.
* Uninstall Python 3 using Windows normal program uninstall process. Alternatively just change environment variables to point at version 2.7 rather than 3.
* Install Python 2.7 from a newly downloaded MSI.
* Make sure the PATH environment variable includes the correct version of Python, e.g. `C:\Python27`.
* Make sure the PATH includes the Ruby bin folder.

I'm still getting "warning: cannot close fd before spawn 'which' is not recognized as an internal or external command". But the project builds correctly (it seems) and code highlighting appears to be working correctly.


