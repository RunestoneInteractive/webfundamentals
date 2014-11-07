Cookies
=======

.. image:: Figures/Double-Stuf-Oreos.jpg
   :width: 400px
   

HTTP is a stateless protocol.  This means that from one request to the next HTTP does not know anything about the state of the webpage you are looking at.  This is a good thing, from the perspective of scale, but it does provide some challenges as well.  How does the server "know" your name every time you come back to Google or Amazon?

The answer is, of course, cookies.  Early on they were called "magic cookies," but lately that has been shortened to just cookies.  A cookie is a small chunk of information (maximum 4096 bytes) that the web **browser** stores on behalf of the web **server.**  The information is sent to the server from the browser along with every request.

The cookie information is transferred back and forth as part of the header in the request and the response.  The server asks the browser to store some information using a ``Set-Cookie`` header, and the browser gives the information back to the server using a ``cookie`` header.

Here is an example of a Set-Cookie header:

::
    
    HTTP/1.0 200 OK
    Content-type: text/html
    Set-Cookie: name=value; Expires=Wed, 09 Jun 2021 07:21:14 GMT; Path=/
    

Besides the name value pair for storing your application data, cookies may have the following attributes:

* Expires -- How long should the browser store this cookie?  By default the cookie will only be stored as long as the browser is open.  When you quit and restart the browser the cookie will be gone.  However you can set a date in the future that will cause the browser to store the cookie until that time.
* Domain -- By defualt, the browser should only return the cookie to the domain that issued it.  For example, www.luther.edu  However the server may set luther.edu as the domain so that the cookie will be supplied to any server inside the luther.edu domain.
* Path -- By default the path is / such that any URI on the server will get the cookie, but the server may restrict this by setting a path such as /api so that only requests that begin with /api will receive the cookie.

The browser supplies the cookie information back to the server using a header like this:

::

    GET /interactivepython.html HTTP/1.1
    Host: www.luther.edu
    Cookie: name=value; name2=value2
    Accept: */*
    

Let us make one final modification to our hello world cgi program and store the users name in a cookie.  This will allow us to avoid asking the user their name every time.  

Our program logic gets just a bit more complicated yet again as now we need to check the ``QUERY_STRING`` to see if the name has been supplied there, and we also need to check for the cookie.  Cookie information is supplied to the CGI program through the environment variable ``HTTP_COOKIE``.  The helper functions do not change, but the main logic of our program now looks like this:

.. code-block:: python

   cookies = os.environ['HTTP_COOKIE']
   if not qs:
       if cookies and 'firstname' in cookies:
           sendHeaders()
           cvalues = cookies.split(';')
           for c in cvalues:
               if 'firstname' in c:
                   name = c.split('=')[1]
           sendPage(name)
       else:
           sendHeaders()
           sendForm()
   else:
       if 'firstname' in qs:
           name = qs.split('=')[1]
           headers.append("Set-Cookie: firstname=%s" % name)
       else:
           name = 'No Name Provided'
       sendHeaders()
       sendPage(name)

