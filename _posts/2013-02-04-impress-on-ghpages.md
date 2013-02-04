---
layout: post
category : slide
tags : [github, gh-pages, impress.js]
---
{% include JB/setup %}

Step to add `gh-pages` removing `master`:

    $ git checkout -b gh-pages
    $ git push -u origin gh-pages

From your repos github settings set `gh-pages` as default.

    $ git branch -D master
    $ git push origin :master

That's it!!!

