
Making Python faster
=======================

Tuning your code is a very easy way to waste lots of time. With that in mind, think carefully about how much energy it actually makes sense to invest in speeding up your code. If you have something that takes an hour to run, it may be annoying, but at the end of the day it may not be worth spending 2 hours figuring out how to speed up that code if you only need to run it a couple times to clean your data.

But, if you do indeed need to make code you've written faster, here are some words of guidance, written as a kind of "checklist" for approaching the problem from easiest to hardest solutions.

1. Find Your Bottlenecks!
--------------------------------------------

There's no reason to tune a line of code that is only responsible for 1/100 of your running time, so before you invest in speeding up your code, figure out what's slowing it down -- a process known as "profiling" your code. Thankfully, because this is so important, there are lots of tools (called profilers) for measuring exactly how long your computer is spending doing each step in a block of code.

The easiest way to profile your Python code is using the iPython `%prun` command (`documented here <https://ipython.org/ipython-doc/3/interactive/magics.html#line-magics>`_). If you haven't used iPython `magic` commands before, `you can learn more about them here <https://ipython.org/ipython-doc/3/interactive/tutorial.html#magic-functions>`_.

2. Check your memory management
--------------------------------------------

When your computer is manipulating data (defining variables, running regressions, etc), what its actually doing is grabbing a little bit of data from storage, moving it to the processor, doing math with it, and then putting it back in storage.

To simplify somewhat, we can think of your computer as having two forms of storage -- RAM (sometimes called main memory), and your harddrive. But these two forms of memory are very, very different. Your computer can grab data from RAM 100,000 times faster it can grab data on the harddrive. Because of this, your computer is much happier (and performs faster) when it's able to keep all the data you're working with in RAM. Indeed, if you're moving data back and forth to your harddrive, it's almost certainly the biggest bottleneck -- doing actual computations is almost instantaneous compared to moving data back and forth to your harddrive on modern computers.

`You can learn more about how to know if your computer is wasting time going back and forth to the harddrive here. <http://www.tadawiki.org/Big_Data#How_do_I_know_if_my_data_is_fitting_into_RAM>`_

**Important:** Just because your dataset is small enough it seems like it should fit into RAM doesn't mean this isn't relevant for you! Programs often make copies of your data when they manipulate it, so even if your dataset is 2gb and your have 8gb of RAM, the program you're using can very easy end up using all 8gb of RAM!

If you can't get your data into memory, head on over to the :doc:`Big Data page for tools! <t_big_data>` for appropriate tools!

3. Use other people's (compiled) functions
--------------------------------------------

As a general rule, code you write in Python is slow. But don't worry, it's not your fault; Python was written to minimize the amount of time it takes to write code, not to minimize the amount of time it takes for code to run. Anything written in Python will be slow compared to code written in a fast language like C or C++.

But interestingly, commands that other people have written that are available in Python are actually usually written in faster ("compiled") languages, like C++. As a result, whenever you have the choice between writing a function yourself or using a function in an established library, you're almost always better off using the command someone else wrote. 

As a result, looping over a vector and adding up each value will be much slower than using a dedicated function from `pandas` to do the same thing. 

Now, using other people's functions is not fool-proof -- some people write their libraries in Python (not a compiled language like C++), so they may run as slowly as your own commands. So if you can, check the documentation for whatever library you want to use to see whether it was written in C / C++ or not! But for big libraries -- like pandas, numpy, etc. -- you can probably assume the dedicated functions in the library are faster than anything you'll ever write. 


4. Use a "Just-In-Time Compiler" like numba
--------------------------------------------

If what's slowing you down is some type of numerical operation, there's an incredibly easy tool for speeding up your code: `numba`. Basically, you add one line above the function you want to speed up, and if the function only uses a certain subset of operations, it can immediately speed up by 10x - 100x or more. 

`Details of using numba with pandas <http://pandas.pydata.org/pandas-docs/stable/enhancingperf.html#using-numba>`_

If you want to know much more (like how it all works) you can find a `tutorial here <https://www.youtube.com/watch?v=eYIPEDnp5C4>`_ . 

5. Parallelize
---------------
Parallelization (which has it's own page Parallelization here) is often the first thing social scientists turn to to speed up code. Whether this is the right decision depends a lot on your situation, but a few facts:

* Parallelization is "sub-linear", meaning if you parallelize across two cores, you can except ~1.8x speedup at best. (More generally, for N cores, expect ~0.8*Nx speedups).
* Improving how your code is written can often yield much higher returns than parallelization, on the order of 5x, 10x, or 100x speed improvements.
* Using code that was written in C++ by someone else can yield 10x or 100x returns.

So, parallelization certainly isn't the best way to speed up your code. But if you read this and find yourself thinking "um, I still don't really what makes code fast versus slow" or "I've already tried all that and it's still too slow!", it's a good option.

`Here are some added considerations and vocabulary for parallelization. <http://www.tadawiki.org/Parallelization>`_

(I almost never use parallelization on my own work, so not sure of easiest resources. When I have, I've done it with `iPython parallelization <http://ipython.org/ipython-doc/dev/parallel/>`_, though I don't know it's the best tool.)

6. Cython
--------------------------------------------

One reason that Python code is relatively slow is that ever time code executes, Python has to spend time checking to see the type of each variable (integer, floating point number, string, etc.). There's a way to speed up Python massively by adding information about the types of your variables using a tool called Cython. It's not super-difficult to use, but it's also not nearly as easy as a tool like numba, so use it only if needed. (Also debatable if easier than parallelization).

`Here's a great tutorial on everything you could ever want to know about Cython. <https://www.youtube.com/watch?v=gMvkiQ-gOW8>`_ 

