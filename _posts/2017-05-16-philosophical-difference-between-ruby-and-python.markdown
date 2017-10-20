---
layout: post
title:  Philosophical difference between ruby and python.
date:   2017-05-16 14:30:12 +0000
---


Example:

{% highlight python %}
    $ irb
    irb(main):001:0> exit
    $ irb
    irb(main):001:0> quit

    $ python
    >>> exit
    Use exit() or Ctrl-D (i.e. EOF) to exit
{% endhighlight %}

**Ruby** follows POLS, principle of least surprise i.e. it accepts both exit and quit to accommodate programmer's obvious desire to quit terminal. Ruby behave as the programmer's expects it to behave. This often leads to having more than one way to do the same thing.

**Python** follows "One right way to do things". python here explicitly instructs programmer to do the right or the proper thing, even though it is obvious to python that user wants to quit terminal. Python is explicit in everything.

Happy Coding.:)