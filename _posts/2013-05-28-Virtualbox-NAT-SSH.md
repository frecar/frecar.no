---
layout: post
---

From time to time, you need to set up a Virtualbox machine and connect with ssh.
The problem is that the default network configuration use NAT, this mean the machine does not have it's own IP-adress.

The easy solution is to set the machine in "Bridged mode", which is shown in these screenshots.
<img src="{{ site.url }}/static/illustrations/virtualbox_nat_step1.png" alt="step1" style="width: 150px;"/>
<img src="{{ site.url }}/static/illustrations/virtualbox_nat_step2.png" alt="step2" style="width: 500px;"/>

But in some network, this is not possible. Another solution is to create a reverse ssh tunnel. To do this
you need to know your own machines ip address, and be able to log on to virtual machine in Virtualbox.

In the virtual machine terminal, type

{% highlight sh %}
$ ssh -R 4000:localhost:22 frecar@your-machine-ip
{% endhighlight %}

What this does is to open a reverse ssh connection from the virtual host to your computer. This means that any connection
to port 4000 on your own machine wil redirect to port 22 on your virtual machine.

To connect to your virtual machine, type

{% highlight sh %}
$ ssh frecar@127.0.0.1 -p 4000
{% endhighlight %}