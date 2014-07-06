---
layout: post
---

In Python we can iterate any iterable easy with a for in loop.

{% highlight py %}
for x in list:
    do_something(x)
{% endhighlight %}

Usually we iterate through lists, for example [1,2,3]
{% highlight py %}
for x in [1,2,3]:
    do_something(x)
{% endhighlight %}

We can generate new lists easily by using range(0,limit)
{% highlight py %}
for x in range(0,10):
    do_something(x)
{% endhighlight %}

But what if the list is very large, what if you don't really need the entire list.. It would be unnecessary to create the entire list up front.
In Python we can use generators to make a partial list, xrange is a brilliant example of this.  If we loop trough a xrange, instead for range, we don't create the entire list up front, we only keep track of the "next" element in the list.
The syntax is the same, the difference is that xrange will only evaluate the next element, so if we want to break the loop on a condition, we don't waste memory.

{% highlight py %}
for x in xrange(0,10):
    if(do_something(x)) == "done":
        break
{% endhighlight %}


But the real power comes when you create your own generators, it is very easy. This is a implementation of xrange.

{% highlight py %}

def generator(start, stop):
    x = start
    while x<stop:
        x+=1
        yield x

for x in generator(0,10):
    if(do_something(x)) == "done":
        break

{% endhighlight %}

