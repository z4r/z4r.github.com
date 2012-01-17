---
layout: post
title: Hide the prompts and output
---

I like to write my pydoc with the great [Sphinx]. One of my preferred feature is the doctest highlighting!!!

In the official [PyDoc] yesterday i noticed a very cool button `>>>` that **hide**/**show** prompts and output.

To install it we need [copybutton.js] in the static folder; then we can simply add in `conf.py` auto-gen by [Sphinx].

{% highlight python %}
def setup(app):
    app.add_javascript('copybutton.js')
{% endhighlight %}

[Sphinx]: http://sphinx.pocoo.org/ 
[PyDoc]: http://docs.python.org/
[copybutton.js]: http://docs.python.org/_static/copybutton.js
