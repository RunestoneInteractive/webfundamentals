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

The ``app`` object created by ``app = Flask(__name__)`` is a WSGI compliant object.  It is quite complex and does a lot of work for us behind the scenes.  To get a better appreciation for that, lets look at a simpler version of a WSGI app.

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
       srv = make_server('localhost', 8000, hello_world)
       srv.serve_forever()


First, an example of parse_qs:

::

    >>> parse_qs("foo=bar&blah=baz")
    {'foo': ['bar'], 'blah': ['baz']}
    >>> parse_qs("foo=bar&blah=baz&foo=sdfsdf")
    {'foo': ['bar', 'sdfsdf'], 'blah': ['baz']}
    >>>


Our app object in Flask is an instance of the Flask class.  Lets look at a really simple class based implementation of a WSGI app, and then look at another example that points us in the direction of how Flask extends the idea into a full framework.

.. code-block:: python

   from cgi import parse_qs
   class WSGIRequestHandler(object):

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

The ``__init__`` method creates two instance variables to handle common

