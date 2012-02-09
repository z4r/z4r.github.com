---
layout: post
category : jekyll
tags : [githum, blog, tutorial]
---
{% include JB/setup %}

Probably like many people I've _"better to have it"_ syndrome.
So we start an infinite search oh the __Ultimate Tool__.
Perhaps by chance, perhaps by fate, I finally found it.
I do not need to complicate simple notes, which I just take for myself.

# Jekyll on GitHub

Really nothing is simpler than this winning combination.

## Evil side of blogging

[Jekyll] is a blog-aware, static site generator in Ruby and to install it just type on your terminal:

    $ [sudo] gem install jekyll

To create your first site just create a folder:

    $ mkdir <folder>
    $ cd <folder>

and fill it with:

    $ touch _config.yml
    $ touch index.html
    $ mkdir _layouts
    $ mkdir _posts

I watched many jekyll projects aroud the web and I decided to _fork_ [Zach] for his cleaning without frippery; but I like too much orange to miss it...
So I edited and filled my folder with some [code] and tried it with:

    $ jekyll --server --auto

and magically _(as Ruby user usually said)_ on localhost:4000 I found my empty blog.

## Let __deploy time__ begin

I just use [GitHub] to version my *garage* projects. Like every their work, [pages] is awesome with a very clean guide, so with some commit/push you now can

## On the infinity and behind
Tomorrow I'll try another guide to migrate my wordpress @ work and I promise I won't speak about Ruby anymore.
To _googlefy_ this blog I need [sitemap] and analytics but for a while they can wait.

[Jekyll]: http://github.com/mojombo/jekyll
[Zach]: http://zachholman.com/
[code]: https://github.com/z4r
[GitHub]: http://github.com/
[pages]: http://pages.github.com/
[shit]: http://z4r.github.com/
[sitemap]: http://recursive-design.com/blog/2010/10/12/static-blogging-the-jekyll-way/
