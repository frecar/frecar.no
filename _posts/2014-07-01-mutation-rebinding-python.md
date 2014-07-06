In Python, one of the most important and fundamental concepts are bindings vs mutations.

Let's try one thing first, what happens if we do this?

{% highlight py %}

l = [1, 2, 3, 4, 5, 6]

for x in l:
    x = 0

for i in l:
    print(i)

{% endhighlight %}

It is tempting to say we change the values in the list to zeroes. But why is that not happening?
Whenver you say x = 0, or x = something, you <i>rebind</i> the x variable! It means to change what the x variable points to,
so for every element in the list, we rebind x to 0, we don't change the values in the list!

But is it possible to actually change the values in the list this way? Yes! Instead of rebinding the x variable, we can mutate the elements in the list.
In order to mutate the value, we need an mutable objects, and int's are not, we can create our own wrapper class called Integer, and mutate
the value of each of the elements.

{% highlight py %}

class Integer(object):
    def __init__(self, n):
        self.n = n

l = [Integer(1), Integer(2), Integer(3), Integer(4), Integer(5), Integer(6)]

for x in l:
    x.n = 0

for i in l:
    print i.n

{% endhighlight %}

In this example, we do not rebind the x variable, we rebind the x.n variable, and therefore change the value of x.n, whereas the x continue to be the
element in the list. We <i>mutate the x object</i>. The result is a list of the same objects, containing differents values for the n variable.
