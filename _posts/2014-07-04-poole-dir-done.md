---
layout: post
title: Poole directory setting problem done
comments: True
---
I follow the this webpage http://joshualande.com/jekyll-github-pages-poole/ to make the poole style blog possible.

The keys are

## another way to set up url


{% highlight yaml %}
baseurl: "/blog"
url: "http://openjerseycity.org"

# Build settings
markdown: kramdown
permalink: pretty
{% endhighlight %}


## set up in _config.yml

_config contains general configuration stuff for the website.
{% highlight yaml %}
# Setup
title:            Poole
tagline:          'The Jekyll Butler'
description:      'Base theme for Jekyll themes by @mdo.'
url:              http://getpoole.com
...
{% endhighlight %}


add 
{% highlight html %}
This is the list of pages to incldue in the header of the website.
pages_list: {'About':'/poole/about','Archive':'/poole/archive','Feed':'/poole/atom.xml'}

{% endhighlight %}


in _config.yml

setup this baseurl, which decide the relative directory.

{% highlight html %}
baseurl:          http://snowdj.github.io/poole/
{% endhighlight %}


It tell github that what is the base url for whole blog and in the blog we add archive and about two pages.

### Add the two page in config.yml

{% highlight yaml %}
# This is the list of pages to incldue in the header of the website.
pages_list:       ['About', 'Archive']
{% endhighlight %}



## set up in default.html in layout folder

{% highlight yaml %}
$ ls -1 _layouts/
default.html
page.html
post.html
$ ls -1 _includes/
head.html
{% endhighlight %}


and add some thing in the default.html

{% highlight html %}
<h3 class="masthead-title">
  <a href="/" title="Home">{{ site.title }}</a>
  {% for page_name in site.pages_list %}
    &nbsp;&nbsp;&nbsp;<small><a href="/{{ page_name | downcase }}">{{ page_name }}</a></small>
  {% endfor %}
</h3>
{% endhighlight %}


The code tell github to render the site.page_list for all pages.





## set up archive.html.


{% highlight html %}
{% raw %}
---
layout: page
title: Archive
---

# Blog Posts

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
{% endfor %}
{% endraw %}
{% endhighlight %}

I add this {{ site.baseurl }} in front of the {{ post.url }}.

Also in the index.html

{% highlight html %}
<h1 class="post-title">
      <a href="{{ site.baseurl }}{{ post.url }}">
        {{ post.title }}
      </a>
    </h1>

{% endhighlight %}





## add disqus

To do that, I modified the file _layouts/default.html to include the line:



{% highlight python %}
{% raw %}
{% include comments.html %}
{% endraw %}
{% endhighlight %}


{% highlight html %}
{% if page.comments %}
<!-- Add Disqus comments. -->
<div id="disqus_thread"></div>
<script type="text/javascript">
  /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
  var disqus_shortname = '<USERNAME>'; // required: replace example with your forum shortname

  /* * * DON'T EDIT BELOW THIS LINE * * */
  (function() {
    var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
    dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
    (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
  })();
</script>
<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
<a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
{% endif %}
{% endhighlight %}


"By setting up the code this way, I can enabled commenting on a page-by-page basis. All I have to do is set "comments: True" in the YAML header of the post.""

then created a file _includes/comments.html which includes the code given to me by Disqus:

That's all. 


