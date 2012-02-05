---
layout: post
title: MusicBrainz DBslave on Ubuntu Server
---

A very simple guide Step by Step to install a clone of [Musicbraiz Database][musicbrainz] on your Ubuntu Server.

01. Download [Ubuntu Server][ubuntu] (i prefer [this][mini.iso]).
02. Install it in the smaller version you can.
03. Install the set of library you'll need:
{% highlight bash %}$ sudo apt-get install vim git postgresql-client-common postgresql-client postgresql openssh-server python-setuptools libpq-dev python-dev
$ sudo easy_install psycopg2 virtualenv{% endhighlight %}
04. Open the <code>postgresql</code> to your *subnet*:
{% highlight bash %}$ sudo vi /etc/postgresql/9.1/main/postgresql.conf{% endhighlight %}
> Change this line <code>listen_addresses = '*'</code>
{% highlight bash %}$ sudo vi /etc/postgresql/9.1/main/pg_hba.conf{% endhighlight %}
> Add this line <code>host all all 192.168.1.0/24 md5</code>
{% highlight bash %}$ sudo /etc/init.d/postgresql restart{% endhighlight %}
05. Create the postgresql user **musicbrainz**:
{% highlight bash %}$ createuser musicbrainz{% endhighlight %}
06. Create the **postgres** and **musicbrainz** passwords:
{% highlight bash %}$ sudo -u postgres psql postgres
postgres=# \password postgres
postgres=# \password musicbrainz{% endhighlight %}
07. Create the DB and the **SCHEMA**:
{% highlight bash %}$ createdb -l C -E UTF-8 -T template0 -O musicbrainz musicbrainz
$ git clone https://github.com/lalinsky/mbslave.git
$ cd mbslave
$ cp mbslave.conf{.default,}
$ echo 'CREATE SCHEMA musicbrainz;' | ./mbslave-psql.py -S
$ sed 's/CUBE/TEXT/' sql/CreateTables.sql | ./mbslave-psql.py{% endhighlight %}
08. Download the latest version of <code>mbdump.tar.bz2</code> and <code>/mbdump-derived.tar.bz2</code> [here][fullexport].
09. Import the data and build indexes:
{% highlight bash %}$ ./mbslave-import.py mbdump.tar.bz2 mbdump-derived.tar.bz2
$ ./mbslave-psql.py <sql/CreatePrimaryKeys.sql
$ grep -vE '(collate|page_index|tracklist_index)' sql/CreateIndexes.sql | ./mbslave-psql.py
$ ./mbslave-psql.py <sql/CreateSimpleViews.sql
$ echo 'VACUUM ANALYZE;' | ./mbslave-psql.py{% endhighlight %}
10. Change your crontab with this synchronizer:
{% highlight bash %}$ crontab -e{% endhighlight %}
> Add this line <code>15 * * * * $HOME/mbslave/mbslave-sync.py >>/var/log/mbslave.log</code>

ENJOY :)

[musicbrainz]: http://musicbrainz.org
[ubuntu]: http://www.ubuntu.com/
[mini.iso]: http://archive.ubuntu.com/ubuntu/dists/oneiric/main/installer-i386/current/images/netboot/mini.iso
[fullexport]:  http://ftp.musicbrainz.org/pub/musicbrainz/data/fullexport/
