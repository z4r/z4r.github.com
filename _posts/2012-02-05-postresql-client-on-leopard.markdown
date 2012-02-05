---
layout: post
title: PostreSQL client on a Mac
---

Whenever I need to install something on my mac involving database, problems arise.

00. You've to install **Xcode**.
01. Download [MacPort][macport] and install it.
02. Install <code>postgresqlXX</code> (9.1 for me):
{% highlight bash %}$ sudo port install postgresql91{% endhighlight %}
03. Add <code>export PATH=/opt/local/lib/postgresql91/bin:$PATH</code> to your <code>.profile</code>
04. If you need postgresql API for your python:
{% highlight bash %}$ pip install psycopg2{% endhighlight %}

[macport]: http://www.macports.org/install.php
