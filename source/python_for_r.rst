
Note to R Users
=========================

Welcome R users!

Most of the recent innovations in Python tools for data science were created by frustrated R users, which means you'll find that many of the things you love about R are preserved in Python, while many of the frustrations you may have have been been addressed. Below are some links to great tutorials on Python (no reason to reinvent the wheel), but first let's highlight some of the things you as an R user will find especially useful/surprising.

* **Analogues for `data.frames` and `vectors` are in `pandas` library, not Python itself**: When you watch basic Python tutorials, you'll find yourself wondering where the vectors and data.frames are -- don't worry! They exist, but they're in a different library called `pandas`, so basic Python tutorials won't talk about them. This site is organized to point you to basic Python tutorials that will just cover what you need to know, then move you to `pandas` tutorials, which is what you'll be using for most of your work.
* **Periods are operators in Python**: In R, it's common to use periods in variable names (like: `my.list`). There are many syntax differences between R and Python, but for some reason people really struggle with this one -- periods are an operator in Python, so don't use them in names! The convention is to use underscores, like: `my_list`.
* **In Python you always count starting at 0, not 1** For example, the first row of a data frame is numbered 0, not 1.


Key Concepts: References
^^^^^^^^^^^^^^^^^^^^^^^^

Before you dive into general-purpose tutorials on Python syntax, there's one large conceptual change you should be aware of coming from R.

Say you make a new vector as follows:

``my.list <- list(1,2,3)``

In R, there's no difference between a variable (like ``my.list``) and the object (the list 1, 2, 3) associated with it. But this is actually a slight of hand used by R to hide something fundamental about how computers work, and it does not happen in Python.

In Python, when you create an object like a `list`, Python puts that list somewhere in memory, kind of like you might put something big on a shelf somewhere in a warehouse. The variable associated with that `list` (``my.list``) is not the same as that list -- it actually just stores the location on the shelves where you placed that list. And because this behavior is normal in most languages, you may not see it emphasized in Python tutorials written by programmers not coming from R.

The reason this matters is that it's possible for multiple variables to be pointed at the same item on a shelf, which means if you do something to one variable, it changes the item on the shelf, and so if you call the other variable that points to that item on a shelf, you will find the change affected both items. For example:

.. ipython:: python

    # Make a new list
    x = [1, 2, 3]
    # Make new var Y, and assign it x. In R this would make a copy.
    y = x
    # Add to the end of the string
    x.append(4)
    # We see this new addition is now at end of x
    x

    # But look! It's also at the end of y!
    # That's because they both point at the same list on the shelf.
    y


If what you want to do is make a *copy* of x, you use the `copy()` command:

.. ipython:: python

   x = [1, 2, 3]
   y = x
   y_copy = x.copy()
   x.append(4)
   y_copy

If you want to see if two variables point to the same thing, you can use the `is` operator, which tests whether two variables are pointed at the same place in memory / same shelf:

.. ipython:: python

   x is y
   x is y_copy

Mutable versus Immutable Types
""""""""""""""""""""""""""""""

However, there are three exceptions to this behavior. Certain data types in Python are called "immutable", meaning that if you try to change them, Python can't modify the item that's already sitting on the shelf; instead, it has to create a new item on a different shelf and redirect the variable to point at that new item. There are only three of these: strings, plain numbers, and tuples (a Python data structure you don't really need to worry about now). So:

.. ipython:: python

   # Make x a simple number
   x = 5
   y = x

   # Modify x
   x = x + 1
   x

   # y is unchanged because x + 1 actually created a new "6" on a new shelf, and x changed from points
   # to 5 to pointing to 6
   y

OK, that's it -- that's the one big, weird conceptual change to be aware of!

Next Steps
^^^^^^^^^^

OK, so here's the best approach to getting going with Python:

#. Do a basic Python tutorial (won't talk about data frames or vector data)
#. `pandas` tutorial (where you find analogues to data frames and vectors)
#. `statsmodels` tutorial (for econometrics)
#. `seaborn` tutorial (equivalent for ggplot)
