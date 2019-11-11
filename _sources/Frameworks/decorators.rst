Python Decorators
=================

One of the cool things about learning Python Frameworks is that you get to dig into some advanced Python features.  In our hello world example we mapped Python functions to URL's using Python decorators, Now its time to see how decorators work, and a simplified implementation of how Flask uses the concept to call a particular function based on a URL.

Before we go there, lets look at a simpler example of a decorator to get an idea of how they work.  First lets start with a definition.  A decorator is a *callable* that takes a function as an argument and returns a replacement function.

Lets write a simple decorator that we can use so that a function can automatically keep track of the number of times it has been called.  This can sometimes be very useful for performance testing or debugging.

The ``call_counter`` function in the code below is a decorator, it takes a function as an argument, and returns a replacement function. The replacement function, called ``wrap``, is defined inside the ``call_counter`` function.

First we define the wrap function which does two things.  First, it increments a counter attribute of itself, and then returns the result of calling ``func``, passing along any and all arguments.  ``*args`` allows you to define a function that accepts a variable number of parameters, and ``**kwargs`` allows you to have any number of named parameters.  This topic could be another whole chapter, but for now you can read a nice `concise description here. <http://markmiyashita.com/blog/python-args-and-kwargs/>`_

You may be confused by the line ``wrap.counter += 1``.  But remember that in Python functions are objects like any other object.  We can always add attributes to objects by just using the dot notation and assigning.  Alternatively we could be really explicit about adding an attribute using ``setattr(wrap,'counter',0)``.  So all the wrap function does is add the ability to increment a private counter each time wrap is called, and then call the original function.

Here is the real key ``@call_counter`` notation before the  definition of fib, is the equivalent of adding the line``fib = call_counter(fib)`` after the function is defined.  You can comment out the ``@call_counter`` line and prove this to yourself.

.. code-block:: python

    def call_counter(func):
       def wrap(*args, **kwargs):
           wrap.counter += 1
           return func(*args,**kwargs)
       wrap.counter = 0
       return wrap

    @call_counter
    def fib(n):
        if n <= 1:
            return 1
        else:
            return fib(n-1) + fib(n-2)

    for i in range(20):
        print(fib(i), fib.counter)
        fib.counter = 0

The idea of wrapping a function like this may seem awkward at first but it is a really cool feature, and one that you will use more often once you become familiar with it.  In the functional programming world functions that take other functions as arguments and manipulate them in some way are called higher order functions.

Think about the wrap function in the previous example more generally:

.. code-block:: python

   def decorator(func)
      # set up an environment
      def wrap(*args, **kwargs):
         # manipulate any arguments
         # use the environment
         res = func(*args, **kwargs)
         # manipulate the result
         # change the environment
         return res
      return wrap

OK, hopefully you are still with me.  Lets look at another way of implementing the same functionality as the ``call_counter`` decorator but we will do it in a slightly different way.  In the definition of a decorator I used the term *callable*.  In Python callable means any object that understands the use of the () as call operators.  Huh?  Take a look at this example:

.. activecode:: dec_callable

   class MyClass:
       def __init__(self, name ):
           self.ivar1 = name

       def __call__(self, x, y):
           print("Hello: {0}".format(self.ivar1))
           sum = x+y
           print("the sum is {0}".format(sum))
           return sum

   foo = MyClass('brad')

   foo(2,9)

In the example above foo is clearly an instance of ``MyClass``.  But because we implement the "dunder method" ``__call__`` we can treat this instance of the class just like a function.

Lets write a new version of our call counter as a class:

.. code-block:: python

   class BetterDecor:
       def __init__(self,func):
           self.counter = 0
           self.func = func

       def __call__(self, *args, **kwargs):
           self.counter += 1
           return self.func(*args,**kwargs)

   @BetterDecor
   def fib(n):
       if n <= 1:
           return 1
       else:
           return fib(n-1) + fib(n-2)

   @BetterDecor
   def fact(n):
       if n <= 1:
           return 1
       else:
           return n * fact(n-1)

   fib(20)
   fact(100)
   print(fib.counter)
   print(fact.counter)

