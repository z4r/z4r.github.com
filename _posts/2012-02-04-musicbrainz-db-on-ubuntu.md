---
layout: post
category : database
tags : [musicbrainz, postgresql, ubuntu]
---
{% include JB/setup %}

A very simple guide Step by Step to install a clone of [Musicbraiz Database][musicbrainz] on your Ubuntu Server.

Download [Ubuntu Server][ubuntu] (i prefer [this][mini.iso]).
Install it in the smaller version you can.
Install the set of library you'll need:

    $ sudo apt-get install vim git postgresql-client-common postgresql-client postgresql openssh-server python-setuptools libpq-dev python-dev
    $ sudo easy_install psycopg2 virtualenv

Open the `postgresql` to your _subnet_:

> Change this line `listen_addresses = '*'` on `/etc/postgresql/9.1/main/postgresql.conf`

> Add this line `host all all 192.168.1.0/24 md5` on `/etc/postgresql/9.1/main/pg_hba.conf`

    $ sudo /etc/init.d/postgresql restart

Create the postgresql user **musicbrainz**:

    $ createuser musicbrainz

Create the **postgres** and **musicbrainz** passwords:

    $ sudo -u postgres psql postgres
    postgres=# \password postgres
    postgres=# \password musicbrainz

Create the DB and the **SCHEMA**:

    $ createdb -l C -E UTF-8 -T template0 -O musicbrainz musicbrainz
    $ git clone https://github.com/lalinsky/mbslave.git
    $ cd mbslave
    $ cp mbslave.conf{.default,}
    $ echo 'CREATE SCHEMA musicbrainz;' | ./mbslave-psql.py -S
    $ sed 's/CUBE/TEXT/' sql/CreateTables.sql | ./mbslave-psql.py

Download the latest version of `mbdump.tar.bz2` and `/mbdump-derived.tar.bz2` [here][fullexport].
Import the data and build indexes:

    $ ./mbslave-import.py mbdump.tar.bz2 mbdump-derived.tar.bz2
    $ ./mbslave-psql.py <sql/CreatePrimaryKeys.sql
    $ grep -vE '(collate|page_index|tracklist_index)' sql/CreateIndexes.sql | ./mbslave-psql.py
    $ ./mbslave-psql.py <sql/CreateSimpleViews.sql
    $ echo 'VACUUM ANALYZE;' | ./mbslave-psql.py

Change your crontab with this synchronizer:

    $ crontab -e

> Add this line `15 * * * * $HOME/mbslave/mbslave-sync.py >>/var/log/mbslave.log`
-------------

Rock'n'Roll :)

[musicbrainz]: http://musicbrainz.org
[ubuntu]: http://www.ubuntu.com/
[mini.iso]: http://archive.ubuntu.com/ubuntu/dists/oneiric/main/installer-i386/current/images/netboot/mini.iso
[fullexport]:  http://ftp.musicbrainz.org/pub/musicbrainz/data/fullexport/
