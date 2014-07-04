---
layout: post
title: Poole directory setting problem down
---
I follow the this webpage http://joshualande.com/jekyll-github-pages-poole/ to make the poole style blog possible.

The keys are


## set up in _config.yml
add 
```
# This is the list of pages to incldue in the header of the website.
pages_list: {'About':'/poole/about','Archive':'/poole/archive','Feed':'/poole/atom.xml'}
```

in _config.yml

setup the 

```
baseurl:          http://snowdj.github.io/poole/
```


It tell github that what is the base url for whole blog and in the blog we add archive and about two pages.



## set up in default.html in layout folder

```
<a href="{{ site.baseurl }}" title="Home">{{ site.title }}</a>
          <small>{{ site.tagline }}</small>
          {% for page in site.pages_list %}
            &nbsp;&nbsp;&nbsp;
            <small><a href="{{ page[1]  }}">{{ page[0] }}</a></small>
          {% endfor %}
        </h3>
```

The code tell github to render the site.page_list for all pages.

## set up archive.

```

---
layout: page
title: Archive
---

## Blog Posts

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
{% endfor %}

```

That's all. 