Template Engines
================

There are many benefits to using templates.  

* Separation of the view from the controller and model code.
* Increased productivity.
* Ease of creating a site with a unified design.
* Division of labor.  Designers can now work on template files using html plus a bit more without needing to know how to write Python.

At the simplest level templates are not much different than a Python formatted string.  However they are much more convenient to use, and have many more features that we will explore shortly.  Here is a simple example:

.. code-block:: python

   from jinja2 import Template
   template = Template('Hello {{ name }}!')
   template.render(name='John Doe')

A slightly more complicated example goes like this:

.. code-block:: python

   from jinja2 import Environment, FileSystemLoader
   env = Environment(loader=FileSystemLoader('/path/to/templates))
   t = env.get_template('foo.html')
   t.render(name='Luther')
   
This example shows how we can set up an environment that can be shared among many functions.  This environment takes care of the details behind locating and reading our templates from a file when we want to use them.  The foo.html file could look like this:

.. code-block:: html

   <html>
       <body>
       <h1>Hello {{ name }}</h1>
       </body>
   </html>

The values inside the double curlies are not limited to being string objects, although they must have an ``__str__`` method if they are going to be useful.  Consider an instance of a Student class that has instance variables for firstname, lastname, and gpa.  Lets change our template to look like the following:

.. code-block:: html

   <html>
       <body>
           <h1>Hello {{ s.firstname }} {{ s.lastname }}</h1>
           <p>Your gpa is {{ s.gpa }}.</p>
       </body>
   </html>


Assuming we have a student object called joe we can render the template above with the line:  ``t.render(s=joe)``  This would also work if joe was a dictionary and had keys firstname, lastname, and gpa.  The dot notation works for either attributes or items in a dictionary  (``__getattr__`` or ``__getitem__``) for those of you who like magic method speak.


Loops in Templates
------------------

Lets suppose you want to make a table in a template.  The ideal would be to pass render a list of things, and have the template turn the list into a table.  (or an unordered list or whatever)  This is easy to do.

.. code-block:: html

   <html>
       <body>
           <h1>The first {{ plist|length }} prime numbers</h1>
           <table>
               {% for i in plist: %}
                   <tr><td>{{ i }}</td></tr>
               {% endfor %}
           </table>
       </body>
   </html>
   

This introduces several interesting new features of templates. 

1.  The ``{% ... %}`` notation is used to include a non-rendering bit of code in the template.  In this example we introduce a for loop.  Notice that since html does not require you to indent things we need an endfor to delimit the end of the for loop.

2.  Jinja2 includes a huge number of filters that you can use on a variable.  The filter ``plist|length`` will render as the number of elements in the plist list.


Conditionals in Templates
-------------------------



