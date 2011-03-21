---
layout: post
title: Schneier & the Blowfish
---

Of course i'm not a spy, but some times i need to encrypt <code>"plaintext"</code>.
Remember probably <code>"0123456789ABCDEF"</code> isn't an *unbreakable* password!


{% highlight perl %}
#!/usr/bin/perl
use strict;
use warnings;
use Crypt::Blowfish;
my $key = pack("H16", "0123456789ABCDEF");  # min. 8 bytes
my $cipher = new Crypt::Blowfish $key;
my $ciphertext = $cipher->encrypt("plaintext");
print unpack("H16", $ciphertext), "\n";
my $plain = $cipher->decrypt($ciphertext);
print $plain."\n";
{% endhighlight %}

Why [Blowfish]? Because [Bruce Schneier] is one of my hero.

[Bruce Schneier]: http://www.schneier.com/
[Blowfish]: http://en.wikipedia.org/wiki/Blowfish_(cipher)