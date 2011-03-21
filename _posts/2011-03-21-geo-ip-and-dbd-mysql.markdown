---
layout: post
title: Geo::IP and DBD::mysql on Snow Leopard
---

During the installation of these two packages I ran into some difficulties due to my lack of handiness with [CPAN] and Snow Leopard.

##Geo::IP
Like we can read on package doc

> Geo::IP 1.37 requires GeoIP CAPI 1.4.5 or higher

*Couff couff, "Copy That"*

1. Download [this][geoipapi]

2. Uncompress the file and type:

{% highlight bash %}
$ ./configure
$ make
$ make check
$ sudo make install
{% endhighlight %}

##DBD::mysql
My [MySQL] installation points to <code>/usr/local/mysql/</code>, while [CPAN] looking for a lib in another path.

1. So we can start creating a separate directory for the mysql static client library and coping the <code>libmysqlclent.a</code> library into it
{% highlight bash %}
$ mkdir /usr/local/mysql/lib-static
$ cp /usr/local/mysql/lib/libmysqlclient.a /usr/local/mysql/lib-static
{% endhighlight %}

2. Remove <code>DBD::mysql</code> modules and clean CPAN's build directory:
{% highlight bash %}
$ sudo rm -fr /Library/Perl/5.10.0/darwin-thread-multi-2level/DBD
$ sudo rm -fr /Users/ademarco/.cpan/build/DBD-mysql-4*
{% endhighlight %}

3. Now get the latest <code>DBD::mysql</code> module:
{% highlight bash %}
$ sudo cpan
> get DBD::mysql
{% endhighlight %}

4. Modify the *Makefile* and install it manually:
{% highlight bash %}
$ sudo -s
$ cd /Users/ademarco/.cpan/build/DBD-mysql-*
$ perl Makefile.PL –libs "-L/usr/local/mysql/lib-static -lmysqlclient"
$ make
$ make check
$ make install
{% endhighlight %}

------
![hate](/images/angry.png)

[CPAN]: http://search.cpan.org/
[geoipapi]: http://geolite.maxmind.com/download/geoip/api/c/
[http://www.maxmind.com/app/c]: http://www.maxmind.com/app/c
[MySQL]: http://www.mysql.it/downloads/mysql/
