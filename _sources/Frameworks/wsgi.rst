Web Server Gateway Interface
============================

The Web Server Gateway Interface (WSGI) and pronounced Whiskey (what else would you put in your Flask?).  Is a standard defined by the Python Software Foundation that describes how a web server communicates with a web application.  In addition the specification allows for applications to be layered in order to respond to a single request.

A web server that is WSGI compliant only receives a request and passes the request on to an application object, it then forwards the response from the object back to the browser.

From our perspective as application builders, WSGI is very simple.  It has the following four features:

* WSGI applications are **callable** python objects (functions or classes with an ``__call__`` method that are passed two arguments: a WSGI environment as first argument and a function that starts the response.

* The application has to start a response using the function provided and return an **iterable** where each yielded item means writing and flushing.

* The WSGI environment is like a CGI environment just with some additional keys that are either provided by the server or a middleware.

* You can add functionality to your application in a general way by wrapping the application in another WSGI compliant application.

The Application Callable
------------------------

The ``app`` object created by ``app = Flask(__name__)`` is a WSGI compliant object, meaning that it is a callable, that takes two parameters, an environment dictionary and a function.  It returns an iterable.  It is quite complex and does a lot of work for us behind the scenes.  To get a better appreciation for that, lets look at a simpler version of a WSGI compliant object, a function called ``hello_world``.

.. code-block:: python

   from cgi import parse_qs

   def hello_world(environ, start_response):
       # parse_qs turns QUERY_STRING into a nice dictionary
       parameters = parse_qs(environ.get('QUERY_STRING', ''))
       if 'subject' in parameters:
           # all values are lists, to accommodate checkboxes
           subject = parameters['subject'][0]
       else:
           subject = 'World'
       start_response('200 OK', [('Content-Type', 'text/html')])
       return ['''Hello {subject} Hello {subject} '''.format(subject=subject)]

   if __name__ == '__main__':
       from wsgiref.simple_server import make_server
       srv = make_server('', 8000, hello_world)
       srv.serve_forever()


First, an example of parse_qs:

::

    >>> parse_qs("foo=bar&blah=baz")
    {'foo': ['bar'], 'blah': ['baz']}
    >>> parse_qs("foo=bar&blah=baz&foo=sdfsdf")
    {'foo': ['bar', 'sdfsdf'], 'blah': ['baz']}
    >>>


.. fillintheblank:: first_wsgi
                    
    Run the example above in a terminal window.  What does your browser display?

    - :Hello World Hello World:  Correct!
      :Hello World: Not quite, look closer
      :x: Hint: Hello ????

The ``wsgiref.simple_server`` is a simple web server instance that acts as a container for our WSGI object.  Every time a request comes in, the hello world function is called passing in the environ object and a function that it provides that we can call to provide our response status as well as any headers we want to set up.

In our ``hello_world`` function we check to see if there is a name called ``subject`` in the QUERY_STRING.    We then call the ``start_response`` function to set up our response code and content-type header.  Finally we return an iterable -- in this case a string -- that will be returned to the browser to be rendered.

Lest you think this is overly simple, we can even do some routing in this function by looking at the ``PATH_INFO`` environment variable.  Try this yourself. Modify the hello world function to return Hello, if the route is ``/hello`` and Goodbye if the route is ``/bye``

Write a single function with a big long if statement is not a very scalable way to build a web development framework.  So lets make some improvments.  First instead of a function lets create a class where the instances of the class are **callable**.

Our app object in Flask is an instance of the Flask class.  Lets look at a simpler class based implementation of a WSGI app, and then look at another example that points us in the direction of how Flask extends the idea into a full framework.

We will do this by implementing a base class that implements most of the WSGI deails and leaves the actual application code up to us.  All we will need to do is write a class that inherits from our class and implements a ``get`` method.

.. code-block:: python

   from cgi import parse_qs
   class WSGIRequestHandler:

       def __init__(self):
           self.request = {}
           self.response = {'Content-Type':'text/plain'}

       def __call__(self, environ, start_response):

           appiter = None
           self.request['args'] = parse_qs(environ['QUERY_STRING'])
           appiter = self.get()
           start_response('200 OK',list(self.response.items()))
           for item in appiter:
               yield item

           # wsgi applications might have a close function. If it exists
           # it *must* be called.
           if hasattr(appiter, 'close'):
               appiter.close()

   class Hello(WSGIRequestHandler):
       def get(self):
           name = self.request['args'].get('subject','world')
           return ['Hello {0}'.format(name)]

   if __name__ == '__main__':
       from wsgiref.simple_server import make_server
       srv = make_server('localhost', 8080, Hello())
       srv.serve_forever()


This example illustrates an instance of a class as a callable, that implements the WSGI interface.  Further it shows a way that we can hide much of the details of the WSGI interface from application programmers by using inheritance.

The WSGIRequestHandler class implements an  ``__call__`` method that relies on a subclass that implements a get method to build the actual page.  Different applications can implement many subclasses of the WSGIRequestHandler class to handle the various requests.

The ``__init__`` method creates two instance variables to handle response headers, as well as incoming environment variables such as cookies and arguments from a submitted form.

the main program in this script imports a make_server function which assembles a web server to handle WSGI requests, on a host, port.  It also needs a callable application object.  In this case an instance of the Hello class.  We will shortly look at how add dispatch functionality to the example to show how to make a WSGI server that can map URLs to classes so thate it can respond to a variety of requests.

There are two big things that we want to add to our WSGI application:

1.  URL mapping
2.  Error Handling


In the decorators module we looked at how Flask uses decorators to associate a function with a particular URL pattern.  In this section we will not use a decorator but will just create a list of URL to callable mappings directly and see how that works with the rest of our implementation.

.. code-block:: python

   urls = [
       (r'^$', Index),
       (r'hello/?$', Hello),
       (r'goodbye/?)$', Goodbye)
   ]


This list of tuples maps three differnt patterns to 3 different callables that provide a simple response.  All of them are very similar to the Hello class shown above.

Given that list we need an WSGI compliant callable that can examine the incoming request and forward the call to the appropriate class.

.. code-block:: python

   def router(environ, start_response):
       path = environ.get('PATH_INFO', '').lstrip('/')
       for regex, callback in urls:
           match = re.search(regex, path)
           if match is not None:
               environ['myapp.url_args'] = match.groups()
               return callback()(environ, start_response)
       return not_found(environ, start_response)

   def not_found(environ, start_response):
       """Called if no URL matches."""
       start_response('404 NOT FOUND', [('Content-Type', 'text/plain')])
       return ['Not Found']

Now the main program looks like this:

.. code-block:: python

   if __name__ == '__main__':
       from wsgiref.simple_server import make_server
       srv = make_server('localhost', 8080, router)
       srv.serve_forever()

The router callable is passed in to the server as the main application object.  The keys to the router function are as follows:

1.  Extract the path from the incoming PATH_INFO environment variable
2.  Match that path against the regular expressions provided in the urls list.
3.  Forward the request to the callable that should handle it using the following:  ``return callback()(environ,start_response)``

That last line looks a bit crazy, so let's break it down.  Remember that WSGI compliant callables must accept an environment and a start_response function,  and they must return an iterable.  So the return statement must first evaluate its argument:  ``callback()(environ,start_response)``.  This is evaluated from left to right.  The reference ``callback`` is set in the for loop and will be set to the callable that matches the current regular expression.  In our class This will be a class.  So ``callback()`` creates an instance of the class that matches the regular expression.  As soon as the instance is created its ``__call__`` method is invoked by the ``(environ,start_resonse)`` operator.  Which in turn will invoke the ``get`` method on the class which returns an iterable.  That iterable is returned by the return statement in the router function.

OK, so now that we can call the right function, let's look at how to handle errors the WSGI way.  Error handling is a nice example of how you can use middleware.  Or you can think of it in Shrek terms:  Applications are like Ogres, they have layers.  To implement a middleware layer we simply implement another WSGI compliant class, that takes an inner WSGI object as a parameter for its constructor.  Each outer layer has access to the results of the layer below it, and can modify the results of the layer below it before returning it to the layer above.

.. code-block:: python

   class ExceptionMiddleware:
       """The middleware we use."""

       def __init__(self, app):
           self.app = app

       def __call__(self, environ, start_response):
           """Call the application can catch exceptions."""
           appiter = None
           # just call the application and send the output back
           # unchanged but catch exceptions
           try:
               appiter = self.app(environ, start_response)
               for item in appiter:
                   yield item
           # if an exception occours we get the exception information
           # and prepare a traceback we can render
           except:
               e_type, e_value, tb = exc_info()
               traceback = ['Traceback (most recent call last):']
               traceback += format_tb(tb)
               traceback.append('%s: %s' % (e_type.__name__, e_value))
               # we might have not a stated response by now. try
               # to start one with the status code 500 or ignore an
               # raised exception if the application already started one.
               try:
                   start_response('500 INTERNAL SERVER ERROR', [
                                  ('Content-Type', 'text/plain')])
               except:
                   pass
               yield '\n'.join(traceback)

           # wsgi applications might have a close function. If it exists
           # it *must* be called.
           if hasattr(appiter, 'close'):
               appiter.close()

You will notice that this is a very similar class to the base class for WSGI applications except that it handles the call to the lower layer inside a try/except block.  If any of the lower layers fail they will be caught by the try except at this layer and the traceback will be rendered on the browser page, along with the 500 internal server error message.  There are many uses for middleware including session management, form authentication, You can find a list of open source WSGI middleware handling user login/logouts, and more you can find a list `here <http://wsgi.readthedocs.org/en/latest/libraries.html>`_. Although for our continued use of Flask these are not necessary, as we will be using some extensions that are specific to flask, which may very well be implemented using the middleware pattern.

