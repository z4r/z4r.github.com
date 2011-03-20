---
layout: post
title: Bored about Blog
---

Probably like many people I've *"better to have it"* syndrome.
So we start and infinite search oh the **Ultimate Tool**.
Perhaps by chance, perhaps the fate I finally found **it**.
I do not need comments and I do not need to complicate simple notes taken first of all for me.

#Jekyll on GitHub

Really nothing simpler than this winning combination.

##Evil side of blogging

[Jekyll] is a blog-aware, static site generator in Ruby and to install it just type on your terminal:
{% highlight bash %}
$ [sudo] gem install jekyll
{% endhighlight %}
To create your first site just create a folder:
{% highlight bash %}
$ mkdir <folder>
$ cd <folder>
{% endhighlight %}
and fill it with:
{% highlight bash %}
$ touch _config.yml
$ touch index.html
$ mkdir _layouts
$ mkdir _posts
{% endhighlight %}
I watched many jekyll projects aroud the web and I decided to *fork* [Zach] for his cleaning without frippery; but I like too much Orange to miss it...
So I edit and fill my folder with some [code] and tried it with:
{% highlight bash %}
$ jekyll --server --auto
{% endhighlight %}
and magically *(as Ruby user usually said)* on localhost:4000 I found my empty blog.

##Let **deploy time** begin

I just use [GitHub] to version my *home*. As every their work, [pages] is awesome with a very clean guide, so with a simple commit/push you now can read my [shit].

##On the infinity and behind
Tomorrow i'll try another guide to migrate my wordpress @ work and i can promise i won't speak no more about Ruby.
To *googlefy* this blog i need [sitemap] and analytics but for a while they can wait.

[Jekyll]: http://github.com/mojombo/jekyll
[Zach]: http://zachholman.com/
[code]: https://github.com/z4r
[GitHub]: http://github.com/
[pages]: http://pages.github.com/
[shit]: http://z4r.github.com/
[sitemap]: http://recursive-design.com/blog/2010/10/12/static-blogging-the-jekyll-way/
