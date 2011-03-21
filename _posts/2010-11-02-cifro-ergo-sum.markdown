---
layout: post
title: Cifro Ergo Sum
---

1. Generate a key-pair:
{% highlight bash %}$ gpg --gen-key{% endhighlight %}

2. Upload the key:
{% highlight bash %}$ gpg --send-keys --keyserver pgp.mit.edu $KEYID{% endhighlight %}

3. Revoke a key:
{% highlight bash %}$ gpg --gen-revoke $KEYID{% endhighlight %}
Save the certificate-block in <code>$FILE</code> .
Import the revocation certificate:
{% highlight bash %}$ gpg --import $FILE{% endhighlight %}
Check the key is correctly revoked:
{% highlight bash %}$ gpg --list-sigs $KEYID{% endhighlight %}
Should say *revoked* in the first line and *rev* in the second one.
Upload the revoked key:
{% highlight bash %}$ gpg --send-keys --keyserver pgp.mit.edu $KEYID{% endhighlight %}
  
4. List all keys:
{% highlight bash %}$ gpg --list-keys{% endhighlight %}

5. List a specific key:
{% highlight bash %}$ gpg --list-keys $NAME{% endhighlight %}
 or:
{% highlight bash %}$ gpg --list-keys $KEYID{% endhighlight %}
  
6. Export the public key (as text-file):
{% highlight bash %}$ gpg --export --armor $KEYID > pubkey.txt{% endhighlight %}

7. Export the private key (as text-file):
{% highlight bash %}$ gpg --export-secret-keys --armor $KEYID > pubkey.txt{% endhighlight %}

8. Import a public or private key:
{% highlight bash %}$ gpg --import $FILE
$ gpg --recv-keys --keyserver pgp.mit.edu $KEYID{% endhighlight %}

9. Interactively edit a key:
{% highlight bash %}$ gpg --edit-key $KEYID{% endhighlight %}

10. Encrypt symmetric (very strong):
{% highlight bash %}$ gpg --cipher-algo RIJNDAEL256 -o $CRYPT-FILE -c $PLAIN-FILE{% endhighlight %}

11. Decrypt symmetric:
{% highlight bash %}$ gpg --cipher-algo RIJNDAEL256 -o $PLAIN-FILE --decrypt $CRYPT-FILE{% endhighlight %}
