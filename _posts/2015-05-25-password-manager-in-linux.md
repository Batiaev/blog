---
layout: post
title:  "Password manager in Linux"
date:   2015-05-25 22:40:11
categories: password linux pass pgp
---
Official site: [http://www.passwordstore.org/](http://www.passwordstore.org/)

##Installing
{% highlight bash %}
sudo aptitude install pass pgp
gpg --gen-key
eval $(gpg-agent --daemon)
pass
pass generate email/anton@batiaev.com 25
{% endhighlight %}