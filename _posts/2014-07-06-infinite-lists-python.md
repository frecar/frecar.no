---
layout: post
---

When you need to solve a problem and use lists of unknown size, you should use generators to not waste memory.
You can easily make use of generators to create infinite lists in Python.

{% highlight py %}

def inf_list(start=0):
    x = start
    while True:
        x+=1
        yield x

#Never ending loop
for x in inf_list():
    print x

"prints 0, 1, 2 ..."


#More examples using custom operaotrs
from operator import add, sub

#Using add operator, increasing list
def inf_list(x=0, op=add):
    while True:
        yield x
        x = op(x, 1)

#Never ending loop..
for x in inf_list():
    print x

"prints 0, 1, 2 ..."


#Using sub operator, decreaseing list
def inf_list(x=0, op=sub):
    while True:
        yield x
        x = op(x, 1)

#Never ending loop..
for x in inf_list():
    print x

"prints 0, -1, -2..."


{% endhighlight %}


### When and how to use this?

Say you want the first 1000 numbers divisible by 3, but you don't know how large the list needs to be.

{% highlight py %}

def inf_list(start=0):
    x = start
    while True:
        x+=1
        yield x

numbers_divisible_by_three = []

for x in inf_list():
    if len(numbers_divisible_by_three) >= 1000:
        break
    if(x%3)==0:
        numbers_divisible_by_three.append(x)

print numbers_divisible_by_three

{% endhighlight %}


### More advanced usage

Generators are powerful and since they are iterators, we can create a more general solution to the previous example.

{% highlight py %}

def inf_list(start=0):
    x = start
    while True:
        x+=1
        yield x

def filter_list(func, list, result_size=None):
    result = []
    for x in list:
        if result_size and len(result) >= result_size:
            break
        if func(x):
            result.append(x)
    return result

#Get the 1000 first elements divisible by given integer
print filter_list(lambda x: x % 1 == 0, inf_list(), 1000)
print filter_list(lambda x: x % 2 == 0, inf_list(), 1000)
print filter_list(lambda x: x % 3 == 0, inf_list(), 1000)
print filter_list(lambda x: x % 4 == 0, inf_list(), 1000)
print filter_list(lambda x: x % 150 == 0, inf_list(), 1000)


{% endhighlight %}

#### Use generators to calculate prime numbers

{% highlight py %}

import itertools
import math


def inf_list(start=0):
    x = start
    while True:
        x += 1
        yield x


def filter_list(func, list, result_size=None):
    result = []
    for x in list:
        if result_size and len(result) >= result_size:
            break
        if func(x):
            result.append(x)
    return result


#Simple prime number number checker, just for this example
def is_prime_number(n):
    if n % 2 == 0 and n > 2:
        return False
    return all(n % i for i in range(3, int(math.sqrt(n)) + 1, 2))


#Get the first 1000 prime numbers
def get_n_first_prime_numbers(n):
    return filter_list(is_prime_number, inf_list(), n)


print get_n_first_prime_numbers(1000)


#Get the nth prime number
def get_nth_prime(n):
    return filter_list(is_prime_number, inf_list(), n + 1)[n]


print get_nth_prime(500)

{% endhighlight %}

