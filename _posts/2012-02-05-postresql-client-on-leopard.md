---
layout: post
category : database
tags : [postgresql, macosx]
---
{% include JB/setup %}

Whenever I need to install something on my mac involving database, problems arise. _Ok, let's start!_

You've to install __Xcode__, the download [MacPort][macport] and install it.

Now to Install `postgresqlXX` (9.1 for me):

    $ sudo port install postgresql91

Add `export PATH=/opt/local/lib/postgresql91/bin:$PATH` to your `.profile`.

If you need postgresql API for your python:

    $ pip install psycopg2

[macport]: http://www.macports.org/install.php