The use of a class in this way is nice because we don't have to clutter our function object with extraneous attributes.  We also don't have to define functions within functions because the ``__init__`` method for the BetterDecor class serves as the outer layer of the decorator, it accepts the function as its parameter and stores away the function in an instance variable!

I recommend you take a short break at this point, especially if your head is spinning from the last few examples.  The next part is even more head spinning.

Consider the decorator used in our hello world flask example.  Oh yeah, this was supposed to be about flask and web programming right?  ``@app.route('/user/<name>')``   Do you see anything wrong with this picture?  If a decorator is a function that takes another function as an argument then what is the deal with the ``('/user/<name>')`` part of the equation.  It looks like we have used up our allotment of parameters with the string, where does the function go?

In this case the decorator is a function that takes some other arguments and returns a function that accepts a function as a parameter and returns a replacement for the function.  Holy levels of abstraction batman.

Here is a simple example that may actually be easier to understand than the previous few sentences:

.. code-block:: python

   def argdec(x,y,z):
      a = x + y + z
      def wrap(func):
         def wrapped_f(*args, **kwargs):
            print('the original args were ', x, y, z)
            print('remember good old a', a)
            func(*args, **kwargs)
         return wrapped_f
      return wrap

Functions within functions within functions.  When the line ``@argdec(1,2,3)`` is executed The ``@`` operator evaluates whatever comes after it.  In the first examples what came after the @ was the name of a function which simply evaluates to the function the name refers to.  In this case we evaluate an actual function call which happens to return a function.   during evaluation the argdec function is called passing the parameters 1,2,3.  The call to argdec computes a  value for ``a`` and defines wrap.  It then returns wrap.  Remember that nothing inside the wrap function is executed just yet.  Next the result of evaluating argdec(1,2,3) is called passing along the function we are decorating. which causes the ``wrapped_f`` function to be defined and returned.

Recall that for the non argument version of a decorator foo, for function bar we said it was equivalent to writing ``bar = foo(bar)``  In the case of using ``argdec`` to wrap bar it would be equivalent to writing ``bar = argdec(1,2,3)(bar)``  This might look funny, but if you think about evaluating the right hand side of the assignment statement from left to right it actually makes sense.  evaluate argdec(1,2,3) which returns wrap, now call wrap(bar) which returns wrapped_f.

Using classes to implement decorators that take arguments is actually quite nice because we can use the constructor for our class as the outer layer and the ``__call__`` method to do the wrapping.

Its a little bit off the wall, but lets say we want to implement our call counter to take an initial value, and the time at which the function was defined.

.. code-block:: python

   class ccc:
       def __init__(self,start_val, current_time):
           self.counter = start_val
           self.define_time = current_time

       def __call__(self, func):
           def wrap(*args, **kwargs):
               self.counter += 1
               return func(*args, **kwargs)
           wrap.wrapper = self
           return wrap
   import time

   @ccc(0,time.time())
   def fib(n):
       if n <= 1:
           return 1
       else:
           return fib(n-1) + fib(n-2)

   print(fib(30))
   print(fib.wrapper.counter)
   print(fib.wrapper.define_time)


Finally, lets consider what our ``app.route`` decorator does.  The app object is our Flask application object, and it will be used to dispatch the correct function based on the URL.  So this decorator is not even really going to wrap the function in question, but rather store away a reference to the original function in a dictionary

.. code-block:: python

   class funcmapper:

       def __init__(self):
           self.funcdict = {}

       def route(self,pattern):
           def wrap(func):
               self.funcdict[pattern] = func
               return func
           return wrap

       def namecall(self,name, *args, **kwargs):
           if name in self.funcdict:
               self.funcdict[name](*args,**kwargs)

   app = funcmapper()

   @app.route('/')
   def hello():
       print("hello world")

   app.namecall('/')
   print(hello)


