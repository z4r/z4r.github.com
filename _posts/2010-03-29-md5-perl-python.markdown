---
layout: post
title: MD5 Perl and Python
---

Perl Version:
{% highlight perl %}
#!/usr/bin/perl
use strict;
use warnings;
use Digest::MD5 qw(md5_hex);
print md5_hex( "Hello World!" )."\n";
{% endhighlight %}

Python Version:
{% highlight python %}
#!/usr/bin/python
from hashlib import md5
print md5("Hello World!").hexdigest()
{% endhighlight %}
