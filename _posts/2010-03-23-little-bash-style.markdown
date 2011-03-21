---
layout: post
title: Little Bash Style
---

Three solutions for three problems

##Multi exec
1. Exec a perl script on several files:

{% highlight bash %}
for i in $(ls path/to/files/*.*);
do perl path/to/script/script.pl --i=$i > path/to/out/$i.new;
done;
{% endhighlight %}

##Multi rename
2. Remove a common suffix from several files:

{% highlight bash %}
for i in $(ls *.new);
do mv "$i" "`echo $i | sed 's/\.new$//g'`";
done;
{% endhighlight %}

##Pipe, pipe i love pipe
3. Extract from a set of formatted files rows with some special words avoiding other ones:

{% highlight bash %}
grep "\-YES\-" * |
grep -v "NO" |
grep -v "ERROR" |
awk '{print $2}' |
sed 's/key=//g' |
sort -u > tmp.txt
{% endhighlight %}