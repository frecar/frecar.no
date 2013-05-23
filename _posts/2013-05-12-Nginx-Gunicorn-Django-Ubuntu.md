---
layout: post
---


First all of all, you have to set up a virtualenv. To do this, you need to have virtualenv installed
{% highlight sh %}
$ pip install virtualenv
{% endhighlight %}

Set up your environment, the --no-site-packages mean that this environment is totally isolated from your site-packages
installed on your computer.

{% highlight sh %}
$ virtualenv venv --no-site-packages
$ cd venv
$ source activate

{% endhighlight %}
