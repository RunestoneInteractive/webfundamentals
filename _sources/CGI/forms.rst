Processing user Input
=====================

In the Javascript chapter we looked at a number of HTML tags for processing user input.  If that user input needs to go back to the web server, then we need to enclose our input elements, and a submit button inside a ``form``.

When we submit a form, the browser packages up all of the data we have entered into the input elements and sends them back to the server, and your program for processing.

Lets change the hello.py program we wrote earlier to have a form where you can enter your name.  After you click on the submit button the page will display ``Hello yourname`` rather than ``Hello World``.  Although it sounds simple, this program will provide us with several avenues to further explore the relationship between the browser, the server, and our cgi program.


Lets start with a basic page with a form.

.. code-block:: html

   <html>
     <body>
         <form action='cgi-bin/hello2.py' method='get'>
             <label for="myname">Enter Your Name</label>
             <input id="myname" type="text" name="thename" value="Nada" />
             <input type="submit">
         </form>
     </body>
   </html>
   
There are two important attributes on the form tag:

* method: this tells the browser which http method to use when submitting the form back to the server.  The options are ``get`` or ``post``.

* action: This tells the browser the URL to use when submitting the form.

The input type ``submit`` renders as a button in the form.  The purpose of this input type is to cause the form to be submitted back to the web server.

.. code-block:: python

   #!/usr/bin/env python
   import os

   print "Content-type: text/html\n"

   qs = os.environ['QUERY_STRING']
   if 'thename' in qs:
       name = qs.split('=')[1]
   else:
       name = 'No Name Provided'

   print "<html>"
   print "<body>"
   print "<h1>Hello %s</h1>" % name
   print "</pre>"
   print "</body>"
   print "</html>"

