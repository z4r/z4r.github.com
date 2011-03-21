---
layout: post
title: JSON Perl and Python
---

Perl Version:
{% highlight perl %}
#!/usr/bin/perl
use strict;
use warnings;
use JSON;
use Data::Dumper;
my $perl_scalar = {
    'a' => 'b',
    'c' => 'd',
};
my $json_text = to_json ($perl_scalar, {utf8 => 1});
print "$json_text\n";
$perl_scalar = from_json ($json_text, {utf8  => 1});
print Dumper($perl_scalar);
{% endhighlight %}

Python Version:
{% highlight python %}
#!/usr/bin/python
import json
d1 = {
    'a' : 'b',
    'c' : 'd',
}
text = json.dumps(d1)
print text
d2 = json.loads(text)
print d2
print d1 == d2
{% endhighlight %}