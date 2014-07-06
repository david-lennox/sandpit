---
layout: post
title: Jekyll Notes
date: 2014-07-06
---

## Adding the Patterns Pages and Links

If `_config.yml` contains `relative_permalinks: false`...

And we have a top level folder called 'patterns' and place in it **markdown files** containing something like:

```
---
layout: patterns
title: Revealing Module
permalink: /patterns/revealing-module/
---
The markdown / html content of the page.
```

And we have a _layouts/patterns.html file looking something like:

```
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
```



#### patterns_contents.html

```
<div class="unit one-fifth hide-on-mobiles">
  <aside>
    {% for section in site.data.patterns %}
    <h4>{{ section.title }}</h4>
    {% include patterns_ul.html items=section.docs %}
    {% endfor %}
  </aside>
</div>
```

When patterns_ul.html is included, `section.docs` is passed along, and will be available in patterns_ul.html as the `include.items` variable.

#### patterns_ul.html

```
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
      <li class="{{ c }}"><a href="{{ site.url }}{{ p.url }}">{{ p.title }}</a></li>
    {% endif %}
  {% endfor %}

{% endfor %}
</ul>
```