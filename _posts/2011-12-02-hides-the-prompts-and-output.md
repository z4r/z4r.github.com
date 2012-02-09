---
layout: post
category : python
tags : [sphinx, documentation]
---
{% include JB/setup %}

I like to write my pydoc with the great [Sphinx]. One of my preferred feature is the doctest highlighting!!!

In the official [PyDoc] yesterday i noticed a very cool button `>>>` that __hide__ / __show__ prompts and output.

To install it we need to download [copybutton.js] in the static folder; then we can simply add in `conf.py` _auto-gen_ by [Sphinx].

    def setup(app):
        app.add_javascript('copybutton.js')

[Sphinx]: http://sphinx.pocoo.org/
[PyDoc]: http://docs.python.org/
[copybutton.js]: http://docs.python.org/_static/copybutton.js
