---
title: Geo::IP + DBD::mysql on Snow Leopard
layout: post
category : perl
tags : [geoip, mysql, cpan, macosx]
---
{% include JB/setup %}

During the installation of these two packages I ran into some difficulties due to my lack of handiness with [CPAN] and Snow Leopard.

## Geo::IP
Like we can read on package doc

> Geo::IP 1.37 requires GeoIP CAPI 1.4.5 or higher

_Couff couff, "Copy That"_

Download [this][geoipapi]
Uncompress the file and type:

    $ ./configure
    $ make
    $ make check
    $ sudo make install

## DBD::mysql
My [MySQL] installation points to `/usr/local/mysql/`, while [CPAN] looking for a lib in another path.

So we can start creating a separate directory for the mysql static client library and coping the <code>libmysqlclent.a</code> library into it

    $ mkdir /usr/local/mysql/lib-static
    $ cp /usr/local/mysql/lib/libmysqlclient.a /usr/local/mysql/lib-static

Remove `DBD::mysql` modules and clean CPAN's build directory:

    $ sudo rm -fr /Library/Perl/5.10.0/darwin-thread-multi-2level/DBD
    $ sudo rm -fr $HOME/.cpan/build/DBD-mysql-4*

Now get the latest `DBD::mysql` module:

    $ sudo cpan
    > get DBD::mysql

Modify the *Makefile* and install it manually:

    $ sudo -s
    $ cd $HOME/.cpan/build/DBD-mysql-*
    $ perl Makefile.PL –libs "-L/usr/local/mysql/lib-static -lmysqlclient"
    $ make
    $ make check
    $ make install
------
![hate](/images/angry.png)

[CPAN]: http://search.cpan.org/
[geoipapi]: http://geolite.maxmind.com/download/geoip/api/c/
[http://www.maxmind.com/app/c]: http://www.maxmind.com/app/c
[MySQL]: http://www.mysql.it/downloads/mysql/
